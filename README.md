# Installing Active Directory and add a new user to active directory and a group

This demonstration walkthrough is going to explain how to install Windows 2022 server on a virtual machine.
After the installation of the operating system we will set up Active Directory Domain Services, DNS, and DHCP on the host device.
This walkthrough was done to help those looking to learn Active Directory, setting up DNS and DHCP and a basic walkthrough of adding a user to a group and into active directory

## Set up virtual machine with Windows 2022 Server Evaluation Version with Virtual Box

For the Windows Server 2022 machine virtual machine setup, open up virtual box and click new at the top of the window toolbar. 
![Step 1](./images/blank_v_box_1.png)

Name your machine, select the folder where your machine and files will be saved, select your ISO file, skip the unattended installation and then click next.
![Step 2](./images/active_directory_step_2.png)

Since this is not going into production, keep the Hardware as the deaults, but adjust according to your needs.

![Step 3](./images/active_directory_step3.png)

Set the size of your virtual hard disk adjust according to your needs. Click next and then verify the settings.

![Step 4](./images/active_directory_step_4.png)

Once the machine is setup before starting your machine, go to your machines system settings.  This can be achieved either right clicking on your machine and clicking settings.  Or you can highlight your machine and then click the settings button at the top of the virtual box toolbar

In the system settings, remove the floppy drive from the boot order and move the hard disk to the top and the optical disk second.

![Step 5](./images/active_directory_step_5.png)

In your network settings, adjust adapter 1 so it is a Bridged adapter.  You can adjust to your own needs.  Since I am using my own home router, I am using the Bridged network, basically the bridge allows my virtual machine to interact with other devices on my home network as though it is a physical machine. 

![Step 6](./images/active_directory_step_6.png)

Once those settings are saved start your machine clicking start at the top of the virtual box menu.  Your machine will start and begin installing the Windows Server 2022.  The initial prompt click next

![Step 7](./images/active_directory_step_7.png)

Select the standard evaluation version with desktop experience.  If you want a smaller sized OS and only command line access install the version without the desktop experience.

![Step 8](./images/active_directory_step_8.png)

Click **Custom: Install Microsoft Server Operating System Only** if it is a fresh install, if you are upgrading click **Install Microsoft Server Operating System and keep files, settings, and applications**

**Be aware, installing the OS will delete everything on your hard drive**
If this is a fresh install and have no files, you do not need to worry.  If you are installing this on your actual working computer or have files you want to keep, make backups of everything and select upgrade.

![Step 9](./images/active_directory_step_9.png)

Select which drive you would like to install the Windows Server on.

![Step 10](./images/active_directory_step_10.png)

Next the installation will take over.
**Grab some coffee, tea or water....this could take some time depending how much processing power you gave your machine**
![Step 11](./images/active_directory_step_11.png)

After the installation completes, you will need to create a unique password for the Administrator account.  
**Do not lose this password!**
![Step 12](./images/active_directory_step_12.png)

Log in to your account, right now this is still a workgroup computer so you will not be able to log in to the domain you create yet.

![Step 13](./images/active_directory_step_13.png)

We will be using this machine to be a DNS server and a DHCP server so you will need to set up a static IP address.
You have 3 ways to get to your network settings to change you IP address to static.
1. right click on your network connection in the System aka Notifications area in the bottom right of the screen -> click **Open Network & Internet settings** -> Click **Change adapter options on the right side of the screen** 
2. in the search bar search Network status and click Network Status -> Click **Change adapter options on the right side of the screen** 
3. right click the start menu -> click **Network Connections** -> Click **Change adapter options on the right side of the screen** 

![Step 14](./images/active_directory_step_14.png)

Right click on your network connection and click **Properties**

![Step 15](./images/active_directory_step_15.png)

Locate Internet Protocol Version 4 (TCP/IPv4) in your list, highlight it and click **Properties**
You will need:
1. an IP address you want to set to your Windows server
2. the default gateway aka your router's address in order to have access to the internet adn handle routing on your network
3. the subnet mask of your network. 
4. a DNS server IP address, this will change but you need one initially either using googles 8.8.8.8 or quad9's 9.9.9.9 or your service providers DNS


