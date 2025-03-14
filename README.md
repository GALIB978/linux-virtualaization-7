# linux-virtualaization
#### Part 1: Introduction to Virtualization Concepts

1. __Virtualization:__ Virtualization is the process of creating virtual instances of computer resources, such as operating systems, storage, and networks, allowing multiple environments to run on a single physical system.

2. __Hypervisor:__ A hypervisor is a software layer that enables virtualization by allowing multiple virtual machines (VMs) to share the same physical hardware.

3. __Virtual Machines (VMs):__ VMs are software-based emulations of a physical computer, running an OS and applications as if they were on a dedicated machine.

4. __Containers:__ Containers are lightweight, portable environments that package an application along with its dependencies, ensuring consistency across different environments.
ization-7

 __Key Differences Between VMs and Containers:__

| Virtual Machines  | Containers |
|---------------------|------------|
| Includes full OS, virtual hardware | Shares host OS kernel |
| Requires more resources | Lightweight |
| Strong isolation, each VM runs separately | Process-level isolation |
|  Slightly slower due to full OS overhead | Faster startup  |


#### Part 2: Working with Multipass:
Following the Source Guide
__Source Used:__ [Canonical Install Guide](https://canonical.com/multipass/docs/install-multipass)

__Steps:__

To install multipass:

```
snap install multipass
```
Checking if its installed correctly or not by running this command:
```
ls -l /var/snap/multipass/common/multipass_socket
```
Found result:
<img width="481" alt="Screenshot 2025-03-10 142516" src="https://github.com/user-attachments/assets/f77a6fe1-7d58-4cb0-a25c-6acb488e4ac1" />



