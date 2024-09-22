Queueing jobs and running a Singularity container
========================================================

Most supercomputers use a system called `SLURM <https://slurm.schedmd.com/documentation.html>`__ to manage jobs and maximise cluster utilisation. 
There are two main workflows:

* Interactive mode, in which the user asks for resources, logs into the compute nodes and runs all they need to run
* Batch mode, in which the user prepares a ``submit`` script (usually Bash) that contains all the instructions to be executed. The script is then placed in the queue and runs without any further inputs. 

Interactive resources can be requested with the ``salloc`` command in the following fashion:

.. code-block:: bash

  $ salloc -n <n_cores> -t HH:MM:SS -A <allocation_number> -p <partition>

Most parameters are self-explanatory. ``-t`` is the wall time, ``-A`` is an allocation dependent on the project. ``-p`` is required by some clusters that have different types of nodes, e.g. Dardel has 
a set of nodes reserved for interactive use on a partition called ``shared`` and a set of nodes with GPUs (``gpu``). There are many other options that are explained `here <https://slurm.schedmd.com/salloc.html>`__. 
Once the requested resources are granted, a MPI job can be executed with ``srun -n <n_cores> my_command``; alternatively, the user can also ssh directly into the allocated node.

.. type-along:: 

  Let's book a node with a GPU to run our script:

  .. code-block:: console

    $ salloc -n 1 -t 00:50:00 -A pdc-bus-2024-8 -p gpu --gpus=1

  Once we get our node, we can train our model:

  .. code-block:: console
    
    $ srun -n 1 singularity exec --rocm -B ./models:/models /cfs/klemming/projects/supr/bustestingshared/ENCCS/rocm_tensorflow/ python models/unet/main.py
  
  The ``-B`` flag is used to bind a directory on the filesystem to a directory in the container and the ``--rocm`` flag is used to expose the GPU to
  the container. The ``rocm_tensorflow`` folder contains a pre-built container with the necessary Python packages. We 
  can inspect the accuracy and losses in the ``results/training`` folder, e.g. copying the images to our own laptop.
  Once the network is trained, we can perform inference: 

  .. code-block:: console

    $ srun -n 1 singularity exec --rocm -B ./models:/models,./images:/images /cfs/klemming/projects/supr/bustestingshared/ENCCS/rocm_tensorflow python models/serving/main.py water_body_17.jpg

  ..
    The image and generated mask can be shown with:

    .. code-block:: console

      $ display images/water_body_17.jpg
      $ display images/generated-images/water_body_17.jpg
  
  You can open another local terminal (i.e. on your computer) and copy the images back for local visualisation:

  .. code-block:: console

    scp -r <yourusername>@dardel.pdc.kth.se:/cfs/klemming/projects/supr/bustestingshared/<yourname>/supercomputing4ai_demo/images /local/path


  
.. type-along:: Bonus - Batch mode job

  It is often easier to submit a job to the general queue rather than waiting for an interactive resource. As an example, we can book two nodes and print 
  their host name. Let's create the following submission script and call it `submit_test.sh`:

  .. code-block:: bash

    #!/bin/bash -l
    #SBATCH -J test # Job name
    #SBATCH -t 00:02:00 # Wall time
    #SBATCH -A pdc-bus-2024-8 # Allocation number
    #SBATCH -p main # Partition - in this case the normal (non-GPU) is fine
    #SBATCH --nodes 2 # We want two different nodes
    #SBATCH --ntasks-per-node=1 # We want to book only one core on each node - We need just the hostname after all :)
    #SBATCH --mail-type=ALL # Get an email when the job starts and when the job ends

    # Now for the actual instruction to be executed
    srun hostname > out.txt 2>&1 # Black magic to redirect both stdout and stderr to the same file
  
  We can now submit our short job to the queue:

  .. code-block:: console

    $ sbatch submit.sh
  
  We can check the status in queue with:

  .. code-block:: console

    $ squeue -u <username>
    
