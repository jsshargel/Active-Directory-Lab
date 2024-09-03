# Active-Directory-Lab
- This tutorial outlines how to set up a lab running active directory.
- I learned how to build this lab from Josh Madakor.
- You can check out his github at https://github.com/joshmadakor1 or his youtube channel at https://www.youtube.com/c/JoshMadakor
# Technologies Used
- VirtualBox
- Powershell
# Operating Systems Used
- Windows 10
- Server 2019
# Configuration Steps
- The first step is to download VirtualBox along with the extension pack.
  
<img src="https://github.com/user-attachments/assets/7fc0fc73-0eb5-4858-a631-55b1c4cbee2d" alt="VirtualBox Download" width="600" style="float: left; margin-right: 10px;">

# 
- Next, we need to download a Windows 10 ISO and a Windows Server 2019 ISO

<img src="https://github.com/user-attachments/assets/c5679b4d-10c1-4a6f-9c4c-de364d661228" alt="Windows 10 ISO" width="600" style="float: left; margin-right: 10px;">

# 

<img src="https://github.com/user-attachments/assets/f656316e-bd33-4764-89f0-59756805c959" alt="Windows Server 2019 ISO" width="600" style="float: left; margin-right: 10px;">

#
- Next, we are going to set up a virtual machine. This will serve as our domain controller. 
- I went ahead and set the machine to have 2GB of RAM, 4 processors, and enabled bidirectional drag and drop features. 
- Since this is the domain controller, we need two NICs, so we also need to make sure to enable a second network adapter.
- NIC 1 is going to be running NAT and is for the domain controller to access the internet through my home internet.
- NIC 2 is for an internal network and is used to create a closed network environment in which the domain controller can manage clients without exposure to the external internet.

<img src="https://github.com/user-attachments/assets/e4da3d89-ed9a-4a0d-802f-f8fc45885b51" alt="Virtual Machine Settings" width="600" style="float: left; margin-right: 10px;">


#
- Next, we need to mount the Windows Server ISO.


<img src="https://github.com/user-attachments/assets/88edf879-a999-4613-a5a2-b385c1d976b1" alt="Mount Windows Server 2019 ISO" width="600" style="float: left; margin-right: 10px;">

#

- Next, to create a smoother experience we are going to install guest additions. 

<img src="https://github.com/user-attachments/assets/910dca2d-0499-49e6-8d3b-3b8155c36493" alt="Installing Guest Additions" width="600" style="float: left; margin-right: 10px;">

<img src="https://github.com/user-attachments/assets/c95c6b31-42ff-46b0-9e2b-6f00cbba10b1" alt="Installing Guest Additions" width="600" style="float: left; margin-right: 10px;">

