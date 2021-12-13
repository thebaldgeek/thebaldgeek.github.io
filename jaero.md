# Ins and outs of Jaero.   
   
Navigation: [home](README.md)  

The core of this whole C-Band and L-Band project is the software called Jaero.  
This page will grow over time. Check back now and then.  
## Download Jaero   
(To use Jaero on Linux, check out [DragonOS](DragonOS.md))   
Use the November 2021 1.0.4.13 dirty version, you don't need to install it, just run it from the directory you unzip it from.  
This version fixes a lot things and most importantly it uses the latest libacars-2 version which itself has a lot of updates and bug fixes. It also allows you to use BaseStation.sqb for its logging aircraft database lookup (If you must log).   
The 1.0.4.13 version of Jaero adds the ZMQ input for data. You should be using at least this version. There is a how-to page for setting up SDRReceiver on Windows or Linux [here](SDRReceiver.md)   
    
# Getting Jaero  

Once you have that running, the next thing is to setup Jaero to connect to the VFOs.   
To download Jaero: <https://github.com/jontio/JAERO/releases>  
Just at the bottom of the top list of bullet points, there is a section called 'Assets 4'.   
Click to download the win_x86 file.  

## Starting and setting up Jaero  

Here is where things change a little bit and for the better honestly....  
Unzip it somewhere on your drive, like in the downloads is a good place.  
It will make a directory with a longish name, and then under that directory, a nice clean 'jaero' directory.  

I would leave it there as we no longer need to install Jaero and we can run where it is.  
(This will also leave your current Jaero install untouched and so you can always go back if you miss the old ways).  

Its pretty important on how to start Jaero.  
I don't know what satellite you are looking at, so I don't know how many VFO's you will need in your startup bat file. Just keep in mind you need to start as many Jaeros as you have VFOs or VACs.  

*IN THE SAME* folder as Jaero, create a new text file, I called mine `startJaero.bat`  

The .bat is the important bit. Your Windows Explorer might call it .bat.txt but hide the .txt so watch out for that. Unlike the .ini file where it did not matter if Windows called it .ini.txt, in the case of a batch file (dot bat), it matters a lot.   
Right click the new file and select Edit.   
Paste in the following:   

```
@ECHO OFF
start "VFO01" "JAERO.exe" "-s VFO01"  
start "VFO02" "JAERO.exe" "-s VFO02"  
start "VFO03" "JAERO.exe" "-s VFO03"  
start "VFO04" "JAERO.exe" "-s VFO04"  
start "VFO05" "JAERO.exe" "-s VFO05"  
start "VFO06" "JAERO.exe" "-s VFO06"  
start "VFO07" "JAERO.exe" "-s VFO07"  
start "VFO08" "JAERO.exe" "-s VFO08"  
start "VFO09" "JAERO.exe" "-s VFO09"  
start "VFO10" "JAERO.exe" "-s VFO10"  
start "VFO11" "JAERO.exe" "-s VFO11"  
start "VFO12" "JAERO.exe" "-s VFO12"  
start "VFO13" "JAERO.exe" "-s VFO13"  
start "VFO14" "JAERO.exe" "-s VFO14"  
start "VFO15" "JAERO.exe" "-s VFO15"  
start "VFO16" "JAERO.exe" "-s VFO16"  
start "VFO17" "JAERO.exe" "-s VFO17"  
start "VFO18" "JAERO.exe" "-s VFO18"
  ```
Now save it.  

What we are doing is running Jaero from the same directory as the .bat file is in.  
This saves a whole lot of pathing issues.  
Also, we are starting the 18 of them that are probably in your .ini file (adjust the length to match your ini file).  
   
Ok, with SDRReceiver running, double click on the startJaero.bat file and wait till all 18 start up.   
Don't worry, they don't have a waveform yet, that's next.   
   
Now, click on the first Jareo and then click on the gear icon.  
Adjust things to your liking from top to bottom.   
   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/jareonumbers.png" height="580">  
  
  Looking at the settings top to bottom - a quick overview.

