<img width="512" height="247" alt="Active Directory logo" src="https://github.com/user-attachments/assets/6e5e4be4-bd02-49cf-a646-a7f6bf3490bd" />


# Preparing-Active-Directory-Infrastructure-in-Azure

This tutorial demonstrates how to set up an Active Directory Infrastructure in Azure.  The objective is to create a Domain Controller and a Client Machine within the same virtual network.
Environments and Technologies Used
Operating System (Local Machine): macOS on a 2018 MacBook Pro


Cloud Platform: Microsoft Azure Portal (accessed via web browser)
Virtual Network (VNet) and Subnet within Azure


Private IP addressing and custom DNS configuration


Remote Access Tool: Microsoft Remote Desktop for macOS


Authentication: Local admin credentials (Peladn229 / Innocn2009!!)


Optional Services:


Active Directory Domain Services (AD DS) for domain setup


Azure Resource Group for resource organization

Operating Systems Used
Compute Resources:


DC-1: Windows Server 2022 Datacenter (Domain Controller)


Client-1: Windows 10 Pro (Client workstation)


Deploying an Active Directory Domain Controller in Microsoft Azure
Create a Resource Group
Create a Virtual Machine and subnet
Create the Domain Controller VM (Windows Server 2022) named DC-1, add you Username and password
After completing the creation of the VM, you must set the Domain controller’s NIC Private IP Address to be Static.
Now log in the VM and disable the Windows Firewall, Imperative for testing purposes.

<img width="512" height="320" alt="Resource manager" src="https://github.com/user-attachments/assets/27c17141-7407-4c45-876e-009bda2e40fc" />

Within Azure Portal locate the Resource groups section. Click Create.
Subscription then  picks  the plan that’s currently active.
Resource group name Active Directory Lab.

<img width="512" height="320" alt="Create a resource Group" src="https://github.com/user-attachments/assets/f5cccc59-2bcf-42b9-8e9c-fc1f883c6976" />

On this page you will now Select your subscription model, and type in the name of your Resource group. Make sure to select the Region, It's imperative that all regions match to have a seamless connection.

<img width="512" height="320" alt="Create Virtual Network" src="https://github.com/user-attachments/assets/65b3d6cc-771c-4e69-bb20-63f07bc52f7c" />

Select a subscription, and continue to name your resource group, then click review and create.


<img width="512" height="320" alt="Virtual network 2" src="https://github.com/user-attachments/assets/3e2815ca-51ce-416e-8674-8464a841724d" />

Review plus create  ends up as a completed creation. Why it matters: A resource group acts like a folder gathering all the AD‑lab components in one place so you can clean everything up later without fuss.




Create a Virtual Network and Subnet



Now you will create a Virtual Network, select your subscription and resource group name. Next you will Name your Virtual network Active-Directory-Vnet and select your region.


<img width="512" height="320" alt="compute infrastructure" src="https://github.com/user-attachments/assets/2072adb0-d2f1-4b76-8c3e-eeb699132c0f" />

Search for networks  then click Create.
Subscription/Resource group: choose the ones you just set up.
Name: Active‑Directory‑VNet 
Region: mirrors the RG.


<img width="1600" height="1000" alt="Virtual network 3" src="https://github.com/user-attachments/assets/dbf60870-cdf7-4157-9efe-1c9a5e961d14" />

Create another virtual network, select your subscription and resource group from the previous step. Name your new virtual network and select your region for this example it will be (US) East US 2.


<img width="1600" height="1000" alt="active directory vnet" src="https://github.com/user-attachments/assets/06338b04-c84d-4020-8632-efce1fcb1f25" />

Take a moment to review then go and create—what you end up with is simply a creation. Why it matters: The 10.0.0.0/16 prefix supplies breathing space for an array of subnets.  Define at least one subnet,  Azure will automatically spin up a default if none are defined.  What you see: a callout noting, When you create a VNet you set an address space say 10.0.0.0/16 and then define one or more subnets. Confirm the address space appears as 10.0.0.0/16 and verify that a subnet is available  for instance the default 10.0.0.0/24. Why it matters, The DC and the client need to end up inside this space for them to talk to each other.







Create the Domain Controller VM (Windows Server 2022)



<img width="1600" height="1000" alt="Compute infrastructure 2" src="https://github.com/user-attachments/assets/644bd157-9473-4b07-941f-6bdd783c80c7" />

The resource group is called AD‑Lab‑RG. The VM’s name is DC‑1. Make sure the Region stays the same. Administrator account: conjure an username and pair it with a sturdy password. During the configuration process any incoming Remote Desktop Protocol traffic, on port 3389 is permitted. Keep cycling through the step until the UI finally surfaces a Review and Create prompt then jump straight into the solitary Create operation. That machine will serve as your Domain Controller. Pick a size that lets the roles install quickly.

<img width="1096" height="769" alt="create virtual machine 1" src="https://github.com/user-attachments/assets/eb1630c7-392f-447e-83d3-0259d93d9861" />
Create a resource group named AD‑Lab‑RG. Additionally create a VM named DC‑1.




<img width="1098" height="622" alt="Zone 1" src="https://github.com/user-attachments/assets/30b85ff1-2837-4c19-a35e-f7abcae6550c" />





Select windows  Image: a view of Windows Server 2022 Datacenter
Size/Memory: go for a setup that offers least 2 vCPUs and 8 GB RAM, 
for a smoother AD experience.








<img width="512" height="290" alt="seamless connection" src="https://github.com/user-attachments/assets/0c1cb934-6b20-40d5-9c0c-b0224deb5acf" />



Make sure you choose the right amount of memory, to have a seamless connection.




<img width="512" height="320" alt="virtual network 4" src="https://github.com/user-attachments/assets/96f135e1-97ea-43f2-8cba-ac6d5493073a" />



When you spin up a Virtual Network (VNet) you first pick an address space—say 10.0.0.0/16. Inside that VNet you then carve out one or more subnets.



DC-1 – Networking tab attaching to your VNet


<img width="1600" height="1000" alt="DC-1 RDP3389" src="https://github.com/user-attachments/assets/5ba8098f-395f-4fbf-8c8d-ba29a4c6ba12" />



Pick the Active Directory Vnet. Leave the subnet at its default setting. Keep the page unchanged then proceed by clicking "Review and Create.”



<img width="1600" height="1000" alt="Virtual machine 2" src="https://github.com/user-attachments/assets/615cb5b5-a22d-4da4-be0f-247b5083f948" />



Head over to the Networking tab it sports drop‑down selectors, for the network and its subnet. Please carry out the following
The virtual network is optional, for the Active‑Directory VNet. Subnet – leave it at the default. If you like, type, in the subnet your server runs on. Why it matters: this guarantees the domain controller lands squarely within the network you’ve built paving the way for the client to join the domain afterward.


<img width="1600" height="1000" alt="Deployment 1" src="https://github.com/user-attachments/assets/78ebd87c-8076-4d3e-84fe-fc851d0580b7" />


Now that the Windows Server is up we’ll go ahead and create another virtual machine.

Create the Client VM (Client-1) – Basics 












<img width="1600" height="1000" alt="CI-Virtual machines" src="https://github.com/user-attachments/assets/6d72c4f6-62e5-4734-8585-6cbe5d66e7de" />


Create a machine cue that pops up again for the client. Set up admin credentials by specifying a username and password. Hook the system to the Active‑Directory‑VNet ensuring it claims the domain controller’s subnet or alternatively lodge it in a client subnet, on the VNet.
Create which at its core merely denotes creation, the machine will eventually point its DNS to DC‑1 thereby becoming part of the domain.















