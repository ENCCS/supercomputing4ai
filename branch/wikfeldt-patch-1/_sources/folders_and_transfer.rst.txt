Move between folders, ls, transferring to/from local storage
===============================================================

Upon logging in, you should be in your "home" folder, as reported by the prompt:

.. code:: console 

   fiusco@login1:~>

where ``login1`` is the name of the host (in this case, the login node) and ``~`` represents
the home folder. The full path of this directory can be printed using the ``pwd`` command
(**p**\ rint **w**\ orking **d**\ irectory):

.. code:: console 

    $ pwd
    /cfs/klemming/home/f/fiusco


The contents of a directory can be listed with the ``ls`` command:

.. code-block:: console 

    $ ls
    Private  Public  spack-user


The ``cd`` (**c**\ hange **d**\ irectory) command can be used to navigate the filesystem. 
 
Moving files/folders from/to the cluster can be achieved via the ``scp`` command to be run locally
(i.e. not on the cluster):

.. code-block:: console
    
    $ scp [-r] user@dardel.pdc.kth.se:/path/to/source /path/to/local/destination

The optional ``-r`` flag is used to indicate recursive copying of whole folders and their contents.

.. type-along::

    In this workshop, our working folder will be in ``/cfs/klemming/projects/supr/testingsharedbus/``. You can create your own folder:

    .. code-block:: console 

        $ cd /cfs/klemming/projects/supr/bustestingshared
        $ mkdir my_name
    
    We can now clone the repository containing the material for the workshop:

    .. code-block:: console

        $ cd my_name
        $ git clone https://github.com/ENCCS/supercomputing4ai_demo
        $ cd supercomputing4ai_demo
