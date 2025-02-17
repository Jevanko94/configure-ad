# Configuring-On-premises-Active-Directory-within-Azure-VMs
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>
<p align="center">
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/7f432c24-4e30-498f-bc8d-c356b9c88f59"/>
</p>
<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create Resource Group
- Create Virtual Machine Windows Server Datacenter
- Create Virtual Machine Windows 
- Use Remote Dektop Connection to log into Cilent-1 VM
- Grab the Private IP of DC-1 to do a endless ping on Cilent-1 VM in Command Prompt
- Go to DC-1 to load wf.msc to allow the ping to occur in inbound rules
- Go to Server Manager to add roles and features
- Create a Active Directory Domain Services
- Promote the server to a domain controller and create a new forest
- Log back into DC-1 VM by using mydomian.com\labuser
- In DC-1 go to tools, and go to Active Directory Users and Computers
- Create a new organizational unit folder called _EMPLOYEES
- Create another new organizational unit folder called _ADMINS
- Create new user in ADMINS folder
- Put new user in Domain Admins then logoff of DC-1
- Log back into DC-1 under Admin account
- Go back to Cilent-1 and rename this pc under a new domain, but will recieve an error
- Copy DC-1 Privite NIC IP then paste in Cilent-1 DNS Servers
- Restart Cilent-1 VM
- Log into Cilent-1 VM using Remote Desktop Connection
- Rename this PC again in Cilent-1 VM
- Change the Domain name to user Admins
- Restart VM again
- Log into Cilent-1 VM under admin account using Remote Desktop Connection
- Use Remote Desktop to let Domain Users log into the account
- Go back to DC-1 VM and go to the Users folder to see both labuser and admin account in Domain Users
- Run Windows Powershell ISE as administrator
- Create a new file and run script for creating 2000 users
- Go to _EMPLOYEES folder and grab one's display name
- Logoff of Cilent-1 VM then log back into Cilent-1 VM under user you picked
- Logoff Cilent-1 as random user
- Grab another random user Display name
- Log back into Cilent-1 VM with new user but mistype password to get kicked out of account
- Go to DC-1 VM and manually reset the password or unlock the account

<h2>Deployment and Configuration Steps</h2>

