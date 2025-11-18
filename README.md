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
Create the Domain Controller VM (Windows Server 2022) named DC-1, add your Username and password
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
Select Subscription/Resource group,  choose the ones you just set up.
Type in the name  Active‑Directory‑VNet. 
Select the region  mirrors the RG.


<img width="1600" height="1000" alt="Virtual network 3" src="https://github.com/user-attachments/assets/dbf60870-cdf7-4157-9efe-1c9a5e961d14" />

Create another virtual network, select your subscription and resource group from the previous step. Name your new virtual network and select your region, in this case  it will be (US) East US 2.


<img width="1600" height="1000" alt="active directory vnet" src="https://github.com/user-attachments/assets/06338b04-c84d-4020-8632-efce1fcb1f25" />

Take a moment to review then click on create, the 10.0.0.0/16 will have many different subnets.  Define at least one subnet,  Azure will automatically create a  default if none are defined. You will see a callout noting, When you create a VNet you set an address space say 10.0.0.0/16 and then define one or more subnets. Confirm the address space appears as 10.0.0.0/16 and verify that a subnet is available  for instance the default 10.0.0.0/24. This way the DC and the client need to end up inside this space for them to talk to each other.







Create the Domain Controller VM (Windows Server 2022)



<img width="1600" height="1000" alt="Compute infrastructure 2" src="https://github.com/user-attachments/assets/644bd157-9473-4b07-941f-6bdd783c80c7" />

The resource group is called AD‑Lab‑RG. The VM’s name is DC‑1. Make sure the Region stays the same. For the administrator account create a username and pair it with a memorable and strong password. During the configuration process any incoming Remote Desktop Protocol traffic, on port 3389 is permitted. Keep cycling through the step until the UI finally surfaces a Review and Create prompt then jump straight into the solitary Create operation. That machine will serve as your Domain Controller. Pick a size that lets the roles install quickly.

<img width="1096" height="769" alt="create virtual machine 1" src="https://github.com/user-attachments/assets/eb1630c7-392f-447e-83d3-0259d93d9861" />
Create a resource group named AD‑Lab‑RG. Additionally create a VM named DC‑1.




<img width="1098" height="622" alt="Zone 1" src="https://github.com/user-attachments/assets/30b85ff1-2837-4c19-a35e-f7abcae6550c" />





Select windows  Image: a view of Windows Server 2022 Datacenter
Size/Memory: go for a setup that offers least 2 vCPUs and 8 GB RAM, 
for a smoother AD experience.








<img width="512" height="290" alt="seamless connection" src="https://github.com/user-attachments/assets/0c1cb934-6b20-40d5-9c0c-b0224deb5acf" />



Make sure you choose the right amount of memory, to have a seamless connection.




<img width="512" height="320" alt="virtual network 4" src="https://github.com/user-attachments/assets/96f135e1-97ea-43f2-8cba-ac6d5493073a" />



When you spin up a Virtual Network (VNet) you will  first pick an address space say 10.0.0.0/16. Inside that VNet you then carve out one or more subnets.



DC-1 – Networking tab attaching to your VNet


<img width="1600" height="1000" alt="DC-1 RDP3389" src="https://github.com/user-attachments/assets/5ba8098f-395f-4fbf-8c8d-ba29a4c6ba12" />



Pick the Active Directory Vnet. Leave the subnet at its default setting. Keep the page unchanged then proceed by clicking Review and Create.



<img width="1600" height="1000" alt="Virtual machine 2" src="https://github.com/user-attachments/assets/615cb5b5-a22d-4da4-be0f-247b5083f948" />



Head over to the Networking tab it sports drop‑down selectors, for the network and its subnet. Please carry out the following
The virtual network is optional, for the Active‑Directory VNet. Subnet leave it at the default. Type, in the subnet your server runs on. This guarantees the domain controller lands squarely within the network you’ve built paving the way for the client to join the domain afterward.


<img width="1600" height="1000" alt="Deployment 1" src="https://github.com/user-attachments/assets/78ebd87c-8076-4d3e-84fe-fc851d0580b7" />


Now that the Windows Server is up we’ll go ahead and create another virtual machine.

Create the Client VM (Client-1) – Basics 












<img width="1600" height="1000" alt="CI-Virtual machines" src="https://github.com/user-attachments/assets/6d72c4f6-62e5-4734-8585-6cbe5d66e7de" />


