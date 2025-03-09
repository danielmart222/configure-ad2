<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure) Part 3 and 4 </h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell
- Command Prompt

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

------------

<h2> Step 1: Configure Group Policy to Lockout the account after 5 attempts </h2>


---------------

![image](https://github.com/user-attachments/assets/7237bf26-4e5b-4e1f-9e7b-330d13dd9f99)


------------


- Expand Forest: Mydomain.com ->  Expand Domains -> Expand Mydomain.com -> Right click on Default Domain Policy and click on Edit ->

--------------

![image](https://github.com/user-attachments/assets/7b3236b9-975c-49b9-95b0-6cf6ab197c55)

----------


- Under Computer Configuration -> Expand Policies -> Expand Windows Settings -> Expand security Settings ->  Expand Account Policies -> next click on Account Lockout Policy.

------------


![image](https://github.com/user-attachments/assets/898cffda-759e-47cf-a0a5-bedfc3e61022)


--------------

- Click on Account lock out duration -> Set account lock out duration to 30 mins -> Click on apply and ok

-----------

![image](https://github.com/user-attachments/assets/d2196705-4e62-41c1-bffb-1ff2604009c8)

---------


- Click on Account lock out Threshold  -> Set account lock out Threshold to  5 invalid logon attempts -> Click on apply and ok 


-----------


![image](https://github.com/user-attachments/assets/9e537167-cda8-4112-8e66-ec02c7acf393)

--------------


<h2> Step 2: Log into Client-1 as jane_admin and force an update immediately on the Group Policy </h2>

--------------

![image](https://github.com/user-attachments/assets/3d5efbc0-3e34-4383-ad01-4f522dfe3808)

----------


- Open Command Prompt as an administrator

----------

![image](https://github.com/user-attachments/assets/2648cff9-41bd-4a76-a994-ebadbf20541b)

-----------

- Type the Command: gpupdate /force


--------------


![image](https://github.com/user-attachments/assets/f473ee5e-6458-4cd9-9bb1-bb84b0562655)

----------


- Next Type the command: gpresult /r

-----------

![image](https://github.com/user-attachments/assets/a1d8efc3-4f84-4657-b637-a3b4de6ee2ad)


------------

<h2> Step 3: Next Log into Client-1 with the user fas.tacos -> Purposely lock out your account with the user fas.tacos  to see if the Group Policy was implemented -> After 5 invalid Attempts, the account for fas.tacos should be locked out  </h2>

-------------


- The logon attempt failed

-----------



![image](https://github.com/user-attachments/assets/81fdf90a-caae-4df0-8596-8008500fe8f0)


-------------

- User Account has been locked

-----------

![image](https://github.com/user-attachments/assets/4f0423c0-a13d-49bf-9802-ab506154e995)

-------------



<h2> Step 4: Unlock the account for user fas.tacos </h2>


--------------


- Within DC-1 -> Right click the Start menu and click on Administrative Tools -> Choose Active Directory Users and Computers -> Right click Mydomain.com and click on find -> Type: fas.tacos and click on Find now -> Right click on fas.tacos and click on Properties -> click on account -> check the box that says: unlock account -> click on apply and ok

-------


![image](https://github.com/user-attachments/assets/bf744900-42e4-4060-a32c-f0cc28eaf6d6)

----------


<h2> Step 5: Attempt to sign in with the user fas.tacos </h2>


----------------

![image](https://github.com/user-attachments/assets/38319c7e-8eb9-45e9-b02f-a46b1abe6c9d)

-----------

![image](https://github.com/user-attachments/assets/5dac9a86-e0d7-41ad-bf3f-76b34d690d84)



-----------


<h2> Step 6: How to reset a Password, disable an account, and enable an account  </h2>


-----------


- Within DC-1 -> Right click the Start menu and click on Administrative Tools -> Choose Active Directory Users and Computers -> Right click Mydomain.com and click on find -> Type: fas.tacos and click on Find now -> Right click on fas.tacos -> Click on Reset Password


-------------

- Reset password

-----------

![image](https://github.com/user-attachments/assets/5dabe3a6-dd5a-4a46-a00b-53562509af9c)


------------

- Password reset 

----------


![image](https://github.com/user-attachments/assets/96145212-725b-4a16-88b9-62af62d80cad)


--------------


- Within DC-1 -> Right click the Start menu and click on Administrative Tools -> Choose Active Directory Users and Computers -> Right click Mydomain.com and click on find -> Type: fas.tacos and click on Find now -> Right click on fas.tacos -> Click on Disable Account/Enable Account 

------------------


- Disable account


---------



![image](https://github.com/user-attachments/assets/98a88cd6-dd17-4ee3-8bba-14ec9d770838)

---------

- Attempt to log into Client-1 with the user fas.tacos

---------------------



![image](https://github.com/user-attachments/assets/61ff2bf7-9956-4ad5-894e-345da193fcd0)


--------------

- Disabled account

------------


![image](https://github.com/user-attachments/assets/93b7fc94-410a-4cec-b573-a96ba3357e6a)


-------------

- Enable account

-------------


![image](https://github.com/user-attachments/assets/1dcd8c60-010f-40dd-bcf6-a3584fec2404)

-----------------

- Enabled Account

--------------


![image](https://github.com/user-attachments/assets/7a8dd51d-74f8-49a4-b2d7-775a59618e54)


-------------


<h2> Step 7: Attempt to log into Client-1 with user fas.tacos </h2>


------------

![image](https://github.com/user-attachments/assets/c947069b-e5f4-4d89-b231-9501e44c6be1)


----------------------

![image](https://github.com/user-attachments/assets/82b5e56d-e97a-4c2c-8176-210eb8cd705e)


