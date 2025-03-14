# linux-virtualaization-7
Introduction to Virtualization Concepts
Virtualization
Virtualization is the technology that allows multiple virtual environments to run on a single physical system. This can be done through virtual machines or containers. Virtualization improves resource utilization and enables better isolation of applications.

Hypervisor
A hypervisor is software that creates and manages virtual machines on a host system. There are two types of hypervisors:

Type 1: Runs directly on the hardware.
Type 2: Runs on top of an existing OS.
Virtual Machines (VMs)
A VM is a software-based simulation of a physical computer. Each VM runs its own operating system, and VMs are isolated from one another.

Containers
Containers provide an isolated environment for running applications. Unlike VMs, containers share the host OS’s kernel but run in separate user spaces, making them lightweight.

 __Key Differences Between VMs and Containers:__

| Virtual Machines  | Containers |
|---------------------|------------|
| Includes full OS, virtual hardware | Shares host OS kernel |
| Requires more resources | Lightweight |
| Strong isolation, each VM runs separately | Process-level isolation |
|  Slightly slower due to full OS overhead | Faster startup  |
