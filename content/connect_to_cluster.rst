Connecting to a HPC resource
==============================


Once SSH keys are created and uploaded on the PDC interface, entering the cluster is as simple as:

.. code-block::bash 

    ssh -Y <username>@dardel.pdc.kth.se


Which should get you into the PDC supercomputer. The ``-Y`` flag is used to be able to open graphical windows on the supercomputer, e.g.
to visualise images. This will work only if you have a running local X server (if you are on Linux/WSL, you most likely do).

.. type-along::

    We can get a sense of the size of Dardel by using the ``sinfo`` command:

    .. code-block:: console

        fiusco@login1:~> sinfo -s
        PARTITION AVAIL  TIMELIMIT   NODES(A/I/O/T) NODELIST
        gpu          up 1-00:00:00        49/9/4/62 nid[002792-002853]
        main         up 1-00:00:00  604/256/112/972 nid[001012-001531,001756-001816,001818-001819,001821-001896,001898-002007,002009-002023,002552-002567,002588-002759]
        scania       up 4-00:00:00    22/187/15/224 nid[001532-001755]
        scania-hf    up 4-00:00:00          0/3/1/4 nid[000011-000014]
        memory       up 7-00:00:00        34/8/0/42 nid[000101-000118,001772-001779,002552-002567]
        shared       up 7-00:00:00        27/5/0/32 nid[001000-001011,002568-002587]
        long         up 7-00:00:00        76/4/0/80 nid[001800-001819,002588-002647]
        eggnog       up 7-00:00:00          4/0/0/4 nid[002536-002539]
        supernova    up 14-00:00:0         5/6/5/16 nid[001817,001820,001897,002008,002540-002551]

    E.g. the ``main`` partition has 972 nodes, each containing 128 cores.

    A general sense of the amount of work load can be gained with the ``squeue`` command, which shows all the jobs (running, queued):

    .. code-block:: console

        fiusco@login1:~> squeue