# Open Bazaar Server


Alright now it's time for what everyone is here for, installing Open Bazaar! Open up your terminal and type 


```sudo apt-get install -y git python-dev libffi-dev libssl-dev python-setuptools nano ```

```sudo easy_install pip```

```git clone https://github.com/OpenBazaar/OpenBazaar-Server.git
cd OpenBazaar-Server/```

```sudo pip install -r requirements.txt```


# Set a Custom Username and Password for your Open-Bazaar Server


Still in the terminal type 


```sudo nano ob.cfg```


    #USERNAME=joebloggs 
	#PASSWORD=aVeryLong&Cmpl1cat3d5tringThatW1llBeVeryHardToGue$5


Change the username to whatever you want as well as a very strong password. I reccomend using [bitaddress.org](https://bitaddress.org "bitaddress") and using a combination of the randomly gnerated private key and unique phrases for your password.  


Remember to uncomment the lines in question (i.e. remove the leading # symbols on ). 


#Run the Server 


```python openbazaard.py start -d -a 0.0.0.0```

Optionally if you want to see information for degub etc you can run 

```python openbazaard.py start -loglevel info -a 0.0.0.0```

Congratulations! You know have Open Bazaar Server running on a Raspeberry Pi 3. Your store will not remain visible as long as it is left running. It is also easy to manage as you can use SSH and either PuTTy or Remote Desktop in for maintenance and management. 


Thanks for reading! Please leave comments and feedback below. 