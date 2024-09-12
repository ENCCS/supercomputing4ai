Available software and modules 
================================

A variety of software, libraries and compiler toolchains is usually available on most HPC resources.
Usually a `module <https://lmod.readthedocs.io/en/latest/>`__ system is used to access software provided by
the cluster. A list of all available modules can be printed with the following syntax

.. code-block:: bash

    $ module avail

The presence of a particular piece of software/library can be queried with:

.. code-block:: bash

    $ ml spider <name>

This command will return all available versions of a module (if present), as well as specific instructions to load it if needed.
The module can then be loaded with ``module load <module_name(s)>``. For example, the *Julia* runtime can be loaded with:

.. code-block:: bash
    
    $ ml PDC julia


.. type-along::

    Let's try now to load the Singularity image to use Tensorflow. Loading the necessary modules first:

    .. code-block:: bash

        $ ml PDC/23.03 singularity/4.1.1-cpeGNU-23.03

    PDC provides a number of pre-built images for common tasks, e.g. Tensorflow. Available images can be found under ``$PDC_SHUB``.

