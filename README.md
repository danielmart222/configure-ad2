<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
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

- Part 1 Preparing AD infrastucture
- Part 2 Deploying Active Directory 
- Part 3 Creating users with Power shell
- Part 4 Group Policy and Managing Accounts

<h1>Part 3 - Creating users with powershell </h1>

<h2> Creating users with powershell </h2>

------------


![image](https://github.com/user-attachments/assets/8fd1e0f9-ebc8-40ff-86db-544ac4b11a50)


----------

<h2>Step 1: Setup Remote Desktop for non-administrative users on Client-1</h2>

----------

- Log on to Client-1 as  jane_admin 

-----

![image](https://github.com/user-attachments/assets/ca14a56b-82cd-49ec-97a9-2bd08e90acc5)

---------------

- Within Client-1: allow domain users to access desktop -> Right click the start menu and click on system -> Click on Remote Desktop on the left hand side of the screen -> Click on (select users that can remotely access this PC) -> Click on Add -> Type: domain users -> Click on check names -> Click on ok -> Then sign out of Client-1 as jane_admin

---------



![image](https://github.com/user-attachments/assets/8e838e39-c7ea-4797-a8f2-dbd8b85b1a28)


----------


   <h2> Step 3: Open Power Shell ISE as an administrator and create 1,000 users with a Script </h2>

-----------

- Log into DC-1 as jane_admin 


---------


![image](https://github.com/user-attachments/assets/d9fb0b0a-e414-4c91-9a90-736f52790b04)


-----------


- Open Power Shell ISE as an Adminstrator 



------------


![image](https://github.com/user-attachments/assets/47eaa5ef-b936-4c17-b781-b3a02a53482c)



-----------



- Within Power Shell -> Create a New Script -> Paste Script -> Click on the Green Play Button on the menu bar ->


--------

![image](https://github.com/user-attachments/assets/4997b04d-af38-4eea-969e-86a6064c7e22)


----------


  <h2> Step 4: Pick a random User that was automatically created from the script and try to log into Client-1 </h2>


-----------

- Within DC-1: Click on the Start menu and click on Windows Administrative Tools -> Click on Active Directory Users and Computers -> Click on the _EMPLOYEES OU -> Select fas.tacos


-----------

![image](https://github.com/user-attachments/assets/982832d2-0147-476a-bc63-be23c0d111fa)

-----------

- Try to log into Client-1 with the User  fas.tacos

---------

![image](https://github.com/user-attachments/assets/061bdb6f-542b-4f20-9d2b-803c3fa124c2)


-------------

![image](https://github.com/user-attachments/assets/22b5a44d-f6aa-44f3-8069-57601c3f264b)





<h1>Part 3 - Group Policy and Managing Accounts </h1>

<h2>  Group Policy and Managing Accounts </h2>


