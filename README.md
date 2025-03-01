<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>


<h1>Active Directory Deployment and Configuration </h1>


This project provides a comprehensive guide to deploying and configuring Active Directory on a designated Domain Controller (DC-1) virtual machine. It includes steps to install Active Directory, promote the server to a Domain Controller, create user accounts, and join a client machine (Client-1) to the domain. The tutorial also covers configuring Remote Desktop access for non-administrative users, ensuring a secure and functional Active Directory environment within Azure.







<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022 Datacenter Azure Edition - x64 Gen 2
- Windows 10 Pro, Version 22H2 - x64 Gen 2
- macOS 


<h1>Creating Our Resource, Network, & Virtual Machines </h1> 
<br>

<h3>&#9312; Create The Resource Group</h3>


<img width="348" alt="0" src="https://github.com/user-attachments/assets/6c7e9a17-44eb-44f1-a383-abb8bf2a97b0">

<br>
  
- Go to https://portal.azure.com/#home to get started
  
- Once you are there click on/ search Resource Groups and afterward click on create
  
- For me, I named mine Active-Directory-Lab, and for the region, since I'm located in the Eastcoast, East US 2 worked out

- Create the resource group once you receive the Validation passed green check mark
  
<br>

<h3>&#9313; Create the Virtual Network</h3>

<img width="410" alt="0A" src="https://github.com/user-attachments/assets/5dbe7a9b-87a0-4c3f-a73f-5e85faaf0e47">

<br>

- For this new step we will be creating the virtual network instead of having the virtual machine do it for us

- Search for Virtual Networks then hit create 

- Put it in your resource Group that we made, this network will be named Active-Directory-VNet

- select your region, once you click on "Review + Create," hit "Create"

<br>
  
<h3>&#9314; Please proceed with the creation of the virtual machines, beginning with DC-1</h3>

<img width="558" alt="1" src="https://github.com/user-attachments/assets/fa689f9f-99ff-4d91-86ac-0be9625dc3f5">


<br>

- Search for Virtual Machines and hit create; Make sure to click on Azure Virtual Machine 

- Please select your designated resource group. For the name of the virtual machine, I have chosen "DC-1"
  
- I have selected my region and configured the availability options to "Availability Zone," ensuring that "Self-Selected Zone" is also marked. For all other settings, I have retained the options as displayed. Furthermore, I have chosen the image for this virtual machine as "Windows Server 2022 Datacenter Azure Edition - x64 Gen 2"

<br>
  
<img width="545" alt="1A" src="https://github.com/user-attachments/assets/b3585c30-9b36-410e-b2c8-76b6c8fc3bb4">

<br>

- When determining the appropriate size, it is essential to ensure that there are a minimum of 2 virtual CPUs (VCPUs) allocated. Additionally, it is advisable to document your username and password in a secure location for future reference

<br>

<img width="554" alt="1B" src="https://github.com/user-attachments/assets/8506c85c-be52-4ff6-b380-99c1d316bd8c">

<br>

- Please ensure that both of the licensing agreements presented are checked, and then proceed by selecting the Networking option
  
<br>

<img width="556" alt="1C" src="https://github.com/user-attachments/assets/2fb1fb90-1a66-4952-9346-943647be0548">
  
<br>
  
- When configuring the virtual network option, please ensure that you select the Virtual Network that has been established, It is advisable to retain all other settings at their default values, After confirming these selections, click on "Review + Create," followed by "Create" Upon completion of this process, we will proceed to create the subsequent virtual machine, designated as Client 1

<h3>&#9315; Set up the virtual machine named Client-1 </h3>

<br>
  
<img width="551" alt="2" src="https://github.com/user-attachments/assets/0a1cb73f-08da-4ec7-8ab1-c315c39e7eb3">

<br>

- The virtual machine will be designated as "Client-1"

- Put it in the same resource group that you made

- We will be using Windows 10 Pro, Version 22H2 - x64 Gen 2 for the image

<br>

<img width="552" alt="3" src="https://github.com/user-attachments/assets/df842a56-0c16-4278-8404-2550690f59c5">
  
<br>

- Make sure the size has at least 2 vcpus, and write down the username 
 and password for this virtual machine as well

<br>

