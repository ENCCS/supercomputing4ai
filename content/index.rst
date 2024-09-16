Introduction to supercomputing for AI
=====================================

High performance computing (HPC) resources can be used to accelerate AI workflows. The EuroHPC Joint Undertaking (JU) offers
free access to such resources to SMEs as well as larger companies. In this hands-on, you will learn:

* What is an HPC resource and how it is different from a cloud environment;
* What are the available HPC resources through the EuroHPC JU;
* How to connect to a cluster and explore resources;
* How to run a demo AI workflow based on Singularity.



.. prereq::

   You will need to have credentials to access the `PDC <https://pdc.kth.se/>`__ cluster. A working SSH client is needed: 
   it is included on macOS and most Linux flavours; it is also available on Windows in the Powershell or under the `Windows Subsystem for Linux (WSL) <https://learn.microsoft.com/en-us/windows/wsl/install>`__.



.. csv-table::
   :widths: auto
   :delim: ;

   20 min ; :doc:`supercomputer_why`
   20 min ; :doc:`connect_to_cluster`
   20 min ; :doc:`folders_and_transfer`
   20 min ; :doc:`software_modules`
   20 min ; :doc:`sbatch_singularity`


.. toctree::
   :maxdepth: 1
   :caption: The lesson

   supercomputer_why
   connect_to_cluster
   folders_and_transfer
   software_modules
   sbatch_singularity



.. toctree::
   :maxdepth: 1
   :caption: Reference

   quick-reference

   guide



Who is the course for?
----------------------

This course is intended for data scientists that want to take advantage of higher computing power to perform their workflows.
Some degree of familiarity with a command-line shell is recommended, but no expertise is required. No previous knowledge of 
supercomputing environments is required.




About the course
----------------

We will train a Unet model to be able to recognise water in satellite pictures. The source code can be found at ``this <https://github.com/ENCCS/supercomputing4ai_demo.git>``__
repo. 

::

  ../supercomputing4ai_demo
  ├── build_singularity.def
  ├── images
  │   └── generated-images
  ├── models
  │   ├── serving
  │   │   └── main.py
  │   └── unet
  │       ├── data
  │       │   └── water
  │       │       ├── Images
  │       │       └── Masks
  │       ├── main.py
  │       └── result
  │           ├── models
  │           └── training
  └── README.md


See also
--------

Further introductory material can be found on the `Introduction to LUMI <https://lumi-supercomputer.github.io/lumi-self-learning/>`__ and 
`HPC carpentry <https://carpentries-incubator.github.io/hpc-intro/>`__ pages. 



Credits
-------

The lesson file structure and browsing layout is inspired by and derived from
`work <https://github.com/coderefinery/sphinx-lesson>`__ by `CodeRefinery
<https://coderefinery.org/>`__ licensed under the `MIT license
<http://opensource.org/licenses/mit-license.html>`__. We have copied and adapted
most of their license text.

Instructional Material
^^^^^^^^^^^^^^^^^^^^^^

This instructional material is made available under the
`Creative Commons Attribution license (CC-BY-4.0) <https://creativecommons.org/licenses/by/4.0/>`__.
The following is a human-readable summary of (and not a substitute for) the
`full legal text of the CC-BY-4.0 license
<https://creativecommons.org/licenses/by/4.0/legalcode>`__.
You are free to:

- **share** - copy and redistribute the material in any medium or format
- **adapt** - remix, transform, and build upon the material for any purpose,
  even commercially.

The licensor cannot revoke these freedoms as long as you follow these license terms:

- **Attribution** - You must give appropriate credit (mentioning that your work
  is derived from work that is Copyright (c) ENCCS and individual contributors and, where practical, linking
  to `<https://enccs.github.io/sphinx-lesson-template>`_), provide a `link to the license
  <https://creativecommons.org/licenses/by/4.0/>`__, and indicate if changes were
  made. You may do so in any reasonable manner, but not in any way that suggests
  the licensor endorses you or your use.
- **No additional restrictions** - You may not apply legal terms or
  technological measures that legally restrict others from doing anything the
  license permits.

With the understanding that:

- You do not have to comply with the license for elements of the material in
  the public domain or where your use is permitted by an applicable exception
  or limitation.
- No warranties are given. The license may not give you all of the permissions
  necessary for your intended use. For example, other rights such as
  publicity, privacy, or moral rights may limit how you use the material.


Software
^^^^^^^^

Except where otherwise noted, the example programs and other software provided
with this repository are made available under the `OSI <http://opensource.org/>`__-approved
`MIT license <https://opensource.org/licenses/mit-license.html>`__.
