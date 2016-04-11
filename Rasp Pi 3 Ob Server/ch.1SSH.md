#  SSH

To log in to your Raspberry Pi remotely, you'll need the IP of the Raspberry Pi – this is basically like your house address and tells the host computer where to look for it on the network. By default, the Raspberry Pi will be given an IP automatically by the router (called Dynamic IP and denoted by DHCP) when you connect to a network. However, this can change whenever you remove the Pi from the network e.g. turn it off.

Having a static IP isn't essential, however it will make repeated access to the Raspberry Pi via SSH much simpler, as you'll always know that the Raspberry Pi has the same address. Imagine how much trouble your postman would have if your house constantly changed location :)

This task assumes that you have the official Raspian OS release installed. This is available in the NOOBS distribution and can be downloaded from http://www.raspberrypi.org/downloads. This guide also assumes that you've connected your Pi to a network via Ethernet. If you're going to be logging into your Pi remotely for most tasks, then I recommend it's easiest and fastest to plonk it next to your router, and use ethernet to access the internet anway!

A. Checking Set Up

Boot into Raspian and log in (Username. pi, Password. raspberry), this will all be command line stuff, so no need to log in to the GUI.

First, we need to list the network interface we currently have available:


    cat /etc/network/interfaces


The line . . . . 


    iface eth0 inet dhcp

Implies that we're currently getting out IP address via DHCP, meaning it's being dynamically registered by the router. This is what we want to change!

B. Gathering Information

Fist of all we need to grab some information from our router and Pi. There's a couple of command we need to run to get this info. Have a pen and paper handy! . . . 


    ifconfig



This reveals your router information, the bit you want is after eth0 (the ethernet connection). . . .

eth0      Link encap:Ethernet  HWaddr b8:27:eb:b3:fc:2c

               inet addr:192.168.1.81  Bcast:192.168.1.255  Mask:255.255.255.0

Write down the following information. . .
    
    inet addr – 192.168.1.81 (Pi's Current IP Address)
    
    Bcast –  192.168.1.255 (The Broadcast IP Range)
    
    Mask –  255.255.255.0 (Subnet Mask Address)

We need a little more information before we proceed. Use the command. . . 

    netstat -nr

(route -n will give you the same info.)


We need:
    
    'Gateway' Address – 192.168.1.254
    
    'Destination' Address – 192.168.1.0

C. Editing Network Configuration

We now need to plug this information into the Pi's network configuration file using a text editor. I always use nano text editor. . . 

    sudo nano /etc/network/interfaces



Simply change the line that reads:

**iface eth0 inet dhcp**

to

**iface eth0 inet static**

Then directly below this line enter the following (Please Note. You will need your own addresses we gathered in Part B, more details below). . . . 
    
    address 192.168.1.81
    
    netmask 255.255.255.0
    
    network 192.168.1.0
    
    broadcast 192.168.1.255
    
    gateway 192.168.1.254
     
To clarify what each part means. . . . 

**address** – The address you want to give your Pi, this can be any IP in the network range, but it's usually advisable to go higher rather than lower, or you could end up logging different devices to the same IP! I've selected 192.168.1.81, as we're already registered to that address (denoted by 'inet addr'), but this can be any IP address from the range192.168.1.1 to 192.168.1.255.

**netmask** – The 'Mask' address we wrote down earlier.

**network** – The router IP address, this is the 'Destination' Address was found earlier. You can also grab this off your router, it will say on the side somewhere.

**broadcast** – The 'Bcast' address we wrote down earlier. 

**gateway** – This is the 'Gateway' address we found earlier.





So, it should look something like the above, but with your values! Remember to save before exit, CTRL+X (exit) then yes to save changes!

D. Re-check Static IP Configuration

UPDATE: Remove any existing leases

    sudo rm /var/lib/dhcp/*

Then we'll need to reboot and check your changes. . . 

    sudo reboot

Log back in and run 

    ifconfig

Which should reveal your new settings. . 



To double checks all is working as it should, ping your 'Gateway' Address. . . 
    
    ping 192.168.1.254 -c 10

(the -c 10 command simply denotes that you want to ping it 10 times, if you forget to add this, it will ping the address continuosly. To stop it press CTRL+C)



This should ping successfully and all packets should be recieved. If something's not right double check through all your IP addresses, and make sure you're pinging the right address too. Remember you can always revert back to DHCP by reversing the steps. The 'network' router IP address is sometimes a little fiddly, so check that if you're still having issues!

Hopefully however, your Raspberry Pi is now set up with a static IP address!