<img width="557" alt="4" src="https://github.com/user-attachments/assets/183db735-7a52-4d52-8c82-59253e9c8358">
  
<br>

- Heading over to Networking we will place this Virtual Machine in the Active-Directory-VNet that we made
 
- Leave the rest to its defaults and click on "Review + Create," followed by "Create"

<br>

<img width="1274" alt="4A" src="https://github.com/user-attachments/assets/a4fde97d-0d0c-4c2c-a518-78ba07d70d88">

<br>

- Here are the 2 Virtual machines that we will be using for the rest of this project

<h1> Configuration Steps</h1>
  <br>

<h3>&#9312; Change DC-1's Nic Private IP address to be static</h3>

<br>

- We will begin by going to the virtual machine dc-1 and going to the network settings

<img width="1486" alt="5" src="https://github.com/user-attachments/assets/fd555109-48a1-4e0e-8ba9-796d9f6f6582" />

<br>

- Click on the Network interface card for dc-1 
<br>

<img width="1325" alt="6" src="https://github.com/user-attachments/assets/40354938-12eb-4927-9693-6559be383ce2" />

<br>

- Click on ipconfig located at the bottom to alter this to Static instead of dynamic
<br>

<img width="505" alt="7" src="https://github.com/user-attachments/assets/9cb9dee8-084d-4824-9912-10be5239f355" />

<br>

- Under Private IP address settings instead of dynamic click on static and save this

- Once you save this head back into dc-1's network settings

- The Private IP address should no longer change regardless of how many times the virtual machine is restored

  <br>

<h3>&#9313; Connect to DC-1</h3>

<br>

- First, copy the public IP address in dc-1

<img width="276" alt="Screenshot 2025-01-13 at 1 12 03 PM" src="https://github.com/user-attachments/assets/f63c13d1-7408-4d1c-9568-884061a5557e" /> 

<br>


- Go to the App Store on Mac and download this app. We are going to use remote desktop to connect to our Windows Server virtual machine

<img width="287" alt="Screenshot 2024-09-19 at 12 28 36 PM" src="https://github.com/user-attachments/assets/fc0b9142-ae88-4315-9a78-b2649a841455">

<br>

- Open Microsoft Remote Desktop --> Click on the Plus icon and click on add Pc --> Name it dc-1 in "Friendly Name:" ---> paste the public IP address in the PC name ---> press add to connect (if needed put in the username and password u made to connect)

<br>

<img width="601" alt="Screenshot 2025-01-12 at 8 00 32 PM" src="https://github.com/user-attachments/assets/a82711e7-80c0-4aa3-9bea-3e06a4c41c91" />

<br>

<img width="470" alt="Screenshot 2025-01-12 at 8 16 35 PM" src="https://github.com/user-attachments/assets/74d8cbbb-70f5-408a-b61f-b737f8123a43" />

  
<br>

<img width="1676" alt="12" src="https://github.com/user-attachments/assets/a1fafc6e-e3af-441a-af58-bd18ac2b7a8e" />

<br>

- Once connected and loaded if you don’t have Server Manager pop up at the start then you logged in to the wrong virtual machine or created the wrong type

<br>
  

<h3>&#9314; Turn the firewall off for DC-1</h3>

<img width="414" alt="Screenshot 2025-01-12 at 8 23 32 PM" src="https://github.com/user-attachments/assets/712d2f39-f64d-42ca-9aa3-a9a02df4293c" />


<br>



- In the domain controller right click the start menu and press run, type wf.msc this is for the Windows firewall



- In the firewall, we are going to disable it so click on Windows Defender Firewall Properties ---> hit the off option for the Firewall state on every profile ---> hit apply then OK

- After that, the firewall should be off

<br>

<img width="1239" alt="Screenshot 2025-01-12 at 8 36 28 PM" src="https://github.com/user-attachments/assets/2c3fe0df-b0cc-4b11-b24e-771a91436397" />

<br>

<img width="645" alt="Screenshot 2025-01-13 at 1 27 31 PM" src="https://github.com/user-attachments/assets/886ff4e7-fde7-42f2-acd0-d68725439e7c" />

<br>


<h3>&#9315; Set Client-1's DNS settings to DC-1's Private IP address </h3>

<img width="509" alt="Screenshot 2025-01-13 at 1 41 14 PM" src="https://github.com/user-attachments/assets/e877b66e-82cd-4162-8ff9-b4b1ba0b8c0a" />

