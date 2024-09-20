Available software and modules 
================================

A variety of software, libraries and compiler toolchains is usually available on most HPC resources.
Usually a `module <https://lmod.readthedocs.io/en/latest/>`__ system is used to access software provided by
the cluster. A list of all available modules can be printed with the following syntax

.. code-block:: console

    $ module avail

The presence of a particular piece of software/library can be queried with:

.. code-block:: console

    $ ml spider <name>

This command will return all available versions of a module (if present), as well as specific instructions to load it if needed.
The module can then be loaded with ``module load <module_name(s)>``. For example, the *Julia* runtime can be loaded with:

.. code-block:: console
    
    $ ml PDC julia

.. type-along::

    We will use a Singularity container to get a Tensorflow environment. For that, we need a few modules:

    .. code-block:: console

        $ ml PDC Singularity
    
    We can also inspect the produced images directly on the cluster using the ``display`` command, available in the ImageMagick
    toolkit:

    .. code-block:: console

        $ ml ImageMagick
