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
```
sudo snap install multipass
```
Found result:

<img width="481" alt="Screenshot 2025-03-10 142516" src="https://github.com/user-attachments/assets/f77a6fe1-7d58-4cb0-a25c-6acb488e4ac1" />

Checking if its installed correctly or not by running this command:
```
ls -l /var/snap/multipass/common/multipass_socket
```
Expected result:
```
srw-rw---- 1 root sudo 0 Dec 19 09:47 /var/snap/multipass/common/multipass_socket
```
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
sudo multipass launch --name galib --cloud-init cloud-init.yml
``` 
![Screenshot 2025-03-10 155319](https://github.com/user-attachments/assets/e26bc3a4-e023-4911-a4d7-5cd8cc525753)


Accessed shell using

``` 
sudo multipass shell galib
``` 
![Screenshot 2025-03-14 172642](https://github.com/user-attachments/assets/4871e07f-6d94-4136-84fd-c9e23c9b8648)


Now checking if the user galib exist.
_command:_

``` 
cat /etc/passwd | grep galib
``` 
![Screenshot 2025-03-14 153134](https://github.com/user-attachments/assets/a8708711-7760-4022-8cd5-ba05c639588b)



Verifying welcome.txt
``` 
sudo cat /home/galib/welcome.txt
``` 
_Result:_
![Screenshot 2025-03-14 153259](https://github.com/user-attachments/assets/28050122-6899-4dea-be75-4d220e98cc53)

Using sudo because the file was created by root and was accessable by galib.
![Screenshot 2025-03-14 153652](https://github.com/user-attachments/assets/f9d7659a-b352-4115-b18a-852403d38dc5)


Then mounted the folder on the host machine using:

```
sudo multipass mount ~/host_machine galib:/home/ubuntu/shared_folder

Creating a test file in the host machine.

echo "Hello from the host!" > ~/shared-folder/hostfile.txt
```

## Part 3: Exploring LXD

### Installation
```
sudo snap install lxd
```
Result:
![Screenshot 2025-03-15 102906](https://github.com/user-attachments/assets/cee24b20-b8d6-4f0c-aeed-476ac411f3ee)

Then,,
```
sudo lxd init
```
Result:
![Screenshot 2025-03-15 105308](https://github.com/user-attachments/assets/7210c79f-df9d-4c92-ba8f-673ceec25a36)


### Basic LXD Commands
```
sudo lxc launch ubuntu:24.04 my-container
```
Result:
![Screenshot 2025-03-15 105438](https://github.com/user-attachments/assets/0ea07bc8-2d80-4a1f-8ed2-1bb5ac5e2677)

Then,

```
sudo lxc list
```
Result:
![Screenshot 2025-03-15 105532](https://github.com/user-attachments/assets/e4bc47e9-6da0-46c1-922e-e64121b78df6)

Then,

```
sudo lxc exec my-container -- bash
```
Result:
![Screenshot 2025-03-15 110640](https://github.com/user-attachments/assets/378a07df-e039-431d-99ea-3a9948c2ec7a)

Then,
```
sudo lxc stop my-container
```
Then,
```
sudo lxc delete my-container
```

## Part 4: Using Docker
### Installation:

```
sudo apt install docker.io -y
sudo systemctl enable --now docker
```

### Basic Docker Commands:
# Test Docker installation
```
sudo docker run hello-world 
```

Result:
![Screenshot 2025-03-16 105954](https://github.com/user-attachments/assets/2a75fe1d-9422-45a6-b3d4-ec97309e657a)


# Pull Ubuntu image
```
sudo docker pull ubuntu:latest
```

Result:
![Screenshot 2025-03-16 110039](https://github.com/user-attachments/assets/a3f1cb1e-a978-4c75-ba75-1d8e3b466281)

# Start Ubuntu container
```
sudo docker run -it ubuntu bash
```
Then write, exit
Result:
![Screenshot 2025-03-16 110335](https://github.com/user-attachments/assets/a417c57d-41ce-4ec9-8ee5-5bd7a86bc57c)

# List running containers

```
sudo docker ps -a
```

Result:
![Screenshot 2025-03-16 111802](https://github.com/user-attachments/assets/f4d743c4-b1df-4401-a47f-7ed17fe4cc0b)

# Stop container
```
sudo docker stop 3f4958fc3880
```

# Remove container
```
sudo docker rm 3f4958fc3880
```

### Dockerfile Experiment:
Created a simple `Dockerfile`:

Command:
```
nano Dockerfile
```

The file is:
![Screenshot 2025-03-16 113251](https://github.com/user-attachments/assets/c48dbe30-2af6-49ed-8751-fe5fb21d85e1)

# Build the Docker Image
```
sudo docker build -t my-nginx .
````

# Run the Container
```
sudo docker run -d -p 8080:80 my-nginx
````
Result:
![Screenshot 2025-03-16 113618](https://github.com/user-attachments/assets/2da63b55-d381-4637-80ab-0788baac94dc)


## Part 5: Snaps for Self-Contained Applications
### Research on Snapcraft:
Snapcraft packages applications with their dependencies for seamless execution across Linux distros.
### Creating a Snap Package:
Installed Snapcraft:
```
sudo snap install snapcraft --classic
```

Result:
![Screenshot 2025-03-16 121654](https://github.com/user-attachments/assets/31f9f61c-ca8f-4828-91ac-c63b934ffcb5)
