<br>

<img width="310" alt="Screenshot 2025-01-13 at 1 44 22 PM" src="https://github.com/user-attachments/assets/57ffa1f7-7ca4-4a05-ba6c-bc4cdf27dcbb" />

<br>


- First back in the Azure portal get DC-1's Private IP address and copy it, then go to Client 1 --> Networking --> Network Settings and click on Client 1's Virtual Network Interface Card

<br>



<img width="448" alt="Screenshot 2025-01-13 at 1 48 24 PM" src="https://github.com/user-attachments/assets/b9ae6fb4-8328-4e0a-8fc4-43d7012dbf12" />

<br>


- Click on DNS servers, hit custom, and then paste the IP address of DC-1 that you copied from the Azure portal

- Whenever the computer needs to look up anything, for instance, Google.com, it will look to DC-1 for it

- Doing this will allow us to join the domain

- Hit Save

- If that doesn't work because there is some issue when you paste it in, type that number in instead

<br>

<img width="873" alt="Screenshot 2025-01-13 at 1 52 53 PM" src="https://github.com/user-attachments/assets/38fc1b75-1190-445b-a2d2-94177961d56f" />


- Then go to your Virtual Machines in Azure, click the box next to Client-1, and press restart at the top

<br>

<img width="219" alt="Screenshot 2025-01-13 at 2 00 10 PM" src="https://github.com/user-attachments/assets/2533ef36-8a04-4d1b-90c8-a9ba85bd794c" />

<br>

- From here, we will attempt to log in to Client 1 and attempt to ping DC-1's private IP address
  

- Click on Client 1 in Azure and copy its Public IP address

<br>

<img width="566" alt="Screenshot 2025-01-13 at 2 11 20 PM" src="https://github.com/user-attachments/assets/346e17d4-54c0-49a2-9569-a55260c9dbbd" />

<br>

- Then head on over to remote desktop to enter Client-1, we are going to name this "client-1", and make sure to put in your username and password that you wrote down

- Head on over to DC-1 in Azure to get that private IP address

<br>

<img width="345" alt="Screenshot 2025-01-13 at 2 18 14 PM" src="https://github.com/user-attachments/assets/f0977b85-74d9-446c-ad02-ca4c3afbe251" />

<br>

- Login to Client-1 and Open up PowerShell

<br>

<img width="399" alt="Screenshot 2025-01-13 at 2 23 48 PM" src="https://github.com/user-attachments/assets/fec097d2-64b0-4725-8a33-70598c9df435" />

<br>

- In PowerShell type ping and DC-1's private IP address and press enter

- If the output says "Destination host unreachable," then they are probably in different virtual networks, or DC-1's firewall is probably still on, or ping is being blocked somehow.

<br>

<img width="243" alt="Screenshot 2025-01-13 at 2 26 25 PM" src="https://github.com/user-attachments/assets/d5e91e87-4302-4aa6-b8a0-ded88b4dbb72" />
<br>

- Type in PowerShell ipconfig /all

<br>

<img width="563" alt="Screenshot 2025-01-13 at 2 28 11 PM" src="https://github.com/user-attachments/assets/80f13c37-ecd8-4782-8d8b-60cc7f7832b1" />

<br>


- Upon execution, the line pertaining to the DNS servers should display the private IP address of DC-1 that I have highlighted here.

- Now client 1 should be using DC-1 as the DNS server

<br>







<h1> Configuration Steps Pt. 2 </h1>

<br>


<h3>&#9312; Install Active Directory and Domain services in DC-1 </h3>

<br>

<img width="336" alt="Screenshot 2025-01-13 at 2 39 31 PM" src="https://github.com/user-attachments/assets/54a01f9e-e0a3-4826-a1de-4fb18cb3f38e" />

<br> 

- To make sure which virtual machine you are in see if the Microsoft store is located below in the taskbar if so that would be Windows 10 which is not DC-1

- Another way is going into your system settings and looking at the operating system

- Please navigate to the search bar located below and enter "Server Manager" if it is not displayed in the Start menu.

<br>

<img width="1676" alt="12" src="https://github.com/user-attachments/assets/dc010b2f-170c-4fd3-8c1f-8a63bb7a29a4" />

