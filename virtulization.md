# Assignment 7: # Linux Virtualization 
**Date:** 2025-02-19
**Author:** Ajit G C (amk1005944@student.hamk.fi) 

## Part 1: Virtualization Concepts

Virtualization

The process of creating a virtual version of something, such as hardware, storage, or network resources.

Hypervisor

Software that creates and manages virtual machines (VMs). Examples include KVM, VMware, and Hyper-V.

Virtual Machines (VMs)

Emulations of physical computers that run their own operating systems.

Containers

Lightweight, isolated environments that share the host OS kernel but have their own file systems and libraries.

### **VMs vs Containers**

- The difference between VMs and Containers in terms of Architecture, Resource Utilization and Isolation

| **Aspect**    | **VMs**                                          | **Containers**    |
|----------------------|------------------------------------------------|------------------------------|
| **Architecture**     | Requires a full OS for each instance            | Shares the host OS kernel      |
| **Resource Utilization** | Requires more resources                        | More lightweight and efficient   |
| **Isolation**        | Provides strong isolation since each VM has its own OS | Provides a lower level of isolation, as it shares the host OS kernel |

 

## Part 2: Multipass Implementation

### Installation

```bash
sudo snap install multipass
```

Screenshot of Multipass installation.

![Install multipass](image/install%20multipass.png)


1. Launch a default Ubuntu instance

```bash
multipass launch --name ajit-vm
```

![Launch a default Ubuntu instance](image/multipass%20lunch.png)

2. List all running instances

```bash 
multipass list
```

![List all running instances](image/multipass%20list.png)

3. View details about an instance 

```bash
multipass info ajit-vm
```

![View details about an instance](image/Multipass-info.png)

4. Access the shell of a running instance

```bash
multipass shell ajit-vm
```

![Access the shell of a running instance](image/multipas%20shell.png)

5. Stop, delete and purge an instance

```bash
multipass stop ajit-vm
multipass delete ajit-vm
multipass purge
```

![Stop, delete and purge an instance](image/stop:delete:purge.png)

### Learn About Cloud-Init Configuration

Create a cloud-init.yaml file to customize an instance.

```bash
nano cloud-init.yaml
```

![Create a cloud-init.yaml file](image/nano%20cloud-init.png)

Launch an instance with cloud-init

```bash
multipass launch --name ajit-vm --cloud-init cloud-init.yaml
```

![Launch an instance with cloud-init](image/cloud%20lunch.png)

3.  Create a new folder and Mount the folder inside a VM:

```bash
mkdir ~/multipass_shared
multipass mount ~/multipass_shared ajit-vm:/mnt/shared
```

![Mount a folder inside a VM](image/mkdir%20and%20mount.png)

I create a txt file inside multipass folder to share it in VM because without creating a file I can't mount the folder.

```bash 
echo "Hello, World!" > ~/multipass_shared/testfile.txt
```

![Create a txt file inside multipass folder](image/making%20txt%20file.png)

Check the mounted folder inside the VM:

```bash
multipass shell ajit-vm
ls /mnt/shared
```

![Mount a folder inside a VM](image/inside%20vm.png)


## Part 3: LXD Implementation

### Installation

```bash
sudo apt update
sudo apt install lxd
```


![Install LXD](image/lxd%20install.png)


### Basic LXD command

1. Create a new container ans list it

```bash
lxc launch ubuntu:24.04 ajit-container
lxc list
```

![Create a new container and list it](image/lxc%20lunch%20.png)

2. Start and stop the container

```bash
lxc start ajit-container
lxc stop ajit-container
```

![Start and stop the container](image/stop.png)

3. Delete the container

```bash
lxc delete ajit-container
```

![Delete a container](image/lxc%20delete.png)


## Part 4: Docker

### Installation

```bash
sudo apt update
sudo apt install docker.io
```

### Verify the installation

```bash
docker --version
```

![Docker version](image/docker%20version.png)

### Making directory and create nano file 

```bash
mkdir myapp
cd myapp
echo "hello world" > index.html
```

![Create a directory and file](image/mkdir.png)

### Build Docker

```bash
docker build -t ajit-gc .
```

![Build a Docker image](image/docker%20build.png)

### Run Docker

```bash
docker ps
docker run -p 8080:80 ajit-gc
```

![Run a Docker container](image/docker%20ps.png)



### Install docker on Desktop to familirize with Docker

I installed Docker Desktop on my laptop and sign with my Github account to access the Docker Hub.

![image of Docker Desktop](image/docor%20accout%20set-up.png)


![image inside docker](image/docker%20search.png)


![image of Docker Desktop](image/docker%20congo.png)


## Part 5: Snaps for Self-Contained Applications

1. What are snaps?
Snaps are containerized software packages that include all the dependencies required to run an application. They are designed to work across different Linux distributions.


2. What is Snapcraft?
Snapcraft is the command-line tool used to create and publish Snaps.

### Install Snapcraft

First, install snapcraft if you haven't already:

```bash
sudo apt update
sudo apt install snapcraft -y
```

For non-Ubuntu system, you need to install snapcraft via snap

```bash
sudo snap install snapcraft --classic
```

### Verify Snapcraft installation

```bash
snapcraft --version
```

![Version](image/snapcraft%20version.png)

### Create a directory for Snap project

```bash
    mkdir my-snapcraft
    cd my-snapcraft
```

### Create a simple Application Script

We'll make a simple bash script that prints "Hello, Snap!".

```bash
mkdir bin
nano bin/hello-snap
```

Add the following code to the file:

```bash
#!/bin/bash
echo "Hello, Snap!"
```

###  Create a Snapcraft Configuration File

Initialize snapcraft

```bash
snapcraft init
```

Edit the snapcraft.yaml file

```bash
nano snapcraft.yaml
```

Add the following content to the file:

```bash
name: my-snapcraft
base: core22
version: "1.0"
summary: "A simple Snapcraft app"
description: "This is a simple Snap application that prints Hello, Snap!"

grade: stable
confinement: strict

apps:
  hello:
    command: bin/hello-snap

parts:
  hello:
    plugin: dump
    source: .
```

![image inside nano](image/nano%20.png)

### Build the Snap

<<<<<<< HEAD
```bash
snapcraft
```

### Install the Snap:

```bash
sudo snap install my-snapcraft_1.0_amd64.snap --dangerous
```

The --dangerous flag is needed because it's not for the offical Snap store.

Run the Snap: 

```bash
my-snapcraft.hello
```

Output
![Hello snap](image/output.png)
=======
### Install the Snap
    sudo snap install hello-snap_1.0_amd64.snap --dangerous
### Run the Snap   
    hello-snap.hello
>>>>>>> 59dd49273b378e98b086359a50438dc96c3f76ef
