Queueing jobs and running a Singularity container
========================================================

Most supercomputers use a system called `SLURM <https://slurm.schedmd.com/documentation.html>`__ to manage jobs and maximise cluster utilisation. 
There are two main workflows:

* Interactive mode, in which the user asks for resources, logs into the compute nodes and runs all they need to run
* Batch mode, in which the user prepares a ``submit`` script (usually Bash) that contains all the instructions to be executed. The script is then placed in the queue and runs without any further inputs. 

Interactive resources can be requested with the ``salloc`` command in the following fashion:

.. code-block::bash

  $: salloc -n <n_cores> -t HH:MM:SS -A <allocation_number> -p <partition>

Most parameters are self-explanatory. ``-t`` is the wall time, ``-A`` is an allocation dependent on the project. ``-p`` is required by some clusters that have different types of nodes, e.g. Dardel has 
a set of nodes reserved for interactive use on a partition called ``shared``. There are many other options that are explained `here <https://slurm.schedmd.com/salloc.html>`__. Once the requested resources are granted, a MPI job can be executed with ``srun -n <n_cores> my_command``; 
alternatively, the user can also ssh directly into the allocated node.