<br>
<br>

- In the Server Manager dashboard, click 'Add Roles and Features' and continue the setup

<br>

- You’re going to click on "Next" mostly throughout the setup

<br>

<img width="789" alt="Screenshot 2025-01-13 at 3 16 40 PM" src="https://github.com/user-attachments/assets/f352a00e-0c5b-43ff-970e-cfd2149d9a2e" />
<br>
<img width="787" alt="Screenshot 2025-01-13 at 3 16 58 PM" src="https://github.com/user-attachments/assets/c07f0d3d-7bf2-441a-b082-ae30e729732b" />
<br>






- For Server Selection, there should only be 1 which is DC-1


<img width="774" alt="14" src="https://github.com/user-attachments/assets/9f9e56d2-a6bf-4bdb-a4c2-0eaf2402862a" />




<br>

- In Server Roles check mark Active Directory Domain Services --> hit add features


<img width="413" alt="Screenshot 2025-01-13 at 3 17 23 PM" src="https://github.com/user-attachments/assets/c7b67da3-1b64-4ae8-8d4e-fcd0c964f006" />

<br>

<img width="245" alt="Screenshot 2025-01-13 at 3 17 43 PM" src="https://github.com/user-attachments/assets/9a51261e-a992-44ed-b3ea-a5c71ee075a6" />

<br>

<img width="785" alt="Screenshot 2025-01-13 at 3 18 07 PM" src="https://github.com/user-attachments/assets/808961aa-ebac-485d-8275-efe980164163" />


<br>


<img width="785" alt="Screenshot 2025-01-13 at 3 18 20 PM" src="https://github.com/user-attachments/assets/10f49db8-47fa-4001-b3dc-c35bdbfa6853" />


<br>




- Then hit Next, Check mark "Restart the destination server automatically if required" --> click YES --> press Install


<img width="786" alt="Screenshot 2025-01-13 at 3 18 45 PM" src="https://github.com/user-attachments/assets/ceb86aae-889c-4cd7-a0e6-f34df75f3834" />

<br>


- After the installation hit close


<img width="783" alt="Screenshot 2025-01-13 at 3 25 46 PM" src="https://github.com/user-attachments/assets/26f433be-1e43-4ecb-b777-97dcc14e1622" />

<br>



<h3>&#9313; Promote DC-1 to Domain Controller </h3>

<img width="377" alt="Screenshot 2025-01-13 at 3 28 42 PM" src="https://github.com/user-attachments/assets/0ee69569-7c21-4899-9cc5-228cd3e248b8" />


- Once the installation is done, notice the flag on the Server Manager at the top right
  
- Click on the flag and press the highlighted text "promote this server a.k.a DC-1 to Domain Controller"

<br>

<img width="761" alt="Screenshot 2025-01-13 at 3 29 19 PM" src="https://github.com/user-attachments/assets/9a44f642-7e75-476c-b7c2-0a7a59b1ff1c" />



-  Next, we will select 'Add a new forest' and set the Root domain name to “mydomain.com”

<br>


<img width="760" alt="Screenshot 2025-01-13 at 3 31 07 PM" src="https://github.com/user-attachments/assets/aa6fa371-a86e-4c78-aeba-42c6bd56f106" />


-  Hit Next, where it says "Directory Services Restore Mode (DSRM) password"  Just put in a password that you can remember and confirm it

<br>

<img width="761" alt="Screenshot 2025-01-13 at 3 31 26 PM" src="https://github.com/user-attachments/assets/09cf3b62-bfb7-426b-be9d-87e17fd6adc4" />

- Uncheck Create DNS delegation then hit Next

<br>

<img width="758" alt="Screenshot 2025-01-13 at 3 31 54 PM" src="https://github.com/user-attachments/assets/dd95e224-8413-4005-9db5-dbfccaf66b59" />

- Click Next

<br>

<img width="761" alt="Screenshot 2025-01-13 at 3 32 13 PM" src="https://github.com/user-attachments/assets/019536f4-320e-4c01-82c4-1a54b850dfd6" />

- Click Next

<br>

<img width="760" alt="Screenshot 2025-01-13 at 3 32 27 PM" src="https://github.com/user-attachments/assets/e2b4962c-59d5-4b0a-b08d-01ef75a3ddf2" />

