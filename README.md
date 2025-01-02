# Installing Active Directory

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

![Step 18](./images/active_directory_step_18_red_lined.png.png)

Back in your Internet Protocol Version 4 (TCP/IPv4) Properties, click Use the following IP address.
Enter in your IP address, subnet mask and default gateway.
The click Use the following DNS server addresses adn fill in 1 or 2 DNS IP addresses
Check the box Validate settings upon exit and click OK to save.

![Step 19](./images/active_directory_step_19.png)

Once verified you had no issues with your settings, open the command prompt again and ping a website, I used www.google.com.  This is to verify we have an internet connection and that the TCP/IP stack is working on your device.

You can also ping your router, even though it should still work if you can access www.google.com.  But if you could not reach google.com the ping to your router is a good first step in troubleshooting.

![Step 20](./images/active_directory_step_20.png)
![Step 21](./images/active_directory_step_21.png)
![Step 22](./images/active_directory_step_22.png)
![Step 23](./images/active_directory_step_23.png)
![Step 24](./images/active_directory_step_24.png)
![Step 25](./images/active_directory_step_25.png)
![Step 26](./images/active_directory_step_26.png)
![Step 27](./images/active_directory_step_27.png)
![Step 28](./images/active_directory_step_28.png)
![Step 29](./images/active_directory_step_29.png)
![Step 30](./images/active_directory_step_30.png)