![Step 16](./images/active_directory_step_16.png)

To find your gateway address, subnet mask and DNS open up command prompt by right clicking the start menu and click run -> type cmd.exe adn then you are in your command prompt

You can also search command prompt in the task bar search bar and click Command prompt

![Step 17](./images/active_directory_step_17.png)

Type in ipconfig /all

This will bring up tons of network information on your device.  Look for the network device you are using for your local connection.  Find the Default Gateway, remember a DNS server address, Subnet Mask and also think of an IP address you want or you can use the current address.

![Step 18](./images/active_directory_step_18_red_lined.png)

Back in your Internet Protocol Version 4 (TCP/IPv4) Properties, click Use the following IP address.
Enter in your IP address, subnet mask and default gateway.
The click Use the following DNS server addresses adn fill in 1 or 2 DNS IP addresses
Check the box Validate settings upon exit and click OK to save.

![Step 19](./images/active_directory_step_19.png)

Once verified you had no issues with your settings, open the command prompt again and ping a website, I used www.google.com.  This is to verify we have an internet connection and that the TCP/IP stack is working on your device.

You can also ping your router, even though it should still work if you can access www.google.com.  But if you could not reach google.com the ping to your router is a good first step in troubleshooting.

![Step 20](./images/active_directory_step_20.png)

Next you will have to change the host name of your computer.  You can do this multiple ways:
1. Click on local server of the dashboard on the left side -> click on the computer name -> click Change...
2. Right click the start button and click System -> Scroll down on the right side and click Advanced sytem settings -> click Computer Name Tab at the top -> click Change...
3. search "about" in the taskbar search box -> Scroll down on the right side and click Advanced sytem settings -> click Computer Name Tab at the top -> click Change...
Once here, change the Computer name to identify your host name, we will change to a domain name later.  Cllick OK then Close and allow the computer to reload for the changes to take effect.

![Step 21](./images/active_directory_step_21.png)

![Step 22](./images/active_directory_step_22.png)

Now we will add the Active Directory Domain Services and DNS on this system.  Click at the top where it says manage and click Add Roles and Features

![Step 23](./images/active_directory_step_23.png)

Add this feature as a Role based installation and click Next.

![Step 24](./images/active_directory_step_24.png)

Select your host and make sure the IP address is still the same as the static one you set up earlier.  Then click Next

![Step 25](./images/active_directory_step_25.png)

For server roles check DNS and add features that are needed and also check Active Directory Domain Services and add its features.  Then click Next.

![Step 26](./images/active_directory_step_26.png)

Follow through the prompts and you will then install these roles and features once the installation is complete you can close out of this window or click **Promte this server to a domain controller**

![Step 27](./images/active_directory_step_27.png)

To promote this server to a domain controller click under the notification flag and click **Promote this server to a domain controller**

![Step 28](./images/active_directory_step_28.png)

For your domain controller select add a new forest and give your domain a domain name. This is up to youi what you want your domain to be named.

Choose the highest level Forest and Domain functional level your Server OS version can be.
Keep the capabilities as default.
Create a Directory Services Restore Mode (DSRM) password.  This is used if you need to log in to recovery mode on the server or are not able to log in to active directory with your normal password such as for a forest or domain restore.

![Step 29](./images/active_directory_step_29.png)

Keep the NetBIOS default.

![Step 30](./images/active_directory_step_30.png)

Keep the file paths as default.

![Step 31](./images/active_directory_step_31.png)

Next there will be a Prerequiste Check screen.  Making sure that your system is able to to be pushed as a Domain Controller and if there are any errors you need to address.
If all looks good, click Install and your system will restart

![Step 32](./images/active_directory_step_32.png)

Once restarted, you will be able to log in to your domain under the Administrator using your password you created.

![Step 33](./images/active_directory_step_33.png)
![Step 34](./images/active_directory_step_34.png)

