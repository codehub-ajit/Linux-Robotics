# 2025-01-19
- Ajit G C, amk1005944@student.hamk.fi

# Task
- How to create a virtual machine to used Azure Platform for Linux Management Course.

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