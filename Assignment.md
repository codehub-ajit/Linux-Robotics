# 2025-01-19
- Ajit G C, amk1005944@student.hamk.fi

# Task
How to create a virtual machine to used Azure Platform for Linux Management Course.

- Step 1: At first, I create a Azure account from portal.azure.com for myself using my university email. 
- Step 2: For getting more credit in Azure, I used my university email to get free Azure credits.

![Azure View after login ](image/available%20credit.png)

- Step 3: I created a new resource group in Azure portal.
- Step 4: I created a new virtual machine in Azure portal. ( It may take some time to load)
- Step 5: I selected North Europe as a Region and Ubuntu Server 24.04 LTS - x64 Gen2 as the operating system. 
- Step 6: I selected the virtual machine size as Standard_B2ls_v2- 2 vCPUs, 4 GiB Memory ($33.29/month).
- Step 7: I selected the network configuration as Public IP address and Network interface and created a new Username.
- Step 8: I seleceted OS disk type as Standard SSD and Storage type as Locally-redundant storage.
- Step 9: I selected the public IP address as Static and created a new public IP address as lab-robotics-ip.
- Step 10: I selected inbound ports as (Http(80), HTTPS(443), SSH(22))
- Step 11: I selected the Enable auto-shutdown and set the auto-shutdown time as 10:00 PM and Select the time Zone as (UTC + 2:00) Helsinki
- Step 12: I reviewed the settings and created the virtual machine.

After creating the virtual machine, I go to lab-robotics-ip and select setting(Configuration) than type ajit-world as DNS name lable and save it.

- Step 13: After that, I select lab-robotics and select connect and select Native SSH and copy the path that I downloaded the key.pam file.
![Click on Native_SSH](image/Native_ssh.jpg)
![Copy the URL](image/path_copy.jpg)

- Step 14: I open the terminal and paste the URL given in SSH to VM with specified private key.
![Successfully done in Termina ](image/terminal.jpg)






# 2025-01-31
- Ajit G C, amk1005944@student.hamk.fi

# Assignment 3

# Task 
- User Management and File System access in Linux

1. Creating Users
- I created a new user named tupu using the command `sudo adduser tupu`
- This will Create a new user tupu Automatically create the home directory /home/tupu. Set the default shell to /bin/bash and Prompt for password creation and additional user details.

- Tupu (Using) To create the user lupu, use the following command:

    `sudo useradd -m -d /home/lupu -s /bin/bash -G supu supu`
This will:
. Create the user supu
. Set the home directory to /home/supu
. Assign the default shell /bin/bash
. Add supu to the supu group
- Set a password for supu using the following command:
`sudo passwd supu`

2. Granting Sudo Privilege Method 1: Using (Recommended) Edit the sudoers file safely:

- I used the command `sudo visudo` to edit the sudoers file safely.
- I added the following line to the end of the file:
`tupu ALL=(ALL:ALL) ALL`
`lupu ALL=(ALL:ALL) ALL `

- Save and exit.

- Method 2: Adding Users to the Group Alternatively, run:
`sudo usermod -aG sudo supu`
`sudo usermod -aG sudo tupu`

- Verify with:
    `groups supu`
   ` groups tupu`

3. Setting Up Shared directory 
- Step 1: Create the directory

- I used the command `sudo mkdir /opt/projekti` to create a new directory /home/shared
- Step 2: Assign a Group
`sudo usermod -aG projekti supu` 
`sudo usermod -aG projekti tupu` 

- Step 3: Change the ownership of the directory

- I used the command ` sudo chown :projekti /opt/projekti`
- Step 4: Set Permissions
`sudo chmod 770 /opt/projekti`

- Output: 
The output of the `ls -ld /opt/projekti` command should look like this:
`drwxrws--- 2 root projekti 4096 Jan 30 21:53 /opt/projekti `


# Screenshot of the project
![SS](image/1.png)
![SS](image/2.png)
![SS](image/3.png)
![SS](image/4.png)