Go back to your command prompt and run ipconfig /all.  Check to make sure the IP address is correct, subnet mask, and default gateway are also correct.
You may noticed the DNS server is 127.0.0.1 which is good because we set our machine up as a DNS server.  This is pointing the DNS server to our IP address.

![Step 35](./images/active_directory_step_35.png)

Go to Open your active directory by going to the start menu -> Windows Administrative Tool -> click Active Directory Users and Computers

![Step 36](./images/active_directory_step_36.png)

In here expand your domain on the left side and locate Domain Controllers.  Click on the Originizational Unit named Domain Controllers and check to see if your device is under this area.

![Step 37](./images/active_directory_step_37.png)

Go back to Windows Administrative Tools and click on DNS

![Step 38](./images/active_directory_step_38.png)

Expand your machine on the left side then the forward lookup zones and click on yopur domain.  Under your domain, check to see if there is a Start of Authority (SOA), a Name Server (NS) and a Host (A) record.  
The A record should have your IP address under the Data table.

![Step 39](./images/active_directory_step_39.png)

We will now install the role of DHCP on the server to handle distributing IP addresses to computers under our network.
Click manage at the top of the server dashboard and select add roles and features.  From the drop down click DHCP server and install any features it may need.
Run through the prompts keeping everything as default and click install.

![Step 41](./images/active_directory_step_41.png)

Once the installation of the DHCP role is complete click close.

![Step 42](./images/active_directory_step_42.png)

To complete the DHCP configuration, click under the flag notification and click Complete DHCP configuration.

![Step 43](./images/active_directory_step_43.png)

Click on start and go to Windows Administrative Tools and click DHCP

![Step 44](./images/active_directory_step_44.png)

Expand the domain controller and right click on IPv4 and click New Scope.
We will now make our range of addreses that we want to assign to computers when they are joinging our network.
This scope can be changed however you see fit.

![Step 45](./images/active_directory_step_45.png)

Give your scope a name.

![Step 46](./images/active_directory_step_46.png)

Set the range of total IP address for the network and then set the network mask length.

![Step 47](./images/active_directory_step_47.png)

Add exclusions in scope range if you would like.  These would be used for devices that would be on the network for a long time or should not have a dynamic IP addresses.

![Step 48](./images/active_directory_step_48.png)

Assign the default gateway that each device will use when they log on to network.

![Step 49](./images/active_directory_step_49.png)

Your domain name and DNS servers for the scope can stay as defaults.

![Step 50](./images/active_directory_step_50.png)

Click that you would like to activate this scope now.

![Step 51](./images/active_directory_step_51.png)

Go back to DHCP and check under IPv4 then scope and address pool.  You shoudl see the scope you just created.

![Step 52](./images/active_directory_step_52.png)

Lets add another User this will be another Domain Administrator to help look over the domain.
Open Active Directory Users and Computers, highlight Users and click create a new user in the current container at the top.

![Step 53](./images/active_directory_step_53.png)

After adding a user fill out the information such as name and logon name.

![Step 54](./images/active_directory_step_54.png)

Then provide a password, can be reset their next logon or you can assign a password they will just use.
Click Next to create the user.

![Step 55](./images/active_directory_step_55.png)

To add a user to a group go ahead and right click on the user and in the drop down click Add to a group...

![Step 56](./images/active_directory_step_56.png)


To add to a group enter the name of the group you would like to add the user to.  Click check names to make sure the correct group shows up.  Then click ok.

![Step 57](./images/active_directory_step_57.png)

Open up your network settings and check that all the IP address information is the same.  Just a nice double check.  Before we log out as Administrator and log in as our user.

![Step 58](./images/active_directory_step_58.png)

Click start -> click the user profile image at the top -> click sign out

![Step 59](./images/active_directory_step_59.png)

Log in as the new user you created with there "username"@"domain" then type in the password.  
I set it up so the user will have to make a new password

![Step 60](./images/active_directory_step_60.png)

Click OK to set up a new password

![Step 61](./images/active_directory_step_61.png)

Set the password and then log in.

![Step 62](./images/active_directory_step_62.png)


