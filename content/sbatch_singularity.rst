Queueing jobs and running a Singularity container
========================================================

Most supercomputers use a system called `SLURM <https://slurm.schedmd.com/documentation.html>`__ to manage jobs and maximise cluster utilisation. 
There are two main workflows:

* Interactive mode, in which the user asks for resources, logs into the compute nodes and runs all they need to run
* Batch mode, in which the user prepares a ``submit`` script (usually Bash) that contains all the instructions to be executed. The script is then placed in the queue and runs without any further inputs. 

Interactive resources can be requested with the ``salloc`` command in the following fashion:

.. code-block::bash

  $ salloc -n <n_cores> -t HH:MM:SS -A <allocation_number> -p <partition>

Most parameters are self-explanatory. ``-t`` is the wall time, ``-A`` is an allocation dependent on the project. ``-p`` is required by some clusters that have different types of nodes, e.g. Dardel has 
a set of nodes reserved for interactive use on a partition called ``shared`` and a set of nodes with GPUs (``gpu``). There are many other options that are explained `here <https://slurm.schedmd.com/salloc.html>`__. Once the requested resources are granted, a MPI job can be executed with ``srun -n <n_cores> my_command``; 
alternatively, the user can also ssh directly into the allocated node.

.. type-along:: 

  Let's book a node with a GPU to run our script:

  .. code-block:: bash

    $ salloc -n 1 -t 00:50:00 -A pdc-bus-2024-8 -p gpu --gpus=1

  Once we get our node, we can train our model:

  .. code-block:: bash
    
    $ srun -n 1 singularity exec --rocm -B ./models:/models /cfs/klemming/projects/supr/bustestingshared/ENCCS/rocm_tensorflow/ python models/unet/main.py
  
  The ``-B`` flag is used to bind a directory on the filesystem to a directory in the container and the ``--rocm`` flag is used to expose the GPU to
  the container. The ``rocm_tensorflow`` folder contains a pre-built container with the necessary Python packages. If the ImageMagick module was loaded, we 
  can inspect a the accuracy and losses in the ``results/training`` folder with the ``display`` command.
  Once the network is trained, we can perform inference: 

  .. code-block:: bash

    $ srun -n 1 singularity --exec --rocm -B ./models:/models,./images:/images /cfs/klemming/projects/supr/bustestingshared/ENCCS/rocm_tensorflow python models/serving/main.py -f water_body_17.jpg

  The image and generated mask can be shown with:

  .. code-block:: bash

    $ display images/water_body_17.jpg
    $ display images/generated-images/water_body_17.jpg
  
  Alternatively, you can open another local terminal (i.e. on your computer) and copy the images back for local visualisation:

  .. code-block:: console

    scp -r <yourusername>@dardel.pdc.kth.se:/cfs/klemming/projects/supr/bustestingshared/<yourname>/supercomputing4ai_demo/images /local/path
    



  

  