- Click Next

<br>

<img width="761" alt="Screenshot 2025-01-13 at 3 33 15 PM" src="https://github.com/user-attachments/assets/88bf4a55-d548-4b4e-aa94-d3f90b6231f7" />

- Click Install, And then wait for the new forest to be installed and this computer to be turned into a Domain Controller

<br>

<img width="682" alt="Screenshot 2025-01-13 at 3 35 36 PM" src="https://github.com/user-attachments/assets/afd51be8-27f4-4553-a7d6-80d437acefcf" />

- The Blue pop up will let you know the restart will be taking place and the server was successful in being changed

<br>



<img width="437" alt="49" src="https://github.com/user-attachments/assets/debafb06-c2fe-40ae-9e50-ee6da95b7640" />


- Log back into Remote Desktop this time with "mydomain.com\" followed by your username

- Since this time we will be logging in as a Domain User instead of a local context

<br>



<h3>&#9314; Create an Admin in Active Directory </h3>

<img width="273" alt="Screenshot 2025-01-14 at 11 30 02 AM" src="https://github.com/user-attachments/assets/9ffa0957-ed58-4877-9e5d-85a50725df69" />
<br>

<img width="561" alt="Screenshot 2025-01-14 at 11 35 27 AM" src="https://github.com/user-attachments/assets/4082bb87-eebc-4d4f-a49b-d8931dd70f66" />

<br>



- Once logged back into DC-1 type in Windows Administrative Tools then select Active Directory Users and Computers

<img width="754" alt="17" src="https://github.com/user-attachments/assets/8ab5cb56-9269-42f5-b58b-e82d6eeadde3" />


- Right click on mydomain.com; select --> New --> Organizational Unit 

<br>

<img width="425" alt="18" src="https://github.com/user-attachments/assets/4485c333-c24e-4534-88cc-0bb30fdc8545" />

<br>

<img width="168" alt="19" src="https://github.com/user-attachments/assets/c36f109c-fb75-4981-81bb-ec7a9523a592" />



- We will create two labeled "_EMPLOYEES" and "_ADMINS" 

<br>

<img width="360" alt="Screenshot 2025-01-14 at 12 01 17 PM" src="https://github.com/user-attachments/assets/3980bdaa-b36f-4e89-ae04-36f15902dc76" />

<br>

<img width="430" alt="20" src="https://github.com/user-attachments/assets/4c9c907d-4887-4ef4-9a37-18289100e50a" />



- Right click on _Admins folder, press -> New -> User and create a new user named "Jane Doe" with the username "jane_admin"

<br>

<img width="384" alt="Screenshot 2025-01-14 at 12 09 20 PM" src="https://github.com/user-attachments/assets/d03d773a-eed0-48af-9e35-7045a8d50d31" />


- Make sure to write down or remember the password you make for her

- Make sure to Uncheck "User must change password at next logon"

- Check "Password never expires"

<br>

<img width="369" alt="Screenshot 2025-01-14 at 12 21 44 PM" src="https://github.com/user-attachments/assets/ab2daee6-68ef-4501-be37-8d715321313b" />

<br>

<img width="249" alt="Screenshot 2025-01-14 at 12 27 48 PM" src="https://github.com/user-attachments/assets/81bb25ad-3e72-4212-8108-de4fa64b50d4" />



- We will change Jane Doe into an admin account by pressing the _ADMINS folder -> right-clicking her name -> Hit Properties -> and adding her to the “Domain Admins” Group

- Type in domain admins for the object names -> press Check Names for it to find the group

- Hit Ok -> Apply -> OK, Now the account is a Domain Admin giving her the ability to create Users, etc

- Next logoff or sign out

<br>

<img width="450" alt="add to group" src="https://imgur.com/n9RKfcz.png">



- Logout of DC-1 and sign back in with Jane Doe’s credentials

<img width="430" alt="23" src="https://github.com/user-attachments/assets/82ef4c94-c830-4bd3-9b75-b62c829b07c1" />




<h3>&#9315; Join Client-1 To The Domain </h3>

- First, get Client 1's public IP address and log into it


<img width="482" alt="Screenshot 2025-01-16 at 3 47 59 PM" src="https://github.com/user-attachments/assets/51d10314-80ce-44f3-abce-f26e3d4fc52b" />

