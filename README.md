**# osticket-prereqs
<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How To Install osTicket with Prerequisites](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- Azure Virtual Machine
- osTicket zip file
- enable IIS with CGI
- install PHP manager for IIS
- install HeidiSQL

<h2>Installation Steps</h2>

![image](https://github.com/user-attachments/assets/6e580345-c4cf-479c-8a03-3baf859462e2)

Create an Azure Virtual Machine Windows 10, 4 vCPUs
Name: osticket-vm
Username: labuser
Password: osTicketPassword1!

Log into the VM with Remote Desktop

Within the VM (osticket-vm), download the osTicket-Installation-Files.zip and unzip it onto your desktop. The folder should be called “osTicket-Installation-Files”
We will use the files in this folder to install osTicket and some of the dependencies.

Install / Enable IIS in Windows WITH CGI
World Wide Web Services -> Application Development Features -> [X] CGI
(Installing IIS example shown above)



![image](https://github.com/user-attachments/assets/5bc49ec0-718c-417e-995b-e79487c0d900)

  
If done correctly the webpage for 127.0.0.1 should display within the VM (virtual machine)
making the computer a webserver. 


![image](https://github.com/user-attachments/assets/cb8f6554-1d54-448d-9b60-477e4fb54552)

From the “osTicket-Installation-Files” folder, install PHP Manager for IIS (PHPManagerForIIS_V1.5.0.msi) (this is so osTicket will work)

![image](https://github.com/user-attachments/assets/656a5bba-421b-4301-ac9a-8ae07361ec97)

From the “osTicket-Installation-Files” folder install the Rewrite Module (rewrite_amd64_en-US.msi)

![image](https://github.com/user-attachments/assets/37975726-d288-4efd-9a83-ad8f13e1bb51)

Create the directory C:\PHP
![image](https://github.com/user-attachments/assets/68f311a5-f2cb-48c4-9469-024662c97a60)

From the “osTicket-Installation-Files” folder, unzip PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip) into the “C:\PHP” folder

![image](https://github.com/user-attachments/assets/52e89b2c-335f-4a05-9d6a-efc25981efb5)

From the “osTicket-Installation-Files” folder, install VC_redist.x86.exe.

![image](https://github.com/user-attachments/assets/70ab8e02-b3ef-4113-af78-307f5692dde3)

 From the “osTicket-Installation-Files” folder, install MySQL 5.5.62 (mysql-5.5.62-win32.msi)
    Typical Setup -> ![image](https://github.com/user-attachments/assets/74ad297f-d083-4b4d-b495-19df07b1403c)

![image](https://github.com/user-attachments/assets/964e85e0-b8ec-4105-8a08-c4eca20e9e8a)

Launch Configuration Wizard (after install) ->
Standard Configuration ->
Username: root
Password: root

![image](https://github.com/user-attachments/assets/8ca88a20-b570-4351-a98c-7d57a1d3f86c)

Open IIS as an Admin
![image](https://github.com/user-attachments/assets/fe8f36e6-0f0c-435a-821f-2783150886c5)

Register PHP from within IIS (PHP Manager -> C:\PHP\php-cgi.exe)

![image](https://github.com/user-attachments/assets/970f8d76-2f28-46f6-8947-7557ca0d3f96)

Reload IIS (Open IIS, Stop and Start the server)

Install osTicket v1.15.8
![image](https://github.com/user-attachments/assets/2905343e-ec11-4146-be31-ea7c4d7c6134)

From the “osTicket-Installation-Files” folder, unzip “osTicket-v1.15.8.zip” and copy the “upload” folder into “c:\inetpub\wwwroot”
Within “c:\inetpub\wwwroot”, Rename “upload” to “osTicket”


Reload IIS (Open IIS, Stop and Start the server)

![image](https://github.com/user-attachments/assets/1a865a31-3efa-498e-8954-e6b3a171e630)

Go to sites -> Default -> osTicket
On the right, click “Browse *:80”

![image](https://github.com/user-attachments/assets/c6eb7f1a-2547-4e6d-8998-942c8536bf81)

Note that some extensions are not enabled
Go back to IIS, sites -> Default -> osTicket
Double-click PHP Manager
Click “Enable or disable an extension”
Enable: php_imap.dll
Enable: php_intl.dll
Enable: php_opcache.dll
Refresh the osTicket site in your browser, observe the changes

![image](https://github.com/user-attachments/assets/92725ef9-9223-403c-91ce-c227f6ca21c1)

Rename: ost-config.php
From: C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php
To: C:\inetpub\wwwroot\osTicket\include\ost-config.php

![image](https://github.com/user-attachments/assets/15b467f8-fde9-47ab-8f8d-39991319f872)
![image](https://github.com/user-attachments/assets/29744b3a-9925-4411-b673-bd43eeb6a232)

Assign Permissions: ost-config.php
Disable inheritance -> Remove All
New Permissions -> Everyone -> All

![image](https://github.com/user-attachments/assets/33b1e625-1b41-4355-8074-78271ab2cb5c)

Continue Setting up osTicket in the browser (click Continue)
Name Helpdesk
Default email (receives email from customers)
![image](https://github.com/user-attachments/assets/80f953b3-e715-40ca-a24f-82f2d73a6d84)

From the “osTicket-Installation-Files” folder, install HeidiSQL.
Open Heidi SQL

![image](https://github.com/user-attachments/assets/ef14980b-db86-4b2b-97a3-b4e503e9dd9b)

Create a new session, root/root
Connect to the session
Create a database called “osTicket”

![image](https://github.com/user-attachments/assets/060e7323-326b-4ba0-a523-2d709fdfda7d)

Continue Setting up osTicket in the browser
MySQL Database: osTicket
MySQL Username: root
MySQL Password: root
Click “Install Now!”

![image](https://github.com/user-attachments/assets/03434be0-55e6-4c3d-b229-26e9d72753b6)






