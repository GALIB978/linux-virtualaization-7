# linux-virtualaization
#### Part 1: Introduction to Virtualization Concepts

### Hypervisor
A hypervisor is software that creates and manages virtual machines. There are two types of hypervisors:
- *Type 1*: Runs directly on the hardware (bare-metal hypervisor).
- *Type 2*: Runs on top of an existing operating system (hosted hypervisor).

### Virtual Machines (VMs)
A *Virtual Machine (VM)* is a virtualized environment that runs its own operating system. VMs are isolated from each other and from the host system, offering high-level isolation but consuming more resources.

### Containers
*Containers* are lightweight virtualized environments that share the host operating system’s kernel but run applications in isolated user spaces. Containers are faster to start and more resource-efficient compared to VMs.

__Key Differences Between VMs and Containers:__

| Virtual Machines  | Containers |
|---------------------|------------|
| Includes full OS, virtual hardware | Shares host OS kernel |
| Requires more resources | Lightweight |
| Strong isolation, each VM runs separately | Process-level isolation |
|  Slightly slower due to full OS overhead | Faster startup  |


#### Part 2: Working with Multipass:
Following the Source Guide
_Source Used:_ [Canonical Install Guide](https://canonical.com/multipass/docs/install-multipass)

_Steps:_

To install multipass:
sudo snap install multipass

Found result:

<img width="481" alt="Screenshot 2025-03-10 142516" src="https://github.com/user-attachments/assets/f77a6fe1-7d58-4cb0-a25c-6acb488e4ac1" />

## Basic commands

 List Running Instances
 Command
``` 
sudo multipass launch
``` 

result:
![Screenshot 2025-03-10 142607](https://github.com/user-attachments/assets/50159d9b-6cac-4070-8456-2c3d6a9715d5)

__List Running Instances__
 Command: 
``` 
sudo multipass list
``` 
Result:
![Screenshot 2025-03-10 142920](https://github.com/user-attachments/assets/fad4764e-5c0c-4228-b508-16f69a485e6d)

__Multipass instance info:__
Command:
``` 
sudo multipass info teeming-imp
``` 
Result:
![Screenshot 2025-03-10 145110](https://github.com/user-attachments/assets/a23c9287-536b-4f00-83e4-55e2ac9b9e45)

_Multipass Shell access:_
Command:
``` 
sudo multipass shell teeming-imp
``` 
I created a file in the instance home directory and named it 'hello_world.txt'.
Now trying to read the file outside the instance using the cat command.

Command:
``` 
sudo multipass exec teeming-imp -- cat hello_world.txt
``` 
Result:
![Screenshot 2025-03-10 145929](https://github.com/user-attachments/assets/87ab376b-9d90-4a00-adf2-2d8aa93da1a3)


_Stop a Running Instance_

Command
``` 
sudo multipass stop teeming-imp
``` 

_Deleting Instance_
``` 
sudo multipass delete teeming-imp
sudo multipass list
``` 
Result:
![Screenshot 2025-03-10 151321](https://github.com/user-attachments/assets/788dbee7-47d6-4182-ab1b-7b649c7bb751)


_Cloud-init Experiment:_

created the *"cloud-init.yml"* file.
![Screenshot 2025-03-10 153813](https://github.com/user-attachments/assets/839e8c86-2514-4619-bbd5-d434f7fa753b)

The config file will install some basic packeges and after successfully starting the instance it will return "Cloud-init is working!" from the welcome.txt file which will create after running the first time.

_Commnad:_

``` 
sudo multipass launch --name galib cloud-init --cloud-init cloud-init.yml
``` 
![Screenshot 2025-03-10 155319](https://github.com/user-attachments/assets/e26bc3a4-e023-4911-a4d7-5cd8cc525753)


Accessed shell using

``` 
sudo multipass shell galib
``` 
![Screenshot 2025-03-14 172642](https://github.com/user-attachments/assets/4871e07f-6d94-4136-84fd-c9e23c9b8648)


Now checking if the user rafsan_cloud exist.
_command:_

``` 
cat /etc/passwd | grep rafsan_cloud
``` 
![Screenshot 2025-03-14 153134](https://github.com/user-attachments/assets/a8708711-7760-4022-8cd5-ba05c639588b)



Verifying welcome.txt
``` 
sudo cat /home/rafsan_cloud/welcome.txt
``` 
_Result:_
![Screenshot 2025-03-14 153259](https://github.com/user-attachments/assets/28050122-6899-4dea-be75-4d220e98cc53)

Using sudo because the file was created by root and was accessable by rafsan_cloud.
![Screenshot 2025-03-14 153652](https://github.com/user-attachments/assets/f9d7659a-b352-4115-b18a-852403d38dc5)


Then mounted the folder on the host machine using:

```
sudo multipass mount ~/host_machine cloud-init:/home/ubuntu/shared_folder

Creating a test file in the host machine.

echo "Hello from the host!" > ~/shared-folder/hostfile.txt
```
















