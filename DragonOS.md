# Care and feeding of DragonOS.   
   
Navigation: [home](README.md)  

No matter your interest in AERO data, be it HF-DL, VHF VDL2, L-Band Data, L-Band voice, C-Band Data or C-Band voice or any combination (up to your CPUs ability to keep up), if you are running Linux, DragonOS should be strongly considered as you go-do distro to get up and running.  
To this end, this page will try and help smooth out that process.   
    
Start by downloading the latest image of DragonOS and burn it to a 32 Gigabyte (minimum) microSD card.  
This page is about getting set up and running on a Pi 4, so that should be noted.
<https://sourceforge.net/projects/dragonos-pi64/>   
Burn it using your tool of choice.   
## Enable SSH
Once the image is burnt, add a file to the root partition called 'ssh' with no extension. (Hint, if you are on a Windows PC, if the image burner has 'ejected' the microSD card, take it out and put it back in again to remount it).   
In Windows File Explorer right click on a empty place on the drive and select 'New Text document'. Remove the .txt extension and so the file is just `ssh`   
Now you can unmount the microSD card and put it in the Pi 4.   
## Headless Setup
Once that is done insert it into your Pi 4 and power up.   
Here you have two options, you will need a monitor, keyboard and mouse to setup full headless initially, so you can find the IP address the Pi got from your router via a terminal session, or you can look on your router or Fingbox or network scanning app and find the IP address the Pi was given on your network and shell (MobaXterm, PuTTY or Power Shell are my go-tos in that order) into the Pi using the default user/pass of ubuntu / dragon  

Once you are in using either method, run `sudo raspi-config` and from there the first thing I do is to [set the time to UTC](raspberrypi.md), expand the file system to the full SD card, turn on the VNC server and lastly set a default screen resolution so you can VNC in without a monitor connected. In my setup, none of these four things are optional. Of course you can also change the hostname and any other tweaks you might know of, but those 4 things a must-do in my setup.   
Next is to add is my ZeroTeir network...  
## ZeroTeir ##
I access all my local and remote Pis (and a few Windows PCs needed for Jaero etc) via ZeroTier.com and can not speak more highly of it. (Its simply a small VPN - Virtual Private Network - a secure tunnel over any network, including the Internet).  
Here is how to quickly install it on a fresh Pi:  
`curl -s https://install.zerotier.com/ | sudo bash`  
`sudo systemctl enable zerotier-one`  
`sudo zerotier-cli status`  
`sudo zerotier-cli join YourZeroTeirNetworkID`  
Authenticate and name this Pi by going to your network on their website then continue.  
`sudo zerotier-cli listnetworks`  
`sudo touch /var/lib/zerotier-one/networks.d/YourZeroTeirNetworkID.conf`    
   
## VNC server
Next up, is the VNC server so we can run the Pi headless. 
For this you will need a monitor and keyboard on the Pi, from the desktop, click on the VNC icon on the task bar and turn off encryption and set a VNC password.   
Thats it, we are done with the screen, keyboard and mouse, from here on, I remote into the Pi with it on my network at the best location for the coax and SDR dongle I am using.   
    
## Start up doc on desktop   
Be sure - this is not optional - and read the start up doc on the desktop.   
It has notes on auto login, SDRPlay devices and many other DragonOS specific notes you *will* want to read.