# 
- Next, we are going to set up IP addressing for the internal NIC.
- We do not have to worry about other NIC because it will automatically get an IP adress from the home router.
- Let's head on over to network settings to identify the different network connections.
- Below we can see that the first connection has an IP address that can be associated with a home network, so we will rename them accordingly.  
![Screenshot 2024-08-28 114717](https://github.com/user-attachments/assets/65ec44fb-4126-4d6f-baf9-7fbf603f0e06)

#
- Now we can set up the IP addressing.
- For the IP address we will use 172.16.0.1
- For the Subnet mask we will use 255.255.255.0
- For the Default gateway we will leave it blank because the domain controller itself will serve as the default gateway.
- For the DNS server address we will use 127.0.0.1 which is a loopback address since the dns server will automatically be installed active directory is installed.  
![Screenshot 2024-08-29 114030](https://github.com/user-attachments/assets/69e7c4d8-c90c-4c5c-9723-0b959e3db011)

#
- Next, we are going to rename the PC to be something other than a random name.
- We'll name it DC for domain controller and then restart the machine. 
<img src="https://github.com/user-attachments/assets/6a6933ce-dd78-442e-bd6b-a8849bcc7eda" alt="Renaming PC" width="600" style="float: left; margin-right: 10px;">

#

- Next, we are going to install active directory domain services to add a domain. 
- To do this we will head over to the dashboard and click on "Add roles and features"
- The installagtion type is role-based or feature-based.
- Select the server we want to use.
- Under server roles we will select "Active Directory Domain Services" and add the features.
- Then we will continue passed Features, AD DS, and go ahead and Install.
<img src="https://github.com/user-attachments/assets/f3f9334e-125c-4ba9-965a-f8c17188658f" alt="" width="600" style="float: left; margin-right: 10px;">

#

- Now we need to create the domain from the sofware we just installed.
- To do this we head over to the flag icon in the server manager.
- Next, we want to click "Promote this server to a domain controller"
- For the deployment configuration we want to select "Add a new forest" and then name the Root domain name. We will use mydomain.com
- Now we will create a password for DSRM.
- After this we will continue through the different options until we are able to install.
- After it is finished installing the machine will automatically restart
  
![Screenshot 2024-08-29 121905](https://github.com/user-attachments/assets/d67f524a-a7a3-4683-ade6-8e7005772bd3)

#

- Next, we will login using the built in admin account.
  
<img src="https://github.com/user-attachments/assets/753aaa79-9c2a-4d17-b116-512b87f5f361" alt="" width="600" style="float: left; margin-right: 10px;">


#

- Once logged in we will create our own dedicated admin account instead of using the built in admin account.
- To do this we will open the start menu and go to "Windows Administrative Tools and open "Active Directory Users and Computers."
- Once open we can see our newly created domain. We right click mydomain.com and hover over "New" to create an Orgaizational Unit.
- We will name it _ADMINS. Make sure to uncheck the option that says to protect container form accidental deletion because it will be annoying when trying to delete later.
<img src="https://github.com/user-attachments/assets/cea4450b-8740-4f13-8e1c-f6ffb2d5f2d3" alt="" width="600" style="float: left; margin-right: 10px;">

#

- Once created we can create a new user following the same steps but under the newley created _ADMINS organizational unit.
- We can now set up our name and the user logon name. I am going to use a-jshargel
- Next, we can create a password. Make sure to uncehck "user much change password at next logon" and also check "password never expires" for convenience and because this is just a lab environment. 
<img src="https://github.com/user-attachments/assets/7994c23c-d047-4f2b-8b7e-db62b404b115" alt="" width="600" style="float: left; margin-right: 10px;">

#

- Now to make it a domain admin we need to right click it and go to properties.
- Next. we will find "Member Of" and then click add.
- Under the object names to select we will type "domain admins."
- Now click on "Check Names" and we can see that it resolves to "Domain Admins."
- Now we can click apply and then ok.
- Now we have our domain admin account!
<img src="https://github.com/user-attachments/assets/a2fb0b06-00fc-4c1f-af9e-d1cb9813903e" alt="" width="600" style="float: left; margin-right: 10px;">

#

- Now we can log into our own domain admin account.
- First we will log out and go back to the log in screen.
- Once there we can go over to "other user" and log in using the credentials we just created
<img src="https://github.com/user-attachments/assets/38bb152e-12ed-4605-8b4f-1efc2a48d6b6" alt="" width="600" style="float: left; margin-right: 10px;">

#

- The next thing we will do is install RAS (remote access server) and NAT (network address translation) on the domain controller. 
- The reason we need to do this is so that the windows 10 clients can be on a private virutal network but still be able to access the interent through the domain controller.
- We need to head on over to roles and features in the server manager dashboard.
- This will be a similar process as before when we installed active directory domain services.
- We select the installation type which is once again role or feature based.
- Next, we select the server.
- After that we will select "Remote Access."
- We will continue foward until we are at role services. Here we will select routing and then add features. We can see that the DirectAccess and VPN (RAS) has also been checked automatically.
- Now we will continue foward until we are able to install the role. 
<img src="https://github.com/user-attachments/assets/82a0f1e4-2ba8-4666-a72b-c72adc0ad46d" alt="" width="600" style="float: left; margin-right: 10px;">

#

- After we have installed the role we need to configure and enable routing and remote access.
- To do this, we head over to tools at the top of the server manager and select "Routing and Remote Access."
- Now we right click on the DC and select "Configure and Enable Routing and Remote Access."
- Then we select NAT.
- Since we previously renamed our NICs we are able to see which public interface we need to select to connect to the internet.
- We will choose the interface that we named internet and then finish up with that.
- We can now see that it is configured!
<img src="https://github.com/user-attachments/assets/029a33b8-de42-4066-ac67-336afdae057f" alt="" width="600" style="float: left; margin-right: 10px;">

#

- The next thing we will do is set up a DHCP server on our domain controller.
- This will allow our windows 10 clients to get an IP address that will allow them to access the internet.
- We are going to head back over to "Add roles and features" in the server manager.
- We will go through the same process as before to add the DHCP role.
<img src="https://github.com/user-attachments/assets/26617980-8129-404f-a062-c4f949fbcf51" alt="" width="600" style="float: left; margin-right: 10px;">

#

- Now we will head over to tools and select "DHCP" to set up our scope.
- Once set up this will allow the client computers on the network to automatically get an IP address in the range that we configure.
- Let's start by right clicking IPv4 and selecting "New Scope."
- Since this is just a lab we can go ahead and name the scope what our IP range will be which is 172.16.0.100-200
- The start address would be 172.16.0.100 and the end address 172.16.0.200.
- The Subnet mask is 255.255.255.0 and the length is 24.
- We don't have any exclusions.
- The lease time we can set at 8 days since this is a home lab.
- Now we want to configure DHCP options for the clients.This will tell the clients which server to use for various things.
- Since we configured NAT on the domain controller and it has routing configured as well we want to point the clients to the internal NIC of the domain controller so they can access the internet.
- For the Router (Default Gateway) we will use the domain controllers IP address which is 172.16.0.1. Make sure to add the address.
- Since we automatically installed DNS on the domain controller when we installed active directory we will use the domain contoller as our DNS server.
- We can skip over the WINS Server because we will not be using this.
- Next, we can complete the setup.
- After this we need to authorize and refresh the DHCP server.
- Afterwards we can see that this worked!
<img src="https://github.com/user-attachments/assets/1878ab40-7434-4e13-9bca-b7ce41e956fd" alt="" width="600" style="float: left; margin-right: 10px;">

#

- The next thing we are going to be doing is running a powershell script to create a bunch of users.
- I am using the same script that Josh Madakor provides in his tutorial.
- You can find the script on his youtube video provided at the beginning of this walkthrough.
- Once we have the file downloaded and saved on the desktop we can extract the contents.
- In the names file I am going to add my name. 
- Now we'll click on Start and open the Windows Powershell drop down menu and run WPS ISE as administrator.  
- Now we can open the Powershell script we have saved in the folder on our desktop. 
- If we try to run the script as is we get an error. This is just a security feature so we need to get around this.
- To do that we enter the command - Set-ExecutionPolicy Unrestricted.
- After this we will change directories to the AD_PS-Master folder using the cd command.
- Once there we can search the content using the ls command and we can see that the name.txt file is there.
<img src="https://github.com/user-attachments/assets/251c0517-2203-4971-a2f6-47af6f882aab" alt="" width="600" style="float: left; margin-right: 10px;">

#

- Alright! Now we can go ahead and run the script.
- After we run the script we can head over to tools and open Active Directory Users and Computers.
- Once there we can see that the Users have been created using the script we just ran. 
<img src="https://github.com/user-attachments/assets/8110df2c-c0a4-44f5-bc13-cc87a6702071" alt="" width="600" style="float: left; margin-right: 10px;">





