<p>
![1](https://github.com/user-attachments/assets/6d3d8fa8-3ca5-44de-b0dd-91398af2d701)

</p>
<p>
First go to Microsoft Azure and type Resource Group 
</p>
<br />

<p>
![2](https://github.com/user-attachments/assets/86671797-6562-411a-a6b5-3ef15cf841c1)

</p>
<p>
Next click create to create the Resource Group
</p>
<br />

<p>
![3](https://github.com/user-attachments/assets/2f645a83-b705-439f-8c76-60e4779c3596)

</p>
<p>
Now for the name type AD-LAb and the region under US West US 3 then go to the review and create tab 
</p>
<br />


<p>
![4](https://github.com/user-attachments/assets/ed0e106f-4eb8-4bd7-95ab-a20477f5cf33)

</p>
<p>
Next the validation pass through 
</p>
<br />


<p>
![5](https://github.com/user-attachments/assets/645ce803-2037-430a-b1a2-7ee3aceec748)

</p>
<p>
Now once the process is done you will see the Resource Group was created 
</p>
<br />

<p>
![6](https://github.com/user-attachments/assets/dc3f53b4-e7bd-449b-8132-e17cb832a5c5)

</p>
<p>
Type Virtual Machine in the search bar 
</p>
<br />

<p>
![7](https://github.com/user-attachments/assets/1c137fb1-2bbc-40cc-a627-2a4c510dd91c)

</p>
<p>
Next click Azure Virtual Machine to create the VM
</p>
<br />

<p>
![8](https://github.com/user-attachments/assets/f5aa9736-1070-4a17-ba8b-67f0c1db7a11)

</p>
<p>
Now for the resource group click AD-LAb, and the virtual machine name type DC-1. The region put under US West US 3 and the image under Windows Server
</p>
<br />

<p>
![9](https://github.com/user-attachments/assets/1d9e5d0e-0664-4632-9c2a-b576a428f88d)

</p>
<p>
Next the size needs to be under Standard E2 and teh username under labuser and the password under your own unique password. Remember to open a notepad and type all your info out so you dont lose it.
</p>
<br />

<p>
![10](https://github.com/user-attachments/assets/224feca9-3084-47cb-b198-7a4b66ca19d8)

</p>
<p>
Next click the box in the Licensing section and then click th econfirm box. Then click review and create 
</p>
<br />

<p>
![11](https://github.com/user-attachments/assets/e70228be-4db8-42cd-afbb-d804b1c42908)

</p>
<p>
Now go to the networking tab and make sure the virtual network, subnet, and the public IP all says (new)
</p>
<br />

<p>
![12](https://github.com/user-attachments/assets/ffce0f42-378a-4fc3-9da9-f7df46003b37)

</p>
<p>
Now go to the review and create section 
</p>
<br />

<p>
![13](https://github.com/user-attachments/assets/b3451c58-138f-4a82-88df-194f048a9a79)

</p>
<p>
Next let the deployment progess load 
</p>
<br />

<p>
![14](https://github.com/user-attachments/assets/0bfb3098-09fc-4b7d-ac7f-7a23fe6e110d)

</p>
<p>
Now the process will be complete when there is a green check 
</p>
<br />

<p>
![15](https://github.com/user-attachments/assets/03f382d0-fdf6-49fe-857d-93e653b7e582)

</p>
<p>
Next type virtual machine and you will see DC-1 VM was created
</p>
<br />

<p>
![16](https://github.com/user-attachments/assets/845878dd-c00c-4d1a-a70c-b7933c32530f)

</p>
<p>
Next click create and then go to Azure Virtual Machine 
</p>
<br />

<p>
![17](https://github.com/user-attachments/assets/f46ce10c-8abe-4791-aae5-fac72af1f5ef)

</p>
<p>
Next in the subscriiption section make sure the same subscription that you used for the resource group is selected. Then in Resource Group click AD-Lab then for the name type Cilent-1 and the region click US West US 3
</p>
<br />

<p>
![18](https://github.com/user-attachments/assets/854ee9ea-0cc9-41c9-8abc-553cb256bca2)

</p>
<p>
Now for the Image click Windows 10 pro version and the size click Standard E2
</p>
<br />

<p>
![19](https://github.com/user-attachments/assets/2fa62e05-18a7-4380-896a-3796e2e65fb7)

</p>
<p>
Next for the username type labuser and the password the same as DC-1 VM. Then click the Licensing tab then click review and create 
</p>
<br />

<p>
![20](https://github.com/user-attachments/assets/8191ee53-05e4-4073-8a44-500fa9035fb3)

</p>
<p>
Now the deployment will be done when a green check appears next to the deployment
</p>
<br />

<p>
![21](https://github.com/user-attachments/assets/b1091537-8035-4e84-9acd-dc2a9fa32991)

</p>
<p>
Next type virtual machines in the search bar 
</p>
<br />

<p>
![22](https://github.com/user-attachments/assets/3c593d78-c6d9-456c-be53-10752902d0f7)

</p>
<p>
Next you will see that DC-1 and Cilent-1 was created 
</p>
<br />

<p>
![23](https://github.com/user-attachments/assets/1b20af55-bfb3-49d0-ac78-478690652d87)

</p>
<p>
Now click DC-1 and click networkng 
</p>
<br />

<p>
![24](https://github.com/user-attachments/assets/ea3c477c-5a68-4562-a31c-f37375ef353f)

</p>
<p>
Next click on the Network Interface 
</p>
<br />

<p>
![25](https://github.com/user-attachments/assets/79f4352e-4b69-43ff-8aaa-e5e060f59ed5)

</p>
<p>
Next click on IP Configurations 
</p>
<br />

<p>
![26](https://github.com/user-attachments/assets/bdbfe284-4fde-4341-a493-cae11359fe89)

</p>
<p>
Now click ipconfig1
</p>
<br />

<p>
![27](https://github.com/user-attachments/assets/9f1fde2b-8d79-4a73-9191-e11388b49202)

</p>
<p>
We are editing the IP Configurations in the allocation section click Static instead of Dynamic then click save.
</p>
<br />

<p>
![28](https://github.com/user-attachments/assets/870ab39d-a92c-4e7c-8bf1-4af137cab681)

</p>
<p>
Now we are going to log into Cilent-1 VM copy the public IP address
</p>
<br />

<p>
![29](https://github.com/user-attachments/assets/b7e51f78-f454-4a71-8343-c356c77d658e)

</p>
<p>
Next type Remote Desktop Connection and click to open the app
</p>
<br />

<p>
![30](https://github.com/user-attachments/assets/7ad80b77-0c9c-4cb3-a649-f8bd938a929c)

</p>
<p>
Next paste the IP of Cilent-1 in the computer section 
</p>
<br />

<p>
![31](https://github.com/user-attachments/assets/a8b0b90d-3af7-45c6-b990-4e617491ddcf)

</p>
<p>
![32](https://github.com/user-attachments/assets/5d74fe76-b7e0-4e46-a2fc-f7721859ec3e)

</p>
<p>
Now tpye for the username type labuser and the password type the password you made for the VM, then click ok
</p>
<br />

<p>
![33](https://github.com/user-attachments/assets/efc90686-125b-4791-8e32-96b9c5740462)

</p>
<p>
Next click yes to open the VM
</p>
<br />

<p>
![34](https://github.com/user-attachments/assets/497dcd68-b644-4ac7-a5f3-656c2329ddfb)

</p>
<p>
Now you should see the VM loading under the name labuser 
</p>
<br />

<p>
![35](https://github.com/user-attachments/assets/e95e1ae0-aa21-4861-89e7-cbc69b27df5b)

</p>
<p>
Next click no to the following image above 
</p>
<br />

<p>
![36](https://github.com/user-attachments/assets/2e454e60-1b7b-49c9-ac69-3a6453f736c5)

</p>
<p>
Once networks load click yes 
</p>
<br />

<p>
![37](https://github.com/user-attachments/assets/0aed68f3-152a-4e6c-b584-f7defc74dc35)

</p>
<p>
Now open up command prompt 
</p>
<br />

<p>
![38](https://github.com/user-attachments/assets/1b80f50c-fa21-4855-b489-9a40b5cd2307)

</p>
<p>
Next go back to Azure and copy the Private IP of DC-1
</p>
<br />

<p>
![39](https://github.com/user-attachments/assets/c62f9d72-1eff-4444-89f2-b38b430344ff)

</p>
<p>
Go back to Cilent-1 VM and type ping -t the the private IP of DC-1. We are doing a endless ping to see the traffic 
</p>
<br />

<p>
![40](https://github.com/user-attachments/assets/6827d94b-bd48-48d1-a90f-ae9294a9f6c3)

</p>
<p>
Then go to Azure and grab the Public IP of DC-1 VM then load Remote Desktop Connection and open the app  
</p>
<br />

<p>
![41](https://github.com/user-attachments/assets/39025d99-ef25-4a88-aa5f-fa17afb8e56e)

</p>
<p>
Paste the IP of DC-1 in the computer section then click connect 
</p>
<br />

<p>
![42](https://github.com/user-attachments/assets/71c78910-7234-4887-a3d8-89e164a2c469)

</p>
<p>
Next type the username labuser and the password you made for DC-1 VM then click ok 
</p>
<br />

<p>
![43](https://github.com/user-attachments/assets/74acf06a-fc69-4522-ad9b-203b4611a305)

</p>
<p>
Next click yes to log into the VM
</p>
<br />

<p>
![44](https://github.com/user-attachments/assets/0918d656-b66d-4722-b4ca-bf5801e6d279)

</p>
<p>
Once the VM loads let Server Manager load as well. Next once networks load click yes 
</p>
<br />

<p>
![45](https://github.com/user-attachments/assets/21de8104-7f47-4ab4-8938-cce45adc4278)

</p>
<p>
Next type wf.msc in the search bar of DC-1 
</p>
<br />

<p>
![46](https://github.com/user-attachments/assets/aa4f6f39-80e4-430d-8fed-5b5210be737e)

</p>
<p>
Next click on Inbound Rules 
</p>
<br />

<p>
![47](https://github.com/user-attachments/assets/161ec2ba-b730-4419-be4e-aaafa0d9d08c)

</p>
<p>
Next click the protocol, then look for ICMPv4 protcol
</p>
<br />


<p>
![48](https://github.com/user-attachments/assets/496a7df3-d69b-47d3-9851-b27aafac8a33)

</p>
<p>
Next right click then enable rule for the following in the image above 
</p>
<br />

<p>
![49](https://github.com/user-attachments/assets/1752d953-1c81-4fa4-8727-fe914038027d)

</p>
<p>
Go back to Cilent-1 VM and you wil see the constant pinging click Ctrl + C then go back to the directory
</p>
<br />

<p>
![50](https://github.com/user-attachments/assets/9b8b7c60-4384-49d9-9dfc-ba48e18c704f)

</p>
<p>
Next go to DC-1 and click add roles and features 
</p>
<br />

<p>
![51](https://github.com/user-attachments/assets/2b494450-edcb-45f0-9848-0146e28e7c66)

</p>
<p>
Click next 
</p>
<br />

<p>
![52](https://github.com/user-attachments/assets/43f59cad-47d6-46f7-a592-a8dc1d919bb7)

</p>
<p>
Click next 
</p>
<br />

<p>
![53](https://github.com/user-attachments/assets/bafce169-a756-4b04-be0b-eeec5eb7a4c4)

</p>
<p>
Click next 
</p>
<br />

<p>
![54](https://github.com/user-attachments/assets/62a77d04-7702-4767-95d4-11a4a946c835)

</p>
<p>
Click the box for Active Directory Domain Services 
</p>
<br />

<p>
![55](https://github.com/user-attachments/assets/7d58b9c2-5776-4b75-83e5-16701846e9ad)

</p>
<p>
Click the add features 
</p>
<br />

<p>
![56](https://github.com/user-attachments/assets/f5e2a322-6fdb-44eb-b5f6-33cd6ddef9b9)

</p>
<p>
Click next 
</p>
<br />

<p>
![57](https://github.com/user-attachments/assets/1d3a2e10-0ac6-4ca8-af5f-08cf3bbc53fe)

</p>
<p>
Click next 
</p>
<br />

<p>
![58](https://github.com/user-attachments/assets/6953cfc5-3686-4cd8-9a5a-aa7a032aa940)

</p>
<p>
Click next 
</p>
<br />

<p>
![59](https://github.com/user-attachments/assets/fc52ca93-7a2c-4e1f-b95e-608a6b8de4ab)

</p>
<p>
Click Install 
</p>
<br />

<p>
![60](https://github.com/user-attachments/assets/3605f480-58c7-4337-9cc9-ccf02e81e4a5)

</p>
<p>
Next let the installation process start
</p>
<br />

<p>
![61](https://github.com/user-attachments/assets/26d0f5e1-e4ea-4bca-a831-b44f9d48ff6c)

</p>
<p>
Once the process finishes click close 
</p>
<br />

<p>
![62](https://github.com/user-attachments/assets/492d3458-7514-4bbc-ac54-5b77e8145053)

</p>
<p>
Next click the caution symbol near manage on the top right 
</p>
<br />

<p>
![63](https://github.com/user-attachments/assets/35dfef81-d781-432b-92bf-890ac9214b7b)

</p>
<p>
Next click Promote this server to a domain controller 
</p>
<br />

<p>
![64](https://github.com/user-attachments/assets/705a6763-2c46-4b5e-a77e-d3256c6d32d6)

</p>
<p>
Click add a new forest then type mydomain.com then click next. {NOTE} you can type anything you want just have a .com at the end of it please copy it down to your notepad to not forget 
</p>
<br />

<p>
![65](https://github.com/user-attachments/assets/720f050e-ed7a-4878-b663-5396e483f2af)

</p>
<p>
Next type the password in for this my password will be Password1 then click next 
</p>
<br />

<p>
![66](https://github.com/user-attachments/assets/6b32e14e-038d-4439-9fba-a3d8a3ba90a7)

</p>
<p>
Next click next
</p>
<br />

<p>
![67](https://github.com/user-attachments/assets/90cb493d-596d-4d4a-8b6b-684a07fbcb2a)

</p>
<p>
Next click next
</p>
<br />

<p>
![68](https://github.com/user-attachments/assets/04ca113d-66e4-422a-85f2-0fac305d339f)

</p>
<p>
Next click next
</p>
<br />

<p>
![69](https://github.com/user-attachments/assets/3a1dc0d6-865d-4c39-8ef0-76b38f2a3851)

</p>
<p>
Next click next
</p>
<br />

<p>
![70](https://github.com/user-attachments/assets/0f652f42-e881-42b8-aece-cd5a060ec567)

</p>
<p>
Next click install to finish creating the domain controller 
</p>
<br />

<p>
![71](https://github.com/user-attachments/assets/de1b2e51-415c-4afb-84ce-81878a5784c2)

</p>
<p>
Then let the installation process finish 
</p>
<br />

<p>
![72](https://github.com/user-attachments/assets/e7ddfa11-bb9f-4bfb-9f57-1d8fe280d366)

</p>
<p>
You might see the image above for Reconnecting dont click cancel let the VM bandwidth connect back only if it doesnt kick you out properly then click cancel 
</p>
<br />

<p>
![73](https://github.com/user-attachments/assets/00a33d64-30b3-4e2a-ab83-7a5cb51471c5)

</p>
<p>
Go back to Azure and click DC-1 copy the public IP 
</p>
<br />

<p>
![74](https://github.com/user-attachments/assets/20e7df53-b643-40eb-9dac-fac8853fbbd7)

</p>
<p>
Next type Remote Desktop Conenction and open the app 
</p>
<br />

<p>
![75](https://github.com/user-attachments/assets/2fab10e5-600c-4009-88ec-29b24eb803f3)

</p>
<p>
Now since we made DC-1 under another name click more choices then click use a different account 
</p>
<br />

<p>
![76](https://github.com/user-attachments/assets/0f58ac94-383a-43ce-81f6-793b953cae78)

</p>
<p>
Next tpye in mydomain.com\labuser for the username and the password is Password1 then click ok 
</p>
<br />

<p>
![77](https://github.com/user-attachments/assets/bc043c09-1fea-4d5e-8ab7-f69dee436e15)

</p>
<p>
Next click yes to log into the VM {NOTE} if it doesnt work the first time try again to log in. If it still doesn't let you then close Remote Desktop Connection and do the process again 
</p>
<br />

<p>
![78](https://github.com/user-attachments/assets/f3e34c06-16bc-430b-95ad-6c58752bc133)

</p>
<p>
Now once you are in the DC-1 VM let Server Manager load on the screen 
</p>
<br />

<p>
![79](https://github.com/user-attachments/assets/cc9d66fc-4d53-4f4e-b7d1-389d7d9238a2)

</p>
<p>
Next click Tools on the top right then go to Active Directory Users and Computers 
</p>
<br />

<p>
![80](https://github.com/user-attachments/assets/6c5d86c0-a599-45f4-a4ac-8f7a7c4ea43b)

</p>
<p>
Next click on mydomain.com folder on the left side 
</p>
<br />

<p>
![81](https://github.com/user-attachments/assets/36ce3c56-c7a0-4a0a-b9e7-ad0b65de843e)

</p>
<p>
Next right click anywhere and go to new then to organizational unit 
</p>
<br />


<p>
![82](https://github.com/user-attachments/assets/2695b3a5-a80e-462b-b17b-d4b7461b93a0)

</p>
<p>
Next type _EMPLOYEES then click ok 
</p>
<br />

<p>
![83](https://github.com/user-attachments/assets/77544dea-83a6-4dec-8cb8-384ceaad438e)

</p>
<p>
Now go back to mydomain.com and right click anywhere again, go to new then to organizational unit 
</p>
<br />

<p>
![84](https://github.com/user-attachments/assets/46f56088-dd29-499f-8a21-d516e1f86ef0)

</p>
<p>
Next type ADMINS then click ok 
</p>
<br />

<p>
![85](https://github.com/user-attachments/assets/64b72151-78f9-4c75-a408-99e302d2f733)

</p>
<p>
In ADMINS right click then go to new then to user
</p>
<br />

<p>
![86](https://github.com/user-attachments/assets/7181426c-341e-4b49-b121-2a05d686fa02)

</p>
<p>
For the first name type jane and the intials can be doe or the last name can be doe. For the user logon name type jane_admin then click next 
</p>
<br />

<p>
![87](https://github.com/user-attachments/assets/d28a9d42-fbe3-465a-8af4-4c91d37af879)

</p>
<p>
Next for the password type Password1 then uncheck user must change password at next login  
</p>
<br />

<p>
![88](https://github.com/user-attachments/assets/f05cbdbb-407a-410e-b4a1-d5715b62a733)

</p>
<p>
Next check the box for Password never expires then click next
</p>
<br />

<p>
![89](https://github.com/user-attachments/assets/979096e0-ab04-46d3-91cf-ceb26d257a1d)

</p>
<p>
Then finish to create the user 
</p>
<br />

<p>
![90](https://github.com/user-attachments/assets/7ecf6f2d-ce2c-4e0f-bba5-59ac7aa9a138)

</p>
<p>
Now you should see jane doe account in the ADMINS folder if not right click then go to refresh 
</p>
<br />

<p>
![91](https://github.com/user-attachments/assets/47bd1fb0-9bd6-40af-9b5b-e224064fab3f)

</p>
<p>
Next right click the account and go to properties 
</p>
<br />

<p>
![92](https://github.com/user-attachments/assets/7062b64c-01a7-4bd1-b56a-806c8a6ac416)

</p>
<p>
Next the member of tab then click add 
</p>
<br />

<p>
![93](https://github.com/user-attachments/assets/8f4b945e-0150-4631-8c35-316f83777475)

</p>
<p>
Next in the enter section type domain then click check names 
</p>
<br />

<p>
![94](https://github.com/user-attachments/assets/97d4d1f3-3e0b-40fa-88fc-94b8c25d6db0)

</p>
<p>
Next double click on Domain Admins then click ok 
</p>
<br />

<p>
![95](https://github.com/user-attachments/assets/8c0ade52-478a-4eef-b9a4-0bc7f6f860a1)

</p>
<p>
Then click ok 
</p>
<br />

<p>
![96](https://github.com/user-attachments/assets/6bf37b31-ca5b-4126-8835-b6ddec0e3627)

</p>
<p>
Then click apply to finish 
</p>
<br />

<p>
![97](https://github.com/user-attachments/assets/f309ef99-12f4-4473-ab76-9b2dae08a41a)

</p>
<p>
Next open command prompt then type whoami you will see we are still under labuser and not jane doe next type logoff 
</p>
<br />

<p>
![98](https://github.com/user-attachments/assets/01d0f8e0-cc86-48b7-a1e8-3cdf7b43acbc)

</p>
<p>
Go back to Azure and click DC-1 and copy the Public IP
</p>
<br />

<p>

</p>
<p>
Next type Remote Desktop Connection and open the app
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/7d700907-3cc5-431b-98f0-a37d65e1b3ec"/>
</p>
<p>
Next paste DC-1 VM public IP then click connect 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/5f10add9-bf30-4aa7-81ab-d83b1000d0b2"/>
</p>
<p>
Next click more choices then click use a different account
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/9c0046b0-84ef-47c0-a14f-1337cac6fdeb"/>
</p>
<p>
Next type mydomain.com\jane_admin in the username then the password is still Passsword1 then click ok 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/08c70bdd-4da0-414e-be79-d51b57e51b9e"/>
</p>
<p>
Next click yes to log into DC-1 VM
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/2b3e72ea-0ceb-453a-8012-d66c78df24c8"/>
</p>
<p>
DC-1 VM should load and you will see the name jane doe.
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/e1872b43-6a00-4378-895a-ef730ced9b33"/>
</p>
<p>
Open command line then type whoami and you will see you are logged in as jane_admin 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/991eb684-0118-4420-b7d8-46c8c5b62477"/>
</p>
<p>
Next right click the windows icon on the bottom left then click the system file 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/ca7edc7e-f5a5-4e71-9271-95a201e7bde7"/>
</p>
<p>
Now click Rename this PC (advanced)
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/167d7c20-efb0-4122-b11b-9e0537d4b2b7"/>
</p>
<p>
Next click change 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/09893ccd-1680-437c-87e2-ddcfe9aa58d4"/>
</p>
<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/b149e245-84ee-4bf8-8a37-c8b48eefa62e"/>
</p>
<p>
Next click member of and click the domain circle, then type domain.com then click ok 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/fcdd96ce-0d3b-4e59-919b-9c0fa77da602"/>
</p>
<p>
Now you will see an error displyed on the screen click ok this is because we have to change the NIC in azure for Cilent-1
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/1dc42180-09dc-4ea2-a91e-ee0533ec444a"/>
</p>
<p>
Now go to the Azure portal and go to Virtual Machine then click DC-1, copy the NIC Private IP
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/c56d3f3c-21ea-4519-bbd1-54138e525937"/>
</p>
<p>
Next click Cilent-1 and go to Network Interface and click on cilent 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/d441f8cb-4e31-46e1-b26f-73320b72ed2b"/>
</p>
<p>
Next click DNS servers then click custom 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/940c1feb-2931-4d21-9a39-313d1dd21af7"/>
</p>
<p>
Now paste the NIC Private IP of DC-1 then click save 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/320e0df8-7201-47b9-8416-e845374097ac"/>
</p>
<p>
Next let the process change the NIC
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/cb2f13af-e7ea-4643-8356-9e5ebd18eeb3"/>
</p>
<p>
Once its done you will see a green check you can click the bell icon to see the prcess load 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/48480f92-8917-4975-9a22-81918bac31cb"/>
</p>
<p>
Next go back to Virtual Machine adn click restart then click yes to restart Cilent-1 VM
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/e6ad8434-0787-4c5b-93f0-51adf131fd56"/>
</p>
<p>
You can click the bell icon and see the process restart the VM
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/60639df1-158c-49cf-9178-85a4b3fef1fd"/>
</p>
<p>
Once its done you will see a green check mark icon 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/afeca4be-57a5-4fb5-afbf-15b572a4495d"/>
</p>
<p>
Next click Cilent-1 then copy the public IP 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/a89632c4-19c5-4687-88c3-b5fde7acd026"/>
</p>
<p>
Type Remote Desktop Connection and load the app 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/e7db9734-b39f-48d6-8ddd-df988a842c36"/>
</p>
<p>
Next paste the Public IP in the computer section and then click connect 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/4658286d-46a4-407a-b067-6ec97cdb16b0"/>
</p>
<p>
Now type labuser for the username and the original password you made for Cilent-1 then click ok 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/4df21922-1a88-49a2-88f6-a6b9c1fd1de4"/>
</p>
<p>
Next press yes to log into the VM
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/32ee1ac3-c0c7-4d4b-8a83-ae2c9e3d3be1"/>
</p>
<p>
Now you will see Cilent-1 VM load under labuser 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/878b7f3d-c799-49c8-9911-15925544646b"/>
</p>
<p>
We are going to do the same process as before right click the windows icon then click on system 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/258597d2-6ac4-41e3-8ef5-b45e44a7ab37"/>
</p>
<p>
Next click Rename this PC (advanced)
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/6d5b289e-811b-4a1e-bfc3-a1cf01118036"/>
</p>
<p>
Now click change 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/b80a520f-fde4-4826-9ebc-c7ab1d78faec"/>
</p>
<p>
Now click domain and type mydomain.com then click ok 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/ebd2a07f-2250-4a7f-a7a8-cefe6c867cca"/>
</p>
<p>
Now Computer Name / Domain Changes should load on your screen 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/b0ef21c9-fb5c-4d48-8b4b-bd6715bc372b"/>
</p>
<p>
Next type mydomain.com\jane_admin then the password is Password1 then click ok 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/9d50d6f6-eb5a-464a-8b81-4f3fa4ae482e"/>
</p>
<p>
You will see the VM is trying to reconnect dont click cancel let the bandwidth conenct back to the VM
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/257c9513-176f-4a61-953d-5117e3c0a1c7"/>
</p>
<p>
Next you will see a Please wait page 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/f0fd0c40-631a-4cc2-abcd-46a6891be72b"/>
</p>
<p>
Close out of everything, but you wil see a tab that says You must restart your computer to apply these changes then click ok 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/eca341c4-0cd2-4648-afd3-76a1dd18c603"/>
</p>
<p>
Then click Restart Now to restart the VM
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/79dac041-0092-49d6-b7ac-6d65e855b887"/>
</p>
<p>
Next you will see a Restarting Screen load 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/f014446b-69f3-4b2a-8e94-29566fd6b64a"/>
</p>
<p>
It will kick you out of Cilent-1 VM now go back to get the Public IP then type Remote Desktop Connection and open the app 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/18513efd-bad4-4501-9805-fbad9aff8315"/>
</p>
<p>
Next paste the public IP in the computer section then click connect 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/979b19d5-09c7-40c9-8a0f-5e8e090fad45"/>
</p>
<p>
Click more choices then click use a different account 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/3e1dce01-7608-47e6-bdf9-e48a73acd8f4"/>
</p>
<p>
Now type mydomain.com\jane_admin then the password is Password1 then click ok 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/bc113c76-8db9-4504-9b7a-dc1e3918b5ae"/>
</p>
<p>
Next click yes to connect to the VM
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/85e0f5b0-72b5-49c4-9eaf-489d53e09d45"/>
</p>
<p>
Now you will see the Cilent-1 VM loading as jane doe 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/88f0493d-c56e-4fd2-b13a-6a12170c3e64"/>
</p>
<p>
Next right click the windows icon then click system 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/6407b46d-9953-456f-ad88-cb61bb9bf7f2"/>
</p>
<p>
Next click Remote Desktop 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/83179131-dce0-42b4-aa5f-ab239c64e11a"/>
</p>
<p>
Now click Select users that can remotely access this PC
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/756760a0-9da9-4b38-bb5b-442fa24ff787"/>
</p>
<p>
Next click add 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/80910d23-635e-4f77-8bf5-9217a6db30b9"/>
</p>
<p>
Type domain users then click check names 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/1fd5e59e-34b0-4fc2-bb12-a76c9338ef3d"/>
</p>
<p>
You will see the name changed to CAPS with a underscore then click ok 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/50bd24fb-9321-4000-8890-afe5ae5962f9"/>
</p>
<p>
Next click ok 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/9daedf6e-ae64-4cd5-bf3d-95d27e2e0f4e"/>
</p>
<p>
Go back to DC-1, another way to get to Users and Computers is to click the windows icon on the bottom left. Next click Windows Administrative Tools then click Active Directory Users and Computers
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/8d0091c5-b02b-48c1-94fb-8df23a4f8f01"/>
</p>
<p>
Next click users then click Domain Users
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/4fc4f2f5-d1d6-43b5-b4fb-982249ecdb8e"/>
</p>
<p>
Now you will see jane doe and labuser are under the Domain Users
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/f00e2f1b-0b58-4ff2-a436-d7a84178cab3"/>
</p>
<p>
Next type Windows Powershell ISE right click and run as administrator
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/52731396-42b2-4752-80a3-65fa335d9b64"/>
</p>
<p>
Now click yes to run the software 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/4e1022f8-6bd3-44d2-9b44-eee5d0883904"/>
</p>
<p>
Click file then click new 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/d3281cb9-e79d-4f93-8a18-7bdb24f3fbf2"/>
</p>
<p>
Go to the Link and copy the code this code will create 2000 users https://github.com/Jacobvillagomez1/Generate-Names-Create-Users.ps1/blob/main/README.md
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/3206dc71-8055-419f-b903-e807c7b92ca8"/>
</p>
<p>
Now paste the code in the white blank page section 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/526b4bd7-d087-4be2-ba06-e5e000c79cb1"/>
</p>
<p>
Now click the green play icon to run the script 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/0899eab8-7d9a-4c5c-b4e2-700f827fa5db"/>
</p>
<p>
Now in the blue section you will see the 2000 users being created in a ligth blue color 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/850e7ff4-196d-4a84-b359-a3565bbf9651"/>
</p>
<p>
Next click on the _EMPLOYEES folder then right click and click refresh 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/3d794795-61d7-4b97-b2c7-8a6ff1283ccb"/>
</p>
<p>
Now you will see the current users that have been created 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/937a3c25-6aee-4bf4-bc18-0100f4f2442a"/>
</p>
<p>
Next go to Cilent-1 open up the command line then type logoff, then press enter 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/d62f1456-4352-4ce0-9d78-a574356f218d"/>
</p>
<p>
Now that we logged out of Cilent-1 we are going to go to DC-1 VM and pick a user then copy the display name. 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/92106042-1475-4cb6-aafb-34b80df93203"/>
</p>
<p>
Open up your notepad and paste or type the display name of the account you want to log into  
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/db198ef9-536f-4a39-b9a2-5baf68143dc4"/>
</p>
<p>
Now type Remote Desktop Connection and open the app
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/0b5b7ff7-afce-42a4-8058-4fe3aff29ba8"/>
</p>
<p>
Next paste the public IP of Cilent-1 VM then click connect
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/075247fe-f3ea-49b9-8109-64249c551e44"/>
</p>
<p>
Next click more choices and click use a different account 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/809a2320-5074-46da-a0e6-7ce3e6984b1e"/>
</p>
<p>
Now type mydomain.com\ then your username. Next for the password type Password1 refer to the image above then press ok
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/d681a6c7-f783-42d1-be11-baaa5ede25a0"/>
</p>
<p>
Next press yes to connect to the VM
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/38251e25-e471-464f-a9d2-c7f7e1858c3a"/>
</p>
<p>
Now you will see the username display on the screen of the loading screen of Cilent-1 VM
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/43d5f06e-cac1-436e-bfe0-d93f94b641fd"/>
</p>
<p>
Open commandline and type whoami and you will see we are logged in as the user you picked. Type hostname and you will see you are still under Cilent-1 then type logoff 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/f83f4694-e231-473f-9e34-8741b13b0a2e"/>
</p>
<p>
Go back to DC-1 VM and pick another user, then copy the display name 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/a0857ddd-8fcd-4bad-8a24-a712a754db5d"/>
</p>
<p>
Type Remote Desktop Connection and load the app 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/4d1f40ee-b93e-4741-83a1-68fceac33c77"/>
</p>
<p>
Next paste the Public IP of Cilent-1 then click connect 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/66242ef0-4145-454b-a85e-cc5a253ee98c"/>
</p>
<p>
Click more choices then click use a different account 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/164e4d51-a623-48ee-8983-8a480d4e0829"/>
</p>
<p>
Now type mydomain.com\ then the username, but for the password type the password incorrectly ten times to lock you out of your account refer to the image above 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/63f27065-9e25-42fb-969b-57824e9cff63"/>
</p>
<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/686606a1-4259-41a9-a12d-843ef254a1d1"/>
</p>
<p>
Next go back to DC-1 VM and go to the account tab of the user you picked. Click th box Unlock account then click ok 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/8a06ac57-d4bc-4478-8ce2-ee345b4e45e1"/>
</p>
<p>
You can also right click the user you picked and click reset password, or even disable the account 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/39a34abc-ab16-4bb4-a6d7-f668f6662af6"/>
</p>
<p>
Now to see Lab 6 https://github.com/Jacobvillagomez1/Create-Inspect-and-Delete-DNS-A-Records-and-CNAME and Lab 7 https://github.com/Jacobvillagomez1/Network-File-Shares-and-Permissions 
</p>
<br />
