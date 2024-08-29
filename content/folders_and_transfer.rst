Move between folders, ls, transferring to/from local storage
===============================================================

Upon logging in, you should be in your "home" folder, as reported by the prompt:

.. code:: console 

   fiusco@login1:~>

where ``login1`` is the name of the host (in this case, the login node) and ``~`` represents
the home folder. The full path of this directory can be printed using the ``pwd`` command
(**p**\ rint **w**\ orking **d**\ irectory):

.. code:: console 

    fiusco@login1:~>pwd
    /cfs/klemming/home/f/fiusco


The contents of a directory can be listed with the ``ls`` command:

.. code-block:: console 

    fiusco@login1:~>ls
    Private  Public  spack-user


The ``cd`` (**c**\ hange **d**\ irectory) command can be used to navigate the filesystem. 
 
Moving files/folders from/to the cluster can be achieved via the ``scp`` command to be run locally
(i.e. not on the cluster):

.. code-block:: console
    
    scp [-r] user@dardel.pdc.kth.se:/path/to/source /path/to/local/destination

The optional ``-r`` flag is used to indicate recursive copying of whole folders and their contents.