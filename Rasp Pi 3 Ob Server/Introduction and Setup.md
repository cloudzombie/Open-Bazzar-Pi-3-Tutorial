# Introduction


> *This is a multi-step to running Open Bazaar on a Raspberry Pi 3. This tutorial is easier if you have a secondary display to plug your Raspberry Pi 3 into until fully configured.*  



#####This is assuming a person with no cli skills whatsoever, to get a new Raspberry Pi 3 running Open Bazaar Server client locally. 


First thing is first, you need to power on your Pi and connect it to the internet. This tutorial is assuming your host computer is Windows, but the steps are the same regardless of OS. 


Now that your Pi is up and running and connected to your display, lets go ahead and open up the Terminal and update it.



```sudo apt-get update```


If prompted hit yes, when it finishes we are going to go ahead and configure some things on the Pi that need to be done. 
 

Open the Menu.


    MENU > PREFERENCES > Raspberry Pi Configuration 


In the System tab, change the Password, don't forget it! and Hostname to whatever you desire. I leave the "Login as user "pi" Checked or the Auto-login.  


Then goto the Localisation tab, set your Locale, Timezone and Keyboard to your geographic area. 


Go back to the System tab, click "Expand Filesystem" This will open up any remaining space on the micro SD card for the OS and any processes we run. 



The Pi will want to reboot here, let it then once you are logged back in, open the Terminal back up. Next we are going to setup an SSH tunnel in part 2. 