Create a machine cue that pops up again for the client. Set up admin credentials by specifying a username and password. Hook the system to the Active‑Directory‑VNet ensuring it claims the domain controller’s subnet or alternatively lodge it in a client subnet, on the VNet.
Create which at its core merely denotes creation, the machine will eventually point its DNS to DC‑1 thereby becoming part of the domain.


<img width="512" height="320" alt="Virtual machine -3" src="https://github.com/user-attachments/assets/90672605-b68a-4cd5-8cfd-a1d57e25b575" />

Go back to Virtual machines and click and create a Virtual Machine.


<img width="512" height="258" alt="Client-1" src="https://github.com/user-attachments/assets/68358f3d-3ef8-4216-8918-7615025b2747" />

Createv resource group identical to the one, for the DC. Name it  Client‑1, as the assigned client tag.

<img width="512" height="258" alt="Client-1 East US@" src="https://github.com/user-attachments/assets/221544f0-3661-40b2-9873-40b8bca175c5" />

Fill in the details and name your virtual machine Client-1, also select East US 2 and make sure that the zone matches with what you choose the first time.


<img width="512" height="334" alt="Windows 10 pro" src="https://github.com/user-attachments/assets/a8b2361b-fb2b-4ac4-b288-671e54230340" />

Choose Image  Windows 10  or alternatively Windows 11 Pro. Size: 2 vCPU, 4–8 GB.

<img width="512" height="334" alt="Image-client 1" src="https://github.com/user-attachments/assets/c250b590-f00f-40ba-8d6a-8fae23f6bfe3" />

Change image to Windows 10 pro, Version 22H2-x64 Gen2

<img width="512" height="292" alt="Click Review and Accept" src="https://github.com/user-attachments/assets/1369f09b-cb70-454f-9312-9bbebe998c4f" />

Make sure all information is correct and then click review, and continue to the next step.

<img width="1600" height="1000" alt="Create Virtual machine 2" src="https://github.com/user-attachments/assets/94ee937b-29b9-46e9-b5c4-600ec1bcba80" />

<img width="1600" height="910" alt="Deployment 2" src="https://github.com/user-attachments/assets/e253b4b8-bb05-45b7-9f1e-231a13291e6a" />

Click on create and wait until the deployment process is completed.

<img width="1600" height="910" alt="Deployment 3" src="https://github.com/user-attachments/assets/a8d84bc5-cce7-429f-83e6-bb795152fd39" />

<img width="1600" height="1000" alt="DC-1165" src="https://github.com/user-attachments/assets/3be24ee3-e1ae-49e3-8515-59f88ae91701" />

Deployment successful. Your deployment is a page. Go back into the resource and double‑check that it’s running and correctly attached to the VNet/subnet. Take a moment for a sanity check before you press on with the DNS and domain steps.




 Networking validation panels 


 <img width="1600" height="1000" alt="Dynamic" src="https://github.com/user-attachments/assets/5c471a46-1141-4ba1-8fe5-a5ac529405f8" />

 In this section we will change the private IP Address from Dynamic to Static.

 <img width="1600" height="1000" alt="Edit Ip Configuration" src="https://github.com/user-attachments/assets/420b7842-a4b4-4b79-9f9d-dc92fb16ea4b" />

 Verify that the private IP, on the DC‑1 NIC is set to static.

 <img width="1600" height="1000" alt="Static" src="https://github.com/user-attachments/assets/d6d1dc35-4edc-409e-874e-52c01d2a3da7" />

 On Client‑1 NIC, double   check that it’s part of the same VNet and that it sits in the correct subnet. When the machines aren’t situated together correctly they fail to discover each other or the domain.


 Disabeling The Firewall



 <img width="1600" height="1000" alt="Disabeling firewall" src="https://github.com/user-attachments/assets/0925cdcd-9a8d-44b0-a41c-d3b8b60f0895" />

 In this section we will be disabling the fire wall, when setting up AD the Domain Controller and the Client have to ping the Domain Controller and the Client. As you can see that the Domain Controller and the Client also have to talk through ports and the ports include DNS, LDAP, SMB and others. The firewall can block these until proper inbound/outbound rules are created. Now  select the start menu, click on run then type wf.msc 


 <img width="1600" height="1000" alt="Profile turned off" src="https://github.com/user-attachments/assets/e4d9ac7d-cca9-4761-a03e-c7888631535d" />

 You will now disable the fire walls, click private profile and select for firewall state off.


 <img width="1600" height="1000" alt="Select firewall state off" src="https://github.com/user-attachments/assets/90cec3e9-11e7-48bb-b50c-cfd1374d4e39" />

 Select Firewall state as off, and select ok and continue.


 <img width="1600" height="1000" alt="public profile" src="https://github.com/user-attachments/assets/d6936b8b-30cd-4466-b97e-dddb2363c9b9" />

 Do the same for the following public profile select firewall state as off. Then select apply and all firewalls will be disabled. Just disable the two profiles leave the third as is.


 <img width="1600" height="1000" alt="windows defender wall" src="https://github.com/user-attachments/assets/eaa1113b-7bfe-4440-ad79-baea2747f4d4" />

 Just disabled the domain profile and private profile firewalls, this is done to prevent the firewall from  blocking  these two profiles until proper inbound/outbound rules are created. Leave the public profile on its own, do not change it. 


 <img width="1600" height="1000" alt="Client-1 Network settings" src="https://github.com/user-attachments/assets/35c1f4b8-800d-4d23-a90b-57ac66fdd8d4" />

 From DC-1 you will copy the Private Ip Address 10.0.0.4 and place it in Client-1.



