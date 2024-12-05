<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory Deployment and Configuration </h1>


<p>This project provides a comprehensive guide to deploying and configuring Active Directory on a designated Domain Controller (DC-1) virtual machine. It includes steps to install Active Directory, promote the server to a Domain Controller, create user accounts, and join a client machine (Client-1) to the domain. The tutorial also covers configuring Remote Desktop access for non-administrative users, ensuring a secure and functional Active Directory environment within Azure.

</p>





<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)
- macOS 


<h2>Creating Our Resource, Network, & Virtual Machines </h2> 
<br>

<h3>&#9312; Create The Resource Group</h3>

  <img width="348" alt="0" src="https://github.com/user-attachments/assets/6c7e9a17-44eb-44f1-a383-abb8bf2a97b0">

  <br>
  
- Go to https://portal.azure.com/#home to get started
  
- Once you are there click on/ search Resource Groups and afterward click on create
  
- For me, I named mine Active-Directory-Lab, and for the region, since I'm located in the Eastcoast East US 2 worked out

- Create the resource group once you receive the Validation passed green check mark
  
  <br><br>

<h3>&#9313; Create the Virtual Network</h3>

<img width="410" alt="0A" src="https://github.com/user-attachments/assets/5dbe7a9b-87a0-4c3f-a73f-5e85faaf0e47">

<br>

- For this new step we will be creating the virtual network instead of having the virtual machine do it for us

- Search for Virtual Networks then hit create 

- Put it in your resource Group that we made, this network will be named Active-Directory-VNet

- select your region, once you hit review and create hit create

  
<h3>&#9313; Create The Virtual Machines</h3>

<img width="558" alt="1" src="https://github.com/user-attachments/assets/fa689f9f-99ff-4d91-86ac-0be9625dc3f5">


<br>

- Search for Virtual Machines and hit create 

- Select your resource group, for the virtual machine name I just made it DC-1
  
- Selected my region, for availability options I left that at Availability Zone with Self-selected zone also bubbled, for the rest just put in exactly what I have displayed and finally the image selected for this virtual machine is Windows Server 2022 Datacenter Azure Edition - x64 Gen 2
  <br>
  
<img width="545" alt="1A" src="https://github.com/user-attachments/assets/b3585c30-9b36-410e-b2c8-76b6c8fc3bb4">

- When it comes to the size make sure you have at least 2 VCPUs, for the username and password make sure you have it written down in your notes

<img width="554" alt="1B" src="https://github.com/user-attachments/assets/8506c85c-be52-4ff6-b380-99c1d316bd8c">

- Checkmark the licensing agreement


<h2>Configuration Steps</h2>

<h3>&#9312; Install Active Directory in DC-1</h3>

- In the Server Manager dashboard, click 'Add Roles and Features' and continue the setup
<img width="680" alt="AD-setup" src="https://imgur.com/cQnpkfN.png">

<p>

</p>

<p><strong> Select Active Directory Domain Services and finish the installation </strong> </p>
<p>
</p>

<h3>&#9313; Promote DC-1 to Domain Controller </h3>

- Once the installation is done, notice the flag on the Server Manager
- Click on the flag and promote DC-1 to Domain Controller

<img width="350" alt="notif" src="https://imgur.com/4W04gBQ.png">



-  Next, we will select 'Add a new forest' and set the Root domain name to “mydomain.com”
<p>
<img width="565" alt="my domain" src="https://imgur.com/ovGgm26.png"> </p>
  
- Finish setup and restart DC-1
- Log back into Remote Desktop with your username credentials following with "@mydomain.com" 



<h3>&#9314; Create an Admin in Active Directory </h3>

- Once DC-1 has rebooted, click on tools and select Active Directory Users and Computers
- Right click on mydomain.com; select -> New -> Organizational Unit 
<img width="500" alt="Users" src="https://imgur.com/VESNQeS.png">

<br>

<p><strong> We will create two OU's labeled "_EMPLOYEES" and "_ADMINS" </strong></p>

<img width="500" alt="admins" src="https://imgur.com/vsSxufF.png">



<p><strong>Right click on Users and create a new user named "Jane Doe" with the username "jane_admin"</strong></p>

<img width="450" alt="jane doe" src="https://imgur.com/n9RKfcz.png">



<p><strong>We will change Jane Doe into an admin account by right clicking her name and adding her to the “Domain Admins” security group</strong></p>

<img width="450" alt="add to group" src="https://imgur.com/n9RKfcz.png">



<p><strong>Logout of DC-1 and sign back in with Jane Doe’s credentials</strong></p>

<img width="400" alt="jane login" src="https://imgur.com/EnnzYVs.png">



<h3>&#9315; Join Client-1 to Domain </h3>

<p><strong> For Client-1 to join the domain, the DNS server must be changed. Therefore we will set it's DNS server as DC-1's private IP address</strong></p>

- In the Azure Portal, select Client-1 -> Networking -> Network interface -> Settings -> DNS Server

<img width="350" alt="dns servers" src="https://imgur.com/9bKXViA.png">


<p><strong>Select custom DNS server and type in the private IP address of DC-1 and restart Client-1 virtual machine in Azure</strong></p>

<img width="410" alt="dns servers2" src="https://imgur.com/5hhy1Ac.png">


<p><strong> Now log back in to Client-1 using your original credentials. Click start and go to Settings -> Rename this PC (advanced) -> Change and add “mydomain.com” and login with the admin credentials previously created (jane_admin) </strong></p>

<img width="310" alt="remote desktop first login" src="https://imgur.com/OsjB5gK.png">

<br>

<p> <strong>Once Client-1 has been added, the VM will restart.</strong></p>



<h3>&#9316; Setup Remote Desktop for non-administrative users </h3>

- Log back into Client-1 using "jane_admin" credentials and open Settings -> Remote Desktop -> User Accounts and click “Select users that can remotely access this PC”
- Add Domain Users

<br>


<img width="350" src="https://imgur.com/R2sxVPR.png">

<p><strong>This allows normal users to login to Client-1</strong></p>

<br>




<h2> Final Thoughts </h2>

<p>
We've successfully completed the Active Directory Deployment and Configuration phase. By configuring Active Directory on the Domain Controller, we established our infrastructure, created a forest and administrator account, and integrated Client-1 into the domain. </p>







