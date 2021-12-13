# Care and feeding of DragonOS.   
   
Navigation: [home](README.md)  

No matter your interest in AERO data, be it HF-DL, VHF VDL2, L-Band Data, L-Band voice, C-Band Data or C-Band voice or any combination (up to your CPUs ability to keep up), if you are running Linux, DragonOS should be strongly considered as you go-do distro to get up and running.  
To this end, this page will try and help smooth out that process.   
## DragonOS or Windows?   
Lets get this out the way first.  
If you only want to run SDRReciver and Jaero (For C or L-Band work), you can do that on Win7, Win10 or Win11. Both program's _require_ a desktop GUI, both run fine under Windows.  
dumpVDL2 and dumpHFDL on the other hand, do not use any graphics at all, they are both command line programs and more so, both only run under Linux, for VHF and HF ACARS, you must go the Linux route.    
## Raspberry Pi or old PC/Laptop?  
There are two builds of DragonOS, one for the Pi4 and one for PC's and laptops.   
If you want to erase Windows and put DragonOS on an old bit of hardware, thats your call. The old laptop/PC should have more bang for the buck than the Pi, so you might be able to run more programs at once. (Jaero and dumpHFDL are CPU intensive - you cant run both on a Pi4 for example).    
## DragonOS on a Pi 4   
It seems from early adopters / testers that the Pi 4 with 4 gig of RAM is plenty.   
Start by downloading the latest image of DragonOS and burn it to a 32 Gigabyte (minimum) microSD card.  
From here on this page is about getting set up and running on a Pi 4, so that should be noted.
<https://sourceforge.net/projects/dragonos-pi64/>   
Burn it using your tool of choice.   
## Enable SSH and HDMI
Once the image is burnt, add a file to the root partition called 'ssh' with no extension. (Hint, if you are on a Windows PC, if the image burner has 'ejected' the microSD card, take it out and put it back in again to remount it).   
In Windows File Explorer right click on a empty place on the USB boot drive and select 'New Text document'. Remove the .txt extension and so the file is just `ssh`  
Once that is done, open up the `usercfg.txt` and make sure that `HDMI_force_hotplug = 1` is uncommented.   
To that same file, just below that line, add `Hdmi_group=2` and on the next line add `Hdmi_mode=82` (this adds a monitor resolution of 1920x1080)  
Now you can unmount the microSD card and put it in the Pi 4.   
## Headless Setup
Once that is done insert it into your Pi 4 and power up.   
You will need to find the IP address the Pi got from your router. You can look on your router or Fingbox or network scanning app on your phone or PC and find the IP address the Pi was given on your network and shell (MobaXterm, PuTTY or Power Shell are my go-tos in that order) into the Pi using the default user/pass of ubuntu / dragon  
### Run raspi-config

Once you are in shell, run `sudo raspi-config` and from there the first thing I do is to [set the time to UTC](raspberrypi.md), expand the file system to the full SD card and turn on the VNC server. None of these three things are optional. Of course you can also change the hostname and any other tweaks you might know of, but those 3 things a must-do in my setup.   
After setting those 3 values, reboot and log back in with shell.  
### Enable auto login    
Once back in, we need to enable auto desktop log in, this is critical for VNC to to work.    
`sudo nano /etc/gdm3/custom.conf` in that file, uncomment the auto log in line and uncoment the user name and change it from user1 to ubuntu   
Reboot the pi and log in via your VNC client.
## ZeroTeir ##
Next is optional, but I always add my ZeroTeir network. (Its simply a small VPN - Virtual Private Network - a secure tunnel over any network, including the Internet)    

I access all my local and remote Pis (and a few Windows PCs needed for Jaero etc) via ZeroTier.com and can not speak more highly of it. .  
Here is how to quickly install it on a fresh Pi:  
`curl -s https://install.zerotier.com/ | sudo bash`  
`sudo zerotier-cli join YourZeroTeirNetworkID`  
Authenticate and name this Pi by going to your network on their website then continue.  
`sudo touch /var/lib/zerotier-one/networks.d/YourZeroTeirNetworkID.conf`    
   
## VNC server
Enable cut/paste in VNC by adding ubuntu as a user in the VNC server.

### Enable Wifi
If you must (I really don't like or trust any wifi on any Raspberry Pi. Have been burnt by its ultra poor performance far too many times) enable and join your wifi from the desktop. NOTE: this is the best way to get wifi going on DragonOS at this time - the usual Pi methods of wpa_suplicent don't work on the Dragon.
    
## *Read* the start up doc on desktop   
Be sure - this is not optional - and read the start up doc on the desktop.   
It has notes on enabling SDRPlay devices and many other DragonOS specific notes you *will* want to read.
