Connecting to a HPC resource
==============================


Once SSH keys are created and uploaded on the PDC interface, entering the cluster is as simple as:

.. code-block::bash 

    ssh -Y <username>@dardel.pdc.kth.se


Which should get you into the PDC supercomputer. The ``-Y`` flag is used to be able to open graphical windows on the supercomputer, e.g.
to visualise images.