What is a supercomputer and how is it different from cloud?
=============================================================

A supercomputer (or *cluster*) is a high-performance computing infrastructure. The general idea is to have many (thousands) of machines, called *nodes*, working in parallel
to increase performance. Each node can have one or several (usually two) multi-core CPUs, local RAM, and possibly accelerators such as GPUs. What distinguishes a cluster
from a simple collection of computers is the high-speed connection between all the nodes, called *interconnect*. The speed and density of connections between nodes makes it 
possible for the nodes to seamlessly communicate and solve a problem in parallel. The general architecture of a cluster looks like below:

.. figure:: img/cluster_diagram.png

    Schematics of a typical cluster.


The user accesses the cluster through the *login nodes*, which act as a gateway between the external world and the compute parts. They should not be used to run calculations. 
Usually a parallel file system is provided (such as `Lustre <https://www.lustre.org/>`__), with independent servers (not shown in the figure) that manage distributed access 
from all the nodes. Moreover, each node usually has some temporary storage called *scratch* for fast access during computation. 
On Dardel specifically, each CPU node has two AMD EPYC CPUs with 64 physical cores each and RAM ranging from 256 GB to 2 TB. Each GPU node has one AMD EPYC and 4 AMD Instinct
MI250X GPUs, each containing two GCDs (compute chips in AMD lingo); thus, each node has 8 GPUs. 

How is HPC different from cloud?
----------------------------------

While they both provide access to high-performance computational resources, a few important differences exist between cloud and HPC systems:

* An HPC resource is shared among several users; usually users do not have root access, unlike cloud where each user has their own sandboxed environment;
* Each workload pushed by a user (called *job*) contends for the available resources; usually, a queueing system is managed by a *job manager* (more on that later) which decides 
  which jobs are going to run to maximise cluster usage. This means that a job may have to wait for resources before it is allowed to run.
* (Through EuroHPC) the cost of HPC does not scale with amount of resources used; with cloud it does.
* Engineering/scientific applications usually expect an HPC-like environment which is harder to set up in the cloud;
* Access to bare metal vs virtual machines.