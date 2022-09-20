# Care and feeding of DragonOS.   
   
Navigation: [home](README.md)  

No matter your interest in AERO data, be it HF-DL, VHF ACARS, L-Band Data, L-Band voice, Iridium, C-Band Data or C-Band voice or any combination (up to your CPUs ability to keep up), if you are running Linux, DragonOS should be strongly considered as you go-do distro to get up and running.  
To this end, this page will try and help smooth out that process.   
## DragonOS or Windows?   
Lets get this out the way first.  
If you only want to run SDRReciver and Jaero (For C or L-Band work), you can do that on Win7, Win10 or Win11. Both program's _require_ a desktop GUI, both run fine under Windows.  
acarsdeco, dumpVDL2, dumpHFDL and Iridium on the other hand, do not use any graphics / desktop at all, they are all command line programs and all of them _only_ run under Linux.    
## Raspberry Pi or old PC/Laptop?  
There are two builds of DragonOS, one for the Pi4 (DragonOS_Pi64) and one for PC's and laptops (DragonOS_Focal).   
If you want to erase Windows and put DragonOS on an old bit of hardware, thats your call. The old laptop/PC should have more bang for the CPU buck than the Pi, so you might be able to run more programs at once. (Jaero, Iridium and dumpHFDL are CPU intensive - you cant run any more than one of these at a time on a Pi4 for example - and Iridium on a Pi4 is next to useless).    
## DragonOS_Focal on a VMware machine   
Since Iridium (and dumphfdl to some extent) is very CPU intensive and requies a USB 3.0 port, a few of the bleeding edge Satcom crew are running DragonOS_Focal on their Windows PCs - often a powerful multi-core computer with a healthy amount of RAM that is somewhat lightly loaded.   
To do this download the free VMware player, create a new Ubuntu64 machine with 32gig hard drive and as many cores as you like (I suggest 4 is a good start). Point it to the Dragon ISO and once its booted up, simply install it from the live desktop icon.    
You can then reboot the VM into DragonOS and when you connect your 10Mhz bandwdith (or HF) SDR, VMware will ask if you want to mount it on the Host PC or the VM, chose VM and you are up and running.   
## DragonOS on a Pi 4   
It seems from early adopters / testers that the Pi 4 with 4 gig of RAM is plenty (2 gig RAM is a bit light on, and 8 gig of RAM is a waste of money - the CPU will max out long before the RAM will).   
Start by downloading the latest image of DragonOS and burn it to a 32 Gigabyte (minimum) microSD card.  
From here on this page is about getting set up and running on a Pi 4, so that should be noted.
<https://sourceforge.net/projects/dragonos-pi64/>   
Burn it using your tool of choice.   
Note that SSH is enabled by default.
## Enable HDMI
Once the image is burnt, open up the `usercfg.txt` and make sure that `hdmi_force_hotplug=1` is uncommented.   
To that same file, just below that line, add `hdmi_group=2` and on the next line add `hdmi_mode=82` (this adds a monitor resolution of 1920x1080, use mode=47 for a 1440x900 monitor, mode=35 for a 1280x1024. You can look up other modes from this table [here](https://www.raspberrypi.com/documentation/computers/config_txt.html#:~:text=These%20values%20are%20valid%20if%20hdmi_group%3D2%20(DMT)%3A))  
Now you can unmount the microSD card and put it in the Pi 4.   
## Headless Setup
Once that is done insert it into your Pi 4 and power up.   
Make sure you are connected to an Ethernet port the first few boots. Once you can VNC in, then you can join your wifi.   
You will need to find the IP address the Pi got from your router. You can look on your router or Fingbox or network scanning app on your phone or PC and find the IP address the Pi was given on your network and shell (MobaXterm, PuTTY or Power Shell are my go-tos in that order) into the Pi using the default user/pass of ubuntu / dragon  

Note. You must shell in and do the following commands before you can VNC to the desktop.
## Run raspi-config

Once you are in shell, run `sudo raspi-config` and from there the first thing I do is to [set the time to UTC](raspberrypi.md), expand the file system to the full SD card and turn on the VNC server. None of these three things are optional. Of course you can also change the hostname and any other tweaks you might know of, but those 3 things a must-do in my setup.   
I _do not_ recommend changing the default *username* of `ubuntu`. If you do, know what you are doing as a lot of paths and system settings are going to change. Changing the *hostname* (as it will show on your network) is fine and probably recommended depending on how many 'ubuntu' hosts you currently have on your network.   
After setting those 3 values, reboot and log back in with shell.  
### Enable auto login    
Once back in, we need to enable auto desktop log in, this is critical for VNC to to work.    
`sudo nano /etc/gdm3/custom.conf` in that file, uncomment the auto log in line and uncoment the user name and change it from user1 to ubuntu.   
It should look like this:   
```
# Enabling automatic login
  AutomaticLoginEnable = true
  AutomaticLogin = ubuntu
  ```   
Reboot the pi and log in via your VNC client.
   
## VNC server
Enable cut/paste in VNC by adding ubuntu as a user in the VNC server.   
Note that you should be able to connect to this VNC server no matter what VNC client you use, TIGHTVNC or OpenVNC for example.  
Some people are having a lot of trouble getting the native VNC Server working. If this is the case, go to the applications 'store' and search / install X11VNC and that should get you up and running. Note, you don't have to install VNC at all if you don't want. We are just finding a lot of people want to run the Pi headless.   
Lastly, some have found that buying and using a fake HDMI adaptor helps the Pi run headless with good screen resolution.

### Enable Wifi
If you must (I really don't like or trust any wifi on any Raspberry Pi. Have been burnt by its ultra poor performance far too many times) enable and join your wifi from the desktop. NOTE: this is the best way to get wifi going on DragonOS at this time - the usual Pi methods of wpa_suplicent don't work on the Dragon.
    
## *Read* the start up doc on desktop   
Be sure - this is not optional - and read the start up doc on the desktop.   
It has notes on enabling SDRPlay devices and many other DragonOS specific notes you *will* want to read.
If you have an Airspy device: `cd /usr/src` and then `./SDRplay_RSP_API-ARM64-3.07.1.run`
## Jaero Software - Quick start    
**Note!** dumphfdl, dumpvdl2 and SDRReceiver are all command line only programs. They do not have menu items.   

Very quick start guide for SDRReceiver on DragonOS:  
`mkdir sdrrini`  
`cd sdrrini`  
`nano 25.ini`  
Cut paste or type your SDRR settings. To save crtl+o then ctrl+x   
`SDRReceiver -s 25.ini`   
    
That will get SDRRx running with your ini file. Of course name the file your satellite and make sure the .ini settings match your satellite.

For L-Band work, start SDRReceiver from the terminal using your .ini file.  
`SDRReceiver -s 98w.ini`  
Start a single instance of Jaero from the DragonOS menu.   
Start many Jaeros from another terminal by making a `jaerostart.sh` file setup as follows:    
`nano jaerostart.sh` then add the following.   
```    
jaero -s VFO01 &   
jaero -s VFO02 &   
jaero -s VFO03 &   
```   
Save with ctrl+o and then exit with ctrl+x   
**BIG NOTE** you need to run each jaero from the terminal with the -s and VFO number and adjust its settings, then click its 'File->Exit' menu before you run that script. You will get a ton of odd errors if you don't. You only have to run each one one at a time the first time, from then on out, you can just run this bulk start script.  

Add as many instances of Jaero as you need. BE SURE and turn off logging and voice decoding in each when running on a Raspberry Pi. Those two features use a lot of CPU and will cause bad/dropped decodes.   

Once you create that .sh file, make it executable by the command `sudo chmod +x jaerostart.sh`   
Then run it with `./jaerostart.sh`
    
   
## dumpxxxx quick start  
For dumpVDL2 and dumphfdl, run them from a terminal. They are not in the DragonOS menu. Just run them from the terminal prompt.

Quick and dirty guide to get you going, more to come on each of these....  

For dumpvdl2, just open a terminal on the desktop, plug in your RTLSDR v3 dongle connected to the Pi and 136mhz antenna connected and enter this command into the terminal:   
`dumpvdl2 --msg-filter all,-avlc_s,-acars_nodata,-gsif,-x25_control,-idrp_keepalive,-esis --rtlsdr 2 --gain 40 --correction -1 --output decoded:text:file:path=vdl.log,rotate=hourly 136650000 136975000 136800000`   
Then to see the messages, do a tail on the log file it creates in your home directory.   
(I don't log locally, since I use Node-RED).   
Set your gain and correction as required by your station - max gain is not always the best. Correction will depend on your dongle. The dumpvdl message headers have important information to help adjust these. More to come.   
Those are the three frequencies in use on mainland USA. Adjust them as per this [table](https://app.airframes.io/about#:~:text=you%20receive%20traffic.-,VDL%20(VHF%20Data%20Link),-We%20currently%20support) and your location (note, you might need more than three, but don't add them needlessly as the more you scan, the more the CPU is taxed. Also note that I don't use acarsdeco2 and can not help with that program, dumpvdl2 works better for my needs and has a richer output).   
If you want to feed a website or Node-RED:   
`dumpvdl2 --msg-filter all,-avlc_s,-acars_nodata,-gsif,-x25_control,-idrp_keepalive,-esis --rtlsdr 2 --gain 40 --correction -1 --output decoded:text:udp:address=thebaldgeek.net,port=xxxxx 136650000 136975000 136800000`
Where xxxxx is the port number of the website.   
My URL is there as an example, but it could be an IP address of a local computer on your network or even localhost if you are running Node-RED on the same PC.

For dumphfdl, run the command to install the RSPlay API as per the desktop text document. Then plug in your RSP1a (or RSPlay SDR) and run the command:   
`dumphfdl --soapysdr driver=sdrplay --sample-rate 250000 8834 8885 8894 8912 8912 8927 8939 8942 8948 8957 8977 --output decoded:text:file:path=hfdl.log,rotate=hourly --device-settings rfnotch_ctrl=false,dabnotch_ctrl=false`   
Note that you might get an error the first time your run this, just press up arrow and run the command again. (It takes a moment for the SDRPlay API to start)   
Then to see your logs, you can do a tail on the log file it creates in your home directory.   
Change the HF frequencies for time of day and your location or ground stations of interest (this is a work in progress for me and I will be using Node-RED to control dumphfdl frequency sets).   

In both dump programs you can have more than `--output` option, so you can for example, log locally and forward to a website without any issues.    
      
<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-HGJWTNL65R"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'G-HGJWTNL65R');
</script>