<img width="1600" height="1000" alt="Client-1 Network settings 2" src="https://github.com/user-attachments/assets/1cbb5b87-0bdc-45b1-9210-8a1ffbbe8076" />

Go into Client-1 and click on Network settings, and look for Client-1 NIC and click on it.


<img width="1600" height="1000" alt="Client-1 DNS Servers" src="https://github.com/user-attachments/assets/39322c05-977f-43d2-b91b-a10bbe553c7a" />

Now click on DNS servers you will notice it has inherited from virtual network checked off in blue, you will unmark it and select Custom.


<img width="1600" height="1000" alt="Client-1 DNS Servers 2" src="https://github.com/user-attachments/assets/a511276d-a1cd-4f2e-b4e1-d7a5a161cca3" />

Now you will paste the DC-1’s Private Ip Address where it states add DNS server.


<img width="1600" height="1000" alt="Client-1 DNS Servers 3" src="https://github.com/user-attachments/assets/50776c44-2395-4a68-ba44-a75c755759d3" />

By doing this it will allow us into the domain, click save and allow for this process to be deployed. 





Restarting Client-1



<img width="1600" height="1000" alt="Client-1 restart" src="https://github.com/user-attachments/assets/29d9ccae-c361-4f95-9a44-ee3fec81e990" />

Return to the Azure portal and select restart Client-1 


<img width="1600" height="1000" alt="Select restart again" src="https://github.com/user-attachments/assets/ee7ab62c-3e4b-4bdd-bb1a-1d0f0f70130c" />

Select yes to restart the Client-1 VM, after completing this step we will now log into Client-1 to open powershell and run ipconfig /all.  To have access to Client-1 you will need to copy the public IP Address and paste it to remote desktop.



  <img width="1600" height="1000" alt="Poweshell-1" src="https://github.com/user-attachments/assets/4fd9a295-7428-486e-81d2-869019b80c68" />

    Once logged in you will search in the search bar and locate Windows Powershell, Select that and continue to use  Dc-1’s  Private address to continue to the next step.


   <img width="1600" height="1000" alt="powershell-2" src="https://github.com/user-attachments/assets/30ea576d-af1e-44d2-ab22-3e52a4e52af5" />

   Type ping and paste DC-1’s private IP Address 10.0.0.4 then press enter.


  <img width="1600" height="1000" alt="powershell-33" src="https://github.com/user-attachments/assets/396ea002-e4a2-4041-aff8-13a66c1ccaf2" />

  Now it will ping, notice if done correctly you will see information in regards to the private IP address. If the ping wasn’t successful you would see messages that state, Destination host unreachable. This could be from having different virtual networks or DC-1’s firewall is not disabled. 


  <img width="1600" height="1000" alt="powershell-4" src="https://github.com/user-attachments/assets/06ac90d8-3816-496f-ba6d-1a32c24faf64" />

  Now you will run Ipconfig /all, when the information is displayed you will located the DNS servers with the private Ip Address from DC-1 10.0.0.4 


This concludes the Active Directory process to create a Domain Controller and a Client Machine within the same virtual network.

























 







