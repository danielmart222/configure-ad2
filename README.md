<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure) Part 3 and 4 </h1>
This tutorial covers how to set up remote desktop access for non-administrative users on a desktop. It includes the use of PowerShell ISE to create 1,000 users with a script for logging into a domain-joined desktop. Configuration of group policy to lock out user accounts and update immediately using commands will be discussed. Instructions for unlocking accounts, resetting passwords, enabling, and disabling accounts will also be provided.<br />




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


------------


![image](https://github.com/user-attachments/assets/8fd1e0f9-ebc8-40ff-86db-544ac4b11a50)


----------

<h2>Step 1: Setup Remote Desktop for non-administrative users on Client-1</h2>

----------

- Log on to Client-1 as  jane_admin 

-----

![image](https://github.com/user-attachments/assets/124a3b14-409f-4292-b4eb-4e52e73362fd)

---------------

- Within Client-1: allow domain users to access desktop -> Right click the start menu and click on system -> Click on Remote Desktop on the left hand side of the screen -> Click on (select users that can remotely access this PC) -> Click on Add -> Type: domain users -> Click on check names -> Click on ok -> Then sign out of Client-1 as jane_admin

---------



![image](https://github.com/user-attachments/assets/f63e0683-b5c7-4282-ac8c-56719eae40ea)



----------


   <h2> Step 3: Open Power Shell ISE as an administrator and create 1,000 users with a Script </h2>

-----------

- Log into DC-1 as jane_admin 


---------


![image](https://github.com/user-attachments/assets/1b4dbf99-6c28-4a1c-9c5d-25906c068e40)



-----------


- Open Power Shell ISE as an Adminstrator 



------------


![image](https://github.com/user-attachments/assets/a64663bc-40c1-438b-a38b-15cdb0272d3f)


-----------



- Within Power Shell -> Create a New Script -> Paste Script -> Click on the Green Play Button on the menu bar ->


--------

![image](https://github.com/user-attachments/assets/101ed999-fc08-4289-ad57-5225c1c85ccd)


----------


  <h2> Step 4: Pick a random User that was automatically created from the script and try to log into Client-1 </h2>


-----------

- Within DC-1: Click on the Start menu and click on Windows Administrative Tools -> Click on Active Directory Users and Computers -> Click on the _EMPLOYEES OU -> Select fas.tacos


-----------

![image](https://github.com/user-attachments/assets/9fc72c6b-34af-40af-9e5b-e30add228c86)


-----------

- Try to log into Client-1 with the User  fas.tacos

---------

![image](https://github.com/user-attachments/assets/85e5e5f1-1952-4902-889c-4e7139e4d52b)


-------------

![image](https://github.com/user-attachments/assets/22b5a44d-f6aa-44f3-8069-57601c3f264b)





<h1>Part 4 - Group Policy and Managing Accounts </h1>

<h2>  Group Policy and Managing Accounts </h2>

------------

<h2> Step 1: Configure Group Policy to Lockout the account after 5 attempts </h2>


-----------

- Right click the Start menu button -> Click on run


---------------

![image](https://github.com/user-attachments/assets/7237bf26-4e5b-4e1f-9e7b-330d13dd9f99)


------------


- Expand Forest: Mydomain.com ->  Expand Domains -> Expand Mydomain.com -> Right click on Default Domain Policy and click on Edit ->

--------------

![image](https://github.com/user-attachments/assets/3b2d6e4e-bc25-49d4-9839-a5ef48631495)


----------


- Under Computer Configuration -> Expand Policies -> Expand Windows Settings -> Expand security Settings ->  Expand Account Policies -> next click on Account Lockout Policy.

------------


![image](https://github.com/user-attachments/assets/d19e41f9-990f-4f5d-8dee-4f396cd18e10)



--------------

- Click on Account lockout duration -> Set account lockout duration to 30 mins -> Click on apply and ok

-----------

![image](https://github.com/user-attachments/assets/c6347c7d-e7c2-48f6-beb7-fa265f47cd80)


---------


- Click on Account lockout Threshold  -> Set account lockout Threshold to  5 invalid logon attempts -> Click on apply and ok 


-----------


![image](https://github.com/user-attachments/assets/e8c172f2-1c17-4c21-8db0-76588e5fb4fa)


--------------


<h2> Step 2: Log into Client-1 as jane_admin and force an update immediately on the Group Policy </h2>

--------------

![image](https://github.com/user-attachments/assets/b4dee952-0078-4f33-84d2-511cf37e6d6f)

----------


- Open Command Prompt as an administrator

----------

![image](https://github.com/user-attachments/assets/dae868a9-ca65-430d-8754-bdf25cd251b5)


-----------

- Type the Command: gpupdate /force


--------------


![image](https://github.com/user-attachments/assets/a78b3519-8105-4700-a29c-961617fe8993)


----------


- Next Type the command: gpresult /r

-----------

![image](https://github.com/user-attachments/assets/4c7fd237-cb36-4bde-bea3-dc6ba5361b43)



------------

<h2> Step 3: Next Log into Client-1 with the user fas.tacos -> Purposely lock out your account with the user fas.tacos  to see if the Group Policy was implemented -> After 5 invalid Attempts, the account for fas.tacos should be locked out  </h2>

-------------


- The logon attempt failed

-----------



![image](https://github.com/user-attachments/assets/c1ad7241-ef54-4249-94a2-8eac6662337c)



-------------

- User Account has been locked

-----------

![image](https://github.com/user-attachments/assets/3b0baf03-94f3-41b6-9b01-575d326ffea6)


-------------



<h2> Step 4: Unlock the account for user fas.tacos </h2>


--------------


- Within DC-1 -> Right click the Start menu and click on Administrative Tools -> Choose Active Directory Users and Computers -> Right click Mydomain.com and click on find -> Type: fas.tacos and click on Find now -> Right click on fas.tacos and click on Properties -> click on account -> check the box that says: unlock account -> click on apply and ok

-------


![image](https://github.com/user-attachments/assets/ddbaa839-0ff9-4d6b-a7bd-beb50bb1043b)


----------


<h2> Step 5: Attempt to sign in with the user fas.tacos </h2>


----------------

![image](https://github.com/user-attachments/assets/c2a840fd-2ac0-480e-a834-8e7395c30d70)


-----------

![image](https://github.com/user-attachments/assets/5dac9a86-e0d7-41ad-bf3f-76b34d690d84)



-----------


<h2> Step 6: How to reset a Password, disable an account, and enable an account  </h2>


-----------


- Within DC-1 -> Right click the Start menu and click on Administrative Tools -> Choose Active Directory Users and Computers -> Right click Mydomain.com and click on find -> Type: fas.tacos and click on Find now -> Right click on fas.tacos -> Click on Reset Password


-------------

- Reset password

-----------

![image](https://github.com/user-attachments/assets/cff8a9a2-2ced-4225-ac45-e241bfd78376)


------------

- Password reset 

----------


![image](https://github.com/user-attachments/assets/3febab47-73ff-44a3-a856-6b0af4df2d43)



--------------


- Within DC-1 -> Right click the Start menu and click on Administrative Tools -> Choose Active Directory Users and Computers -> Right click Mydomain.com and click on find -> Type: fas.tacos and click on Find now -> Right click on fas.tacos -> Click on Disable Account/Enable Account 

------------------


- Disable account


---------


![image](https://github.com/user-attachments/assets/bc453c34-f0bf-47b2-a572-e46ea25f36da)


---------

- Attempt to log into Client-1 with the user fas.tacos

---------------------



![image](https://github.com/user-attachments/assets/6ce9aae4-9320-4356-ab51-0e87b4487bed)



--------------

- Disabled account

------------


![image](https://github.com/user-attachments/assets/5d7442aa-8596-4179-b459-f067035d4f70)



-------------

- Enable account

-------------


![image](https://github.com/user-attachments/assets/38c25569-3bd2-4501-a5cb-4b1c0e4822f4)


-----------------

- Enabled Account

--------------


![image](https://github.com/user-attachments/assets/3e030ed4-0eb7-4abd-b759-1be52031bb79)



-------------


<h2> Step 7: Attempt to log into Client-1 with user fas.tacos </h2>


------------

![image](https://github.com/user-attachments/assets/95b67155-fd11-46a2-a2db-825180cf550a)


----------------------

![image](https://github.com/user-attachments/assets/dd9e824d-1f6d-46c7-80c8-8f7306b090e1)