- To join it to the Domain go into System settings --> About

<br>

<img width="185" alt="Screenshot 2025-01-16 at 3 47 51 PM" src="https://github.com/user-attachments/assets/3ac7b7cb-1e49-4b94-8180-b30c0b3cd361" />

- Click on "Rename this PC (advanced)"

<br>


<img width="404" alt="24" src="https://github.com/user-attachments/assets/ba0b9cdb-f99c-4384-a5fc-24436dacd263" />


- under the Computer Name tab click on Change

<br>

<img width="318" alt="29" src="https://github.com/user-attachments/assets/09aa36dd-65a9-4d81-bbd4-cec1bf5057e8" />


- To join it to a Domain you would select "Domain" then under "Member of" type in mydomain.com -> press OK

<br>

<img width="457" alt="Screenshot 2025-01-16 at 4 28 36 PM" src="https://github.com/user-attachments/assets/1bec6e7d-042b-4f5e-83e9-713ca92ab384" />


- From there you will get a pop-up to log in which will be using the Jane Admin account

<br>

<img width="304" alt="Screenshot 2025-01-16 at 4 34 18 PM" src="https://github.com/user-attachments/assets/4d6b4d58-6662-4618-b57f-291972e48dea" />

<br>

<img width="354" alt="Screenshot 2025-01-16 at 4 34 27 PM" src="https://github.com/user-attachments/assets/8e9bceb7-b05d-4f75-bdbb-b8899517ab7f" />



- Once you receive this pop-up click Ok -> Ok -> Close -> Restart Now
  

- When it comes back up it will be a member of the Domain

<br>

<img width="536" alt="Screenshot 2025-01-16 at 4 49 06 PM" src="https://github.com/user-attachments/assets/838d6ca8-59a7-43d9-a119-31c4fa98a0c5" />



- Go back into DC-1 and go back into the Active Directory Users and Computers

- Expand "mydomain.com" -> Click "Computers" and Client 1 will be located in there

<br>

<img width="339" alt="Screenshot 2025-01-18 at 3 05 08 PM" src="https://github.com/user-attachments/assets/4f893073-5a45-4bae-ac6c-c1555f09c68d" />

<br>

<img width="306" alt="Screenshot 2025-01-18 at 3 04 58 PM" src="https://github.com/user-attachments/assets/b436fad4-b20f-4182-b0e0-f73acdf6db0a" />

<br>

<img width="399" alt="Screenshot 2025-01-18 at 3 04 20 PM" src="https://github.com/user-attachments/assets/69b53207-30ab-4280-ac10-02d697ad5a9a" />




- Once you click on Client 1 you can check out things like its Operating System, Member of and etc

<br>

<img width="754" alt="17" src="https://github.com/user-attachments/assets/25b81eb4-8a99-4c4c-a4ab-13155bcceb60" />


- To keep everything more organized I'll make a new organizational unit called _CLIENTS to do this like before, Right-click mydomain.com-> New -> Organizational Unit

<br>

<img width="208" alt="Screenshot 2025-01-18 at 3 23 14 PM" src="https://github.com/user-attachments/assets/2b3a0e2a-4032-4e26-8f07-34ddc49ca095" />

<br>

<img width="148" alt="Screenshot 2025-01-18 at 3 23 25 PM" src="https://github.com/user-attachments/assets/8fa000ea-2259-49fe-8d5e-088db3554f26" />

<br>


- Then back in the Computers Unit you wanna drag Client-1 and put that in _CLIENTS then refresh to make the list updated

<br>



<h3>&#9316; Setup Remote Desktop for non-administrative users </h3>

<img width="257" alt="Screenshot 2025-03-01 at 3 20 01 PM" src="https://github.com/user-attachments/assets/c8ef0476-e323-4566-a949-5336aec84f6f" />


<br>


- Log back into Client-1 using "jane_admin" credentials

<br>

<img width="144" alt="Screenshot 2025-01-18 at 5 38 24 PM" src="https://github.com/user-attachments/assets/05f6cb92-8e60-4e1d-9d52-eb7135a0cca6" />

<br>

<img width="285" alt="Screenshot 2025-01-18 at 5 39 11 PM" src="https://github.com/user-attachments/assets/6ea5a5ef-78c9-4f24-bf79-5f40e7e8043d" />

