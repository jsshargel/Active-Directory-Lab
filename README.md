# Active-Directory-Lab
- The goal of this tutorial is to gain hands-on experience in setting up and managing Active Directory in a virtualized environment. During the tutorial, we will explore many other important topics such as system administration, network configuration, server setup, domain controller configuration, and user account management.
- I learned how to build this lab from Josh Madakor.
- You can check out his GitHub at https://github.com/joshmadakor1 or his YouTube channel at https://www.youtube.com/c/JoshMadakor.
# Technologies and Tools Used
- Virtualization: VirtualBox
- Automation and Scripting: PowerShell
- Network Services: DNS, DHCP, and NAT
- Server Roles: Active Directory Domain Services and Remote Access Server
- Operating Systems: Windows 10 and Windows Server 2019
# Skills and Lessons Learned
- This lab taught me a ton of hands-on practical skills. I now have some familiarity with setting up and configuring Active Directory Domain Services. I learned how to set up a domain controller, manage user accounts, and configure network services like DNS and DHCP. It was awesome to gain a basic understanding of how networking works in a corporate environment.   
# Visualized Overview
![Screenshot 2024-09-03 120540](https://github.com/user-attachments/assets/3ebcccbf-7131-45c0-8549-0570320b5632)
Source: https://www.youtube.com/watch?v=MHsI8hJmggI&t=2049s
# Configuration Steps
- The first step is to download VirtualBox along with the extension pack.
  
<img src="https://github.com/user-attachments/assets/7fc0fc73-0eb5-4858-a631-55b1c4cbee2d" alt="VirtualBox Download" width="600" style="float: left; margin-right: 10px;">

# 
- Next, we need to download a Windows 10 ISO and a Windows Server 2019 ISO.

<img src="https://github.com/user-attachments/assets/c5679b4d-10c1-4a6f-9c4c-de364d661228" alt="Windows 10 ISO" width="600" style="float: left; margin-right: 10px;">

# 

<img src="https://github.com/user-attachments/assets/f656316e-bd33-4764-89f0-59756805c959" alt="Windows Server 2019 ISO" width="600" style="float: left; margin-right: 10px;">

#
- Next, we will set up a virtual machine, which will serve as our domain controller.
- I went ahead and set the machine to have 2GB of RAM, 4 processors, and enabled bidirectional drag-and-drop features. 
- Since this is the domain controller, we need two NICs, so we also need to make sure to enable a second network adapter.
- NIC 1 is going to be running NAT and is for the domain controller to access the internet through my home internet.
- NIC 2 is for an internal network and is used to create a closed network environment in which the domain controller can manage clients without exposure to the external internet.

<img src="https://github.com/user-attachments/assets/e4da3d89-ed9a-4a0d-802f-f8fc45885b51" alt="Virtual Machine Settings" width="600" style="float: left; margin-right: 10px;">


#
- Next, we need to mount the Windows Server ISO.


<img src="https://github.com/user-attachments/assets/88edf879-a999-4613-a5a2-b385c1d976b1" alt="Mount Windows Server 2019 ISO" width="600" style="float: left; margin-right: 10px;">

#

- Next, to create a smoother experience, we will install guest additions. 

<img src="https://github.com/user-attachments/assets/910dca2d-0499-49e6-8d3b-3b8155c36493" alt="Installing Guest Additions" width="600" style="float: left; margin-right: 10px;">

<img src="https://github.com/user-attachments/assets/c95c6b31-42ff-46b0-9e2b-6f00cbba10b1" alt="Installing Guest Additions" width="600" style="float: left; margin-right: 10px;">

# 
- Next, we are going to set up IP addressing for the internal NIC.
- We do not have to worry about other NIC because it will automatically get an IP address from the home router.
- Let's head on over to network settings to identify the different network connections.
- Below, we can see that the first connection has an IP address that can be associated with a home network, so we will rename them accordingly.  
![Screenshot 2024-08-28 114717](https://github.com/user-attachments/assets/65ec44fb-4126-4d6f-baf9-7fbf603f0e06)

#
- Now we can set up the IP addressing.
- For the IP address, we will use 172.16.0.1
- For the Subnet Mask, we will use 255.255.255.0
- We will leave the Default Gateway blank because the domain controller itself will serve as the default gateway.
- For the DNS server address, we will use 127.0.0.1, which is a loopback address since the DNS server will automatically be installed when active directory is.  
![Screenshot 2024-08-29 114030](https://github.com/user-attachments/assets/69e7c4d8-c90c-4c5c-9723-0b959e3db011)

#
- Next, we will rename the PC to be something other than a random name.
- We'll name it DC for the domain controller and then restart the machine. 
<img src="https://github.com/user-attachments/assets/6a6933ce-dd78-442e-bd6b-a8849bcc7eda" alt="Renaming PC" width="600" style="float: left; margin-right: 10px;">

#

- Next, we are going to install active directory domain services to add a domain. 
- To do this, we will head over to the dashboard and click on "Add roles and features."
- The installation type is role-based or feature-based.
- Select the server we want to use.
- Under server roles, we will select "Active Directory Domain Services" and add the features.
- Then we will continue past Features, AD DS, and go ahead and install.
<img src="https://github.com/user-attachments/assets/f3f9334e-125c-4ba9-965a-f8c17188658f" alt="" width="600" style="float: left; margin-right: 10px;">

#

- Now we need to create the domain from the software we just installed.
- To do this, we head over to the flag icon in the server manager.
- Next, we want to click "Promote this server to a domain controller."
- For the deployment configuration, select "Add a new forest" and then name the root domain name. We will use mydomain.com.
- Now, we will create a password for DSRM.
- After this, we will continue through the different options until we are able to install.
- After it is finished installing, the machine will automatically restart.
  
![Screenshot 2024-08-29 121905](https://github.com/user-attachments/assets/d67f524a-a7a3-4683-ade6-8e7005772bd3)

#

- Next, we will log in using the built-in admin account.
  
<img src="https://github.com/user-attachments/assets/753aaa79-9c2a-4d17-b116-512b87f5f361" alt="" width="600" style="float: left; margin-right: 10px;">


#

- Once logged in, we will create our own dedicated admin account instead of using the built-in admin account.
- To do this, we will open the Start Menu, and go to "Windows Administrative Tools" and open "Active Directory Users and Computers."
- Once open, we can see our newly created domain. We right-click mydomain.com and hover over "New" to create an Organizational Unit.
- We will name it _ADMINS. Make sure to uncheck the option to protect the container from accidental deletion, as it will be annoying when trying to delete it later.
<img src="https://github.com/user-attachments/assets/cea4450b-8740-4f13-8e1c-f6ffb2d5f2d3" alt="" width="600" style="float: left; margin-right: 10px;">

#

- Once created, we can create a new user following the same steps but under the newly created _ADMINS organizational unit.
- We can now set up our name and the user logon name. I am going to use a-jshargel
- Next, we can create a password. Make sure to uncheck "user must change password at next logon" and check "password never expires" for convenience because this is just a lab environment. 
<img src="https://github.com/user-attachments/assets/7994c23c-d047-4f2b-8b7e-db62b404b115" alt="" width="600" style="float: left; margin-right: 10px;">

#

- Now, to make it a domain admin, we need to right-click it and go to properties.
- Next, we will find "Member Of" and click add.
- Under the object names to select, we will type "domain admins."
- Now click on "Check Names," and we can see that it resolves to "Domain Admins."
- Now we can click apply and then ok.
- Now we have our domain admin account!
<img src="https://github.com/user-attachments/assets/a2fb0b06-00fc-4c1f-af9e-d1cb9813903e" alt="" width="600" style="float: left; margin-right: 10px;">

#

- Now, we can log into our domain admin account.
- First, we will log out and return to the login screen.
- Once there, we can go over to "other user" and log in using the credentials we just created
<img src="https://github.com/user-attachments/assets/38bb152e-12ed-4605-8b4f-1efc2a48d6b6" alt="" width="600" style="float: left; margin-right: 10px;">

#

- The next step is to install RAS (remote access server) and NAT (network address translation) on the domain controller. 
- We need to do this so that the Windows 10 clients can be on a private virtual network but still access the Internet through the domain controller.
- We need to head over to roles and features in the server manager dashboard.
- This process will be similar to when we installed active directory domain services.
- We select the installation type, which is once again role or feature-based.
- Next, we select the server.
- After that, we will select "Remote Access."
- We will continue forward until we reach role services. Here, we will select routing and then add features. We can see that DirectAccess and VPN (RAS) have also been checked automatically.
- Now, we will continue until we can install the role.
<img src="https://github.com/user-attachments/assets/82a0f1e4-2ba8-4666-a72b-c72adc0ad46d" alt="" width="600" style="float: left; margin-right: 10px;">

#

- After we have installed the role, we need to configure and enable routing and remote access.
- To do this, we go to the tools section at the top of the server manager and select "Routing and Remote Access."
- Now we right-click on the DC and select "Configure and Enable Routing and Remote Access."
- Then we select NAT.
- Since we previously renamed our NICs, we can see which public interface we need to select to connect to the Internet.
- We will choose the interface we named “Internet” and finish with that.
- We can now see that it is configured!
<img src="https://github.com/user-attachments/assets/029a33b8-de42-4066-ac67-336afdae057f" alt="" width="600" style="float: left; margin-right: 10px;">

#

- The next thing we will do is set up a DHCP server on our domain controller.
- This will allow our Windows 10 clients to get an IP address that will allow them to access the internet.
- We are going to head back over to "Add roles and features" in the server manager.
- We will go through the same process as before to add the DHCP role.
<img src="https://github.com/user-attachments/assets/26617980-8129-404f-a062-c4f949fbcf51" alt="" width="600" style="float: left; margin-right: 10px;">

#

- Now we will head over to tools and select "DHCP" to set up our scope.
- Once set up, this will allow the client computers on the network to automatically get an IP address in the range we configure.
- Let's start by right-clicking IPv4 and selecting "New Scope."
- Since this is just a lab, we can go ahead and name the scope our IP range, which is “172.16.0.100-200.”
- The start address would be 172.16.0.100 and the end address 172.16.0.200.
- The Subnet mask is 255.255.255.0 and the length is 24.
- We don't have any exclusions.
- The lease time we can set at 8 days since this is a home lab.
- Now, we want to configure the clients' DHCP options. This will tell the clients which server to use for various purposes.
- Since we configured NAT on the domain controller and it has routing configured as well, we want to point the clients to the domain controller's internal NIC so they can access the Internet.
- For the Router (Default Gateway), we will use the domain controller's IP address, which is 172.16.0.1. Make sure to add the address.
- Since we automatically installed DNS on the domain controller when we installed the active directory, we will use the domain controller as our DNS server.
- We can skip over the WINS Server because we will not be using this.
- Next, we can complete the setup.
- After this, we need to authorize and refresh the DHCP server.
- Afterwards, we can see that this worked!
<img src="https://github.com/user-attachments/assets/1878ab40-7434-4e13-9bca-b7ce41e956fd" alt="" width="600" style="float: left; margin-right: 10px;">

#

- The next thing we are going to be doing is running a PowerShell script to create a bunch of users.
- I am using the same script Josh Madakor provides in his tutorial.
- You can find the script on his YouTube channel provided at the beginning of this walkthrough.
- Once we have the file downloaded and saved on the desktop, we can extract the contents.
- In the names file I am going to add my name. 
- Now we'll click on Start, open the Windows PowerShell drop-down menu, and run WPS ISE as administrator.  
- Now, we can open the PowerShell script saved in the folder on our desktop. 
- If we try to run the script as is, we get an error. This is a security feature, but we need to get around this.
- To do that we enter the command - Set-ExecutionPolicy Unrestricted.
- After this, we will change directories to the AD_PS-Master folder using the cd command.
- Once there, we can search the content using the ls command, and we can see that the name.txt file is there.
<img src="https://github.com/user-attachments/assets/251c0517-2203-4971-a2f6-47af6f882aab" alt="" width="600" style="float: left; margin-right: 10px;">

#

- Alright! Now we can go ahead and run the script.
- After we run the script, we can head over to tools and open Active Directory Users and Computers.
- Once there, we can see that the Users have been created using the script we just ran. 
<img src="https://github.com/user-attachments/assets/8110df2c-c0a4-44f5-bc13-cc87a6702071" alt="" width="600" style="float: left; margin-right: 10px;">

#

- Now, we will create the Windows 10 client.
- To do that we can head back over to Virtual Box and create a new VM.
- Let's name it Client1 and select Windows 10 64 Bit.
- I'm going to give it the same settings as the server, except I'll increase the RAM on this one to 4GB. 
- Also, under network, we need to select Internal Network.
<img src="https://github.com/user-attachments/assets/2f8e9bfa-c890-4ce2-accd-de8b9e8c9981" alt="" width="600" style="float: left; margin-right: 10px;">

#

- Ok, now we can find and mount the Windows ISO we downloaded earlier.
- When the setup asks for a Product Key, we can just bypass it by selecting that we don't have one.
- We also need to make sure to select Windows 10 Pro because the Home edition cannot join the domain.
- Now we select custom install and go ahead and install.
- Once it is finished installing, it will restart on its own.
- Once we get to the option to select which type of account this will be, we select a personal account.
- On the next page, we want to make sure to select the offline account and then limited experience. 
- Let's set the username to "user" and skip over the password.
- Let's skip over everything else.
- Now that we are finished with that, let's make sure that the internet is working on the Windows 10 VM.
- To do that we can open the command line and run ipconfig.
- Success!
<img src="https://github.com/user-attachments/assets/e0777a99-b493-4cb2-b696-51d7e733e772" alt="" width="600" style="float: left; margin-right: 10px;">

#

- To test if everything is working, we can ping Google.
- Because www.google.com resolved, we know that the DNS server is working, and because we can ping to the internet, we know that everything is working correctly. 
<img src="https://github.com/user-attachments/assets/54c0031a-c609-40a7-9ee3-54c9e3f9263e" alt="" width="600" style="float: left; margin-right: 10px;">

#

- Now let's go ahead and rename the PC and join the domain at the same time.
- To do this, we right-click the start menu and select system.
- Once there, we scroll down until we find the option to Rename the PC (Advanced).
- Now we can select "Change" and rename it to CLIENT1.
- On the change the option from workgroup to domain and enter our domain which is mydomain.com.
- Now, we need to enter a username and password that has permission to join the domain.
- I am going to enter the admin account that I created before.
- Then we can go ahead and restart.
<img src="https://github.com/user-attachments/assets/b6d60a84-9c13-4220-bf92-77aa89e43d32" alt="" width="600" style="float: left; margin-right: 10px;">

#

- Let's explore some things now that the client is up and running.
- Let's log into the domain controller using the admin account. 
- Once we are logged in, let's head over to the tools and open the DHCP.
- If we go back to the scope we created and open “Address Leases,” we can see that there is a lease from the client VM that we just created!
- This is where all the leases will appear when a client connects to the network.
![Screenshot 2024-09-03 114531](https://github.com/user-attachments/assets/fc2f3148-f8d4-45f3-8d32-8eb4c0794153)

#

- Ok, let's head to "Active Directory Users and Computers."
- Once there we can click on computers and see that our CLIENT1 is connected to the domain. 
- Since this is connected to the domain, we can log onto that computer using any of the accounts that we created before.
- Also note that we can delete CLIENT1 from the domain controller, and then none of those accounts will be able to log in anymore.
<img src="https://github.com/user-attachments/assets/74d2b3da-31dc-4ff3-b65b-bc9d226d412a" alt="" width="600" style="float: left; margin-right: 10px;">

#

- Let's head back over to the Windows 10 VM and sign in using one of the users we created with the script. 
- I entered my name into the list, so I am going to log in using that. 
<img src="https://github.com/user-attachments/assets/7e3f1e2c-f33b-49f2-9b4c-cb243d78baba" alt="" width="600" style="float: left; margin-right: 10px;">

#

- Once we are logged in let's head over to the command line to verify everything.
- We can enter the command "whoami" and see that we are logged into mydomain using the username jshargel!
- Success!
<img src="https://github.com/user-attachments/assets/127677e8-fb62-43bb-9b4a-0d686010e359" alt="" width="600" style="float: left; margin-right: 10px;">













