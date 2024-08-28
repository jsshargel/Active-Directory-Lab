# Active-Directory-Lab
- This tutorial outlines how to set up a lab running active directory. 
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
<img src="https://github.com/user-attachments/assets/5142fc8c-341d-49e1-9b7f-ea3d5a48f214" alt="Identifying Network Connections" width="600" style="float: left; margin-right: 10px;">

#
- Now we can set up the IP addressing.

#
- Next, we are going to rename the PC to be something other than a random name.
- We'll name it DC for domain controller and then restart the machine. 
![Screenshot 2024-08-28 120620](https://github.com/user-attachments/assets/6a6933ce-dd78-442e-bd6b-a8849bcc7eda)

#







  