<br>

<img width="208" alt="Screenshot 2025-01-18 at 5 42 42 PM" src="https://github.com/user-attachments/assets/ba17a924-ae33-4621-9a35-98edb5e773e6" />

<br>



- Right Click start menu -> Click "System" -> Click "Remote Desktop" -> Under "User Accounts" Click “Select users that can remotely access this PC” -> Click "Add"


<br>

<img width="350" src="https://imgur.com/R2sxVPR.png">



- The computer can now access the context of mydomain.com


- Type in "domain users" -> Click "Check Names" Click OK then Ok again

- By doing this all user accounts are automatically assigned to this group by default, granting them permission to log into the computer.

<br>

<img width="375" alt="34" src="https://github.com/user-attachments/assets/e66c1e96-d71c-4d94-9953-2ff9913c5e21" />


- This allows normal users to log in to Client-1

<br>

<h3>&#9317; Create a bunch of additional users and attempt to log into client-1 with one of the users </h3>


<br>

- First Log into DC-1
<br>
  
<img width="230" alt="Screenshot 2025-01-19 at 6 05 00 PM" src="https://github.com/user-attachments/assets/5efb44a0-419f-4bd2-9c4f-ad79b6ca5da6" />

- Type in "Windows PowerShell" in the start menu -> Right-click on the "ISE" version -> Click "Run as administrator"

<br>

<img width="1468" alt="39" src="https://github.com/user-attachments/assets/805c4d54-ebf8-40a5-bb1f-2b1d125786b0" />

- link <https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1/>
  
- Open up, copy, and paste the script that is provided to you

<br>

<img width="42" alt="Screenshot 2025-01-19 at 6 13 44 PM" src="https://github.com/user-attachments/assets/6df065cc-b3bb-458b-9781-1aab73418dbf" />

- At the top of Powershell click on New Script

- Save it, for me I named it create-users

<img width="153" alt="Screenshot 2025-01-19 at 6 20 16 PM" src="https://github.com/user-attachments/assets/20a7030b-01e4-4a07-86c7-008207837f3b" />

<br>


- The script relies on this piece because our organizational Unit in Active Directory Users and Computers is _EMPLOYEES

- The script just creates 1000 Users for us with random names

- Click "Run Script"
<br>

<img width="279" alt="Screenshot 2025-01-19 at 6 29 16 PM" src="https://github.com/user-attachments/assets/cbd4d497-637c-4a3d-b138-d03a5fb2ba50" />

- All of the Users will have the same password for instance mine is "Password 1"


<br>


<img width="355" alt="Screenshot 2025-01-19 at 6 40 18 PM" src="https://github.com/user-attachments/assets/4bf76cb1-9c8e-48d9-a26a-8ebf82a89568" />

- Back in the Active Directory Users and Computers you can see the employees being created

- If not "Right Click" on the "EMPLOYEES" folder --> Click Refresh

<br>

<img width="299" alt="65" src="https://github.com/user-attachments/assets/b7d0cc0c-c840-4886-b065-8f3c12e69130" />

(pic 09:53)

- This is what I chose

- Pick any random name you want and logout of Client-1 A.K.A Jane Doe and log in with the new user name

- When logging back into Client-1 Username is "mydomain.com\ "new user" plus the password is "Password1" with a capital P and try logging in now.
<br>

(pic 10:53)

- When you double-click on your selected user -> Click "Member of:"

- Default they will be listed under Domain Users; we allowed domain users to log into Client-1 using remote desktop

<br>

<h3>&#9318; Unlock Accounts, Reset Passwords, Enable & Disable Accounts, Finally Observe Logs  </h3>

<br>

<h4>- Configure Group Policy to lockout the account after 5 attempts</h4>

<br>

(pic 11:30)

- At the start menu type in cmd to bring up "Command Prompt"

<br>

(pic 11:37)

- You can see at the top once you're logged in a local profile

- Click on File Explorer -> Click This PC -> Click Windows (C:) -> Users

<br>

(pic 11:57)

- You will see in that folder the profile of the created user you chose from the script since we logged in with that profile along with others we logged into like jane_admin, and labuser

- The Script will keep going until it creates 10,000 users

<br>

(pic 3:31)

