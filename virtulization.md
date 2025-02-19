# Assignment 7
**Date:** 2025-02-19
**Author:** Ajit G C (amk1005944@student.hamk.fi) 


# Linux Virtualization Assignment

## Part 1: Virtualization Concepts
### Summary

#### Virtualization
- The process of creating a virtual version of something, such as hardware, storage, or network resources.

#### Hypervisor
- Software that creates and manages virtual machines (VMs). Examples include KVM, VMware, and Hyper-V.

#### Virtual Machines (VMs)
- Emulations of physical computers that run their own operating systems.

#### Containers
- Lightweight, isolated environments that share the host OS kernel but have their own file systems and libraries.

### **VMs vs Containers**
- The difference between VMs and Containers in terms of Architecture, Resource Utilization and Isolation
| VMs | Containers | 
| ---| --- | 
| It require a full OS for each instance | It share the host OS kernel|
| It require more resources | It is more Lightweight and efficient|
| It provide strong isolation since each VM has its own OS| It provide a lower level of isolation, it share the host OS kernel|
 

## Part 2: Multipass
### Installation
```bash
sudo snap install multipass
```
- Screenshot of Multipass installation.
![Install multipass](image/install%20multipass.png)

- I practice the basic command 
1. Launch a default Ubuntu instance
```bash
multipass launch --name ajit-vm
```
- Screenshot of launching a default Ubuntu instance.
![Launch a default Ubuntu instance](image/multipass%20lunch.png)
2. List all running instances
```bash 
multipass list
```
- Screenshot of listing running instances.
![List all running instances](image/multipass%20list.png)

3. View details about an instance 
```bash
multipass info ajit-vm
```
- Screenshot of viewing details about an instance.
![View details about an instance](image/Multipass-info.png)
4. Access the shell of a running instance
```bash
multipass shell ajit-vm
```
- Screenshot of accessing the shell of a running instance.
![Access the shell of a running instance](image/multipas%20shell.png)

5. Stop, delete and purge an instance
```bash
multipass stop ajit-vm
multipass delete ajit-vm
multipass purge
```
- Screenshot of stopping, deleting and purging an instance.
![Stop, delete and purge an instance](image/stop:delete:purge.png)

### Learn About Cloud-Init

1. Create a cloud-init.yaml file to customize an instance.
```bash
nano cloud-init.yaml
```
- Screenshot of creating a cloud-init.yaml file.
![Create a cloud-init.yaml file](image/nano%20cloud-init.png)
2. Launch an instance with cloud-init
```bash
multipass launch --name ajit-vm --cloud-init cloud-init.yaml
```
- Screenshot of launching an instance with cloud-init.
![Launch an instance with cloud-init](image/cloud%20lunch.png)

3.  Create a new folder and Mount the folder inside a VM:
```bash
mkdir ~/multipass_shared
multipass mount ~/multipass_shared ajit-vm:/mnt/shared
```
- Screenshot of mounting a folder inside a VM.
![Mount a folder inside a VM](image/mkdir%20and%20mount.png)

- I create a txt file inside multipass folder to share it in VM because without creating a file I can't mount the folder.
```bash 
echo "Hello, World!" > ~/multipass_shared/testfile.txt
```
- Screenshot of creating a txt file inside multipass folder.
![Create a txt file inside multipass folder](image/making%20txt%20file.png)

4. Check the mounted folder inside the VM:
```bash
multipass shell ajit-vm
ls /mnt/shared
```
- Screenshot of mounting a folder inside a VM.
![Mount a folder inside a VM](image/inside%20vm.png)




## Part 3: LXD

### Installation
```bash
sudo apt update
sudo apt install lxd
```
- Screenshot of installing LXD.
![Install LXD](image/lxd%20install.png)


### Basic LXD command

1. Create a new container ans list it
```bash
lxc launch ubuntu:24.04 ajit-container
lxc list
```
- Screenshot of creating a new container and listing it.
![Create a new container and list it](image/lxc%20lunch%20.png)
2. Start and stop the container
```bash
lxc start ajit-container
lxc stop ajit-container
```
- Screenshot of starting and stopping the container.
![Start and stop the container](image/stop.png)

3. Delete the container
```bash
lxc delete ajit-container
```
- Screenshot of deleting a container
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
- Screenshot of version
![Docker version](image/docker%20version.png)

### Making directory and create nano file 
```bash
mkdir myapp
cd myapp
echo "hello world" > index.html
```
- Screenshot of creating a directory and file
![Create a directory and file](image/mkdir.png)

### Build Docker
```bash
docker build -t ajit-gc .
```
- Screenshot of building a Docker image
![Build a Docker image](image/docker%20build.png)

### Run Docker
```bash
docker ps
docker run -p 8080:80 ajit-gc
```
- Screenshot of running a Docker container
![Run a Docker container](image/docker%20ps.png)

### Install docker on Desktop to familirize with Docker

- I installed Docker Desktop on my laptop and sign with my Github account to access the Docker Hub.
![image of Docker Desktop](image/docor%20accout%20set-up.png)

![image inside docker](image/docker%20search.png)

![image of Docker Desktop](image/docker%20congo.png)


## Part 5: Snaps for Self-Contained Applications
1. What are snaps?
- Snaps are containerized software packages that include all the dependencies required to run an application. They are designed to work across different Linux distributions.
2. What is Snapcraft?
- Snapcraft is the command-line tool used to create and publish Snaps.

### Install Snapcraft
```bash
sudo snap install snapcraft --classic
```
### Verify Snapcraft installation

    snapcraft --version

![Version](image/snapcraft%20version.png)

### Create a directory for Snap project
    mkdir hello-snap
    cd hello-snap
- Create a simple Python script named hello.py
    echo 'print("Hello, Snap!")' > hello.py

###  Create a Snapcraft Configuration File
- Initialize snapcraft
```bash
snapcraft init
```
- Edit the snapcraft.yaml file
```bash
nano snapcraft.yaml
```

![image inside nano](image/nano%20.png)

### Build the Snap
    snapcraft

### Install the Snap
    sudo snap install hello-snap_1.0_amd64.snap --dangerous
### Run the Snap   
    hello-snap.hello