1. This just hides these message types from the live display window. Most people leave it as those listed messages can be hard to read or understand their purpose.  
2. This changes the format of the message in the main window, play around when you get it running, most people like format 3. If you are a software programmer, you might like the JSON option from this list - note, you can only select one message format type.  
3. Most people leave this checked. It seems the non text messages are link Pings or ACKs for L/C-Band messages and other system stuff that is not of interest to (most) humans.
4. Beeps are annoying when you get 18 Jaeros running - uncheck it for sanity.
5. This sends the ACARS messages to another computer using UDP (For example PlanePlotter or Node-RED or a remote site). Note that Jaero can not use host names here, it must be an IP address and port number. Leave a space, then put in the next IP:port if you want to feed more than one server the ACARS messages.  
6. Is for when you have a satellite dish and are using Jaero on C-Band. This is the IP and port for your VRS or tar1090 to plot the aircraft positions on a map. (Not used on L-Band since there is no position data).  
7. Check it if you must log, it will slow down the starting of Jaero the longer it runs. It will also drive you nuts trying to view the logs of 18 different Jaeros. Review the Node-RED page and see that there is a better way to build custom logs.
8. If you have a VRS with images, you can pick them up here if you are logging.
9. Never thought we would get here did you.... 
Check your ini file as it shows: zmq_address=tcp://*:6003 (Note, some of the .ini files have different port numbers, thats fine, just be sure to match port for port. The port in your .ini must match the port you use in your Jaeros).  
Again, the port number and VFO number are important. So in each jaero Check the ZMQ box and just put your home IP of `tcp://127.0.0.1:6003` and again, make sure the port matches your ini file.  
Lastly, the topic. In your .ini file each VFO has a name, you must make sure that the name in JAERO matches the names in the ini. If you have used the .ini file and the startJaero batch file I have here, they should be very close.  
Also **WATCH OUT!** Jaero likes to put a space at the start of the word VFO!! So **make sure** that the V is tucked up against the edge of his box!!!! (Ask me how I know this!!!!!!!!!! - No don't)  

For the tabs on the top, I like turn off logging and turn off voice decoding. You may do otherwise, but if you just want the data, logging and voice use up CPU that you don't need to waste for just getting data.   

Click Ok. Last few things to do here... make sure you select the right data rate in Jaero that matches the VFO in the ini file for that VFO.  

Click the blue bump to move the pale green box over it so it will start to decode.  

Lastly, click the black CPU square to turn it green and save some computer power (It just slows down the blue wave form update - but is well worth enabling this CPU reduction feature) and if you want to save even more CPU, select "None' from the drop down list under the constellation to turn that off. Make sure AFC is on.  

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/jaerocpusavemodes.png" height="400">   

Now, minimize that Jaero, and do that all over again on the next 17. Making sure you get the next VFO number and its matching decode rate.  
Each one will save its settings when you close it, so next time, just double click the start batch file and you will be up and running in a few seconds.

### Logging in Jaero
basestation.sqb. This is a pseudo 'standard' of aircraft details database. As Jaero decodes aircraft messages, it looks up each ICAO (Jaero calls them AES) in the database and provides type and owner information in its log file. If you are going to use Node-RED to track the aircraft, skip this step.   
The basestation.sqb file that this version of Jaero includes has around 188,000 aircraft details, but we can quickly do better.    
Visit the flightairmap page and download their basestation.sqb file: <https://data.flightairmap.com/>  
The link is at the bottom of that page.   
Unzip it on your computer and copy the file to your Jaero subdirectory and replace (over write) the one in there. The flightairmap database has 380,000 aircraft, so almost double the chances of Jaero showing the information for any satcom ACARS messages you decode.   
If you are using Node-RED I will walk you through building an even larger database with around 558,000 aircraft details. Or you can get creative and modify your own database to use with Jaero.    
    
Once you have copied the database over, you can now double click Jaero.exe and run it.   
But lets just do one more tweak for those of you running standalone (ie, no Node-RED) and want to see some aircraft logs/details.   

### Jaero Log Link   
Click on the gear icon, then click on the second tab in the settings, the 'Log Window'.   
Here you will see the link that will be opened in your web browser when you click on the aircraft drawing in the Jaero log.   
Out of the box it is set to: `http://www.flightradar24.com/data/airplanes/{REG}`  
This is Ok for some people, but many would rather it open to ADSBExcahnge, good news, we can change it.    
Delete the fightradar24 link and replace it with: `https://globe.adsbexchange.com/?icao={AES}`   
Now when you click on that drawing (and first highlighting the aircraft of interest in the Jaero log list), you will open that aircraft last known position on the ADSBExchange map.   
If you are going to be using Node-RED, I will show you how to make those links in a function node so we can skip this step.


<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-HGJWTNL65R"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'G-HGJWTNL65R');
</script>