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

![chrome_I5lKivZDH1](https://github.com/user-attachments/assets/7fc0fc73-0eb5-4858-a631-55b1c4cbee2d)
# 
- Next, we need to download a Windows 10 ISO and a Windows Server 2019 ISO

![chrome_dm1pkFC6TC](https://github.com/user-attachments/assets/c5679b4d-10c1-4a6f-9c4c-de364d661228)
# 
![chrome_sxMh7h1LvF](https://github.com/user-attachments/assets/f656316e-bd33-4764-89f0-59756805c959)
#
- Next, we are going to set up a virtual machine. This will serve as our domain controller. 
- I went ahead and set the machine to have 2GB of RAM, 4 processors, and enabled bidirectional drag and drop features. 
- Since this is the domain controller, we need two NICs, so we also need to make sure to enable a second network adapter.
- NIC 1 is going to be running NAT and is for the domain controller to access the internet through my home internet.
- NIC 2 is for an internal network and is used to create a closed network environment in which the domain controller can manage clients without exposure to the external internet.

![VirtualBox_kzbkJemOrD](https://github.com/user-attachments/assets/e4da3d89-ed9a-4a0d-802f-f8fc45885b51)
#
- Next, we need to mount the Windows Server ISO.


![VirtualBoxVM_iJteGHcb6z](https://github.com/user-attachments/assets/88edf879-a999-4613-a5a2-b385c1d976b1)
#

- After it is installed we will create a password for the administrator and login.
- To create a smoother experience we are going to install guest additions. 