- First, pick any easy name from the _EMPLOYEES folder remember the password is "Password1" and open up the remote desktop application 

- Get and copy Client-1's public IP address from Azure

(pic 4:17)

- Connect to Client-1 with the random name you selected, going in this order Username: mydomain\ "random name" for the password put in any non-correct password a couple of times

- The account will then be locked out when you try to sign in

- *However if you logged in and you were able to get in with no problem after putting the wrong password in a couple of times then you probably don't have an account lockout policy set in Active Directory

  (pic 7:30)
  
- We will open up Group Policy Management on the Domain Controller, right-click the Start menu hit run then type gpmc.msc -> click enter

  (pic 7:42)

- This is the Group Policy Management Console

<br>


 (pic 8:23)
 
- Within that, there should be a Group Policy Object named "Default Domain Policy"

- Right Click on it -> Press Edit


<br>
  (pic 8:54)

- Next, we will be navigating to the account Lockout Policy settings

- Go to Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy

<br>

(10:05)

- Click on Lockout duration -> Set the timer for 30 minutes

<br>

(pic 10:34)

- Account Lockout Threshold A.K.A how many times you can attempt to log in before it gets locked out

- Set it to 5 attempts

- Keep "Reset account lockout counter after" to 5 minutes so if you fail once you have 4 more attempts but if you fail once and wait 10 minutes you still have 5 attempts

<br>

- Log back into client-1 this time with jane_admin and the password you wrote

<br>

(pic 12:54)

- After logging in we will be forcing the computer to accept the new policy

- Open up the "Command Prompt"

- Type in "gpupdate /force" and the policy should update and be reflected

- Now if someone fails a login over 5 times it should lock out their account

<br>

(pic 14:33)

- Re-open the command prompt but this time click on run as an Administrator so that we can see if the policy was applied

- Type in "gpresult /r" under "Computer settings" and see the last time the policy was applied

(pic 15:42)

- Now try to log into client-1 with your selected random name and type in the password wrong over 5 times

<br>

(pic 16:14)

- Now go back into the Domain Controller -> Right Click "mydomain.com" -> Click "Find" -> and search for that randomly named account you selected

- Double Click the account -> Click "Account" -> Check mark "Unlock Account" -> Press Apply

- Then re-attempt to log back into the account but with the right password this time

<br>

<h4>-Resetting Passwords </h4>

<br>

- Now we will be Resetting the password

- Go back to DC-1

(pic 18:36)

- Navigate to your chosen random name -> Right Click it -> Click "reset password" -> Check mark "Unlock the user's account" if needed, Now you can make the password into anything you want

<br>

<h4>-Disabling and Enabling Accounts </h4>

<br>

(pic 19:40)

- Navigate back to your chosen random name -> Right Click it -> Click "Disable Account"

- Logout of Client-1

(pic 20:23)

- Try to log back in and it should be disabled

<br>
(pic 20:44)

- Now Right Click the user and click on "Enable Account" which should re-enable the user
<br>

<h4>-Observing Logs </h4>

<br>

(pic 21:41)

- For this one go back into DC-1 -> Click start -> Type in "eventvwr.msc"

- This is the event bureau to see all the authentication logs


<br>

(pic 21:44)

- Press the arrow on the left of Windows Logs to expand it -> Click on "Security" -> Right-click on "Security" -> Select "Find" -> Type in your chosen random name -> press "Find Next"

- From here you can see the actions of the account and when you log out of it

<br>
(pic 24:00)

- Since in this account you are not an admin to see when the failures took place you will run the event viewer as an administrator

- Type back in the start menu "eventvwr.msc" -> Press run as administrator -> Type in the username and password for Jane

<br>

(pic 24:21)

- Now when it loads up expand "Windows Logs" again -> Click "Security"

- From here then you will see all the failures,  They will be stated as "Audit Failures"

<br>


(pic 24:50)

- When you pan to the right, you'll notice the "Event ID" and "Task Category," which detail the exact times of login failures.

- It will also display the successful logins, along with the corresponding IP addresses.

<br>


<h2> Final Thoughts </h2>

<p>
We've successfully completed the Active Directory Deployment and Configuration phase. By configuring Active Directory on the Domain Controller, we established our infrastructure, created a forest and administrator account, and integrated Client-1 into the domain. </p>







