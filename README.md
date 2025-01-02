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
![Step 10](./images/active_directory_step_10.png)
![Step 11](./images/active_directory_step_11.png)
![Step 12](./images/active_directory_step_12.png)
![Step 13](./images/active_directory_step_13.png)
![Step 14](./images/active_directory_step_14.png)
![Step 15](./images/active_directory_step_15.png)
![Step 16](./images/active_directory_step_16.png)
![Step 17](./images/active_directory_step_17.png)
![Step 18](./images/active_directory_step_18.png)
![Step 19](./images/active_directory_step_19.png)
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
