# How to use SDRReceiver to send data to Jaero.   
   
Navigation: [home](README.md)  
  
## The Old Way
The old way to send data from your SDR software to Jaero was to use virtual audio cables (VAC). This was very fragile, CPU intensive, expensive (a licensed copy of VAC was required) and each SDR software package had its up and down's. Issues ranged from unpredictable lockups/crashes, PC hangs, high CPU use, memory leaks, convoluted graphical interfaces and a lot of unneeded features (bloat). It also made the option of running on Linux just about impossible. With satcom you just need the aircraft data to be sent to each Jaero the most efficient way possible with out needing constant monitoring and restarts. Most systems even run headless and you never need to look at the actual SDR software for months at at time.   
  
In August 2021, a new SDR receiver and version of Jaero was released that solved all these issues.   
## Big Picture    
SDRReceiver uses an ini file to set its frequencies. It is not visual point-and-click software so will take some patience to get used to and get it dialed for your system. You put the center frequency in the text file, then sub VFO frequencies and name them, Jaero then picks up the data from the ZMQ data stream identified by the VFO names.  

This is critical and really important. All other SDR software requires an audio pipe from it to Jaero, SDRR uses a data pipe. The latter is a LOT more robust, light weight and far more accurate way to move data from the SDR dongle to Jaero.  
### The bottom line
There are two main parts to getting the whole system working, SDRReceiver and its ini file and starting Jaero with a batch file, setting up each Jaero with the correct port number and VFO name. Note, you only have to configure everything once. Once its all setup, its a simple double click to start everything up as needed.
## Install SDRReceiver on Windows  
(For running SDRReceiver on Linux, check out DragonOS).   
Visit the github page and download the Windows zip file.   
<https://github.com/jeroenbeijer/SDRReceiver>  
  
The download is on the right, click on the 'Releases', then on that page, at the bottom, click on 'Assets' and select the file with win_x86 in it.  
This will download it on your PC, once there, extract it into a directory of your liking. You don't have to install it, so it will be run from the directory you extract it. I simply left it in my downloads folder.  

## Satellite ini file     
Once you have downloaded and unzipped the receiver software, the next thing is to get your satellite ini file and copy or create it in the same directory as SDRReceiver.   
At the start of August, there are only a few ini files for the satellites. I hope that the community will share their files and we can have them all on this website to download.   
For now, there are a few here: <https://github.com/jeroenbeijer/SDRReceiver/tree/master/sample_ini>   
While you are there, be sure and check out the comments in the 98W ini file, the software author includes many helpful remarks about the required structure of the .ini file:
<https://github.com/jeroenbeijer/SDRReceiver/blob/master/sample_ini/sdr_98W.ini>  

The main missing one is L-Band for 143E. If you have it, please let me know.  

Download the .ini file into the same directory as your SDRReceiver unzipped into.   
Now, from Windows Explorer, hold down the right shift key on your keyboard and right mouse click on an empty part of the page to pull up the menu. From that pop up menu select either Open Command Prompt, or Open PowerShell Window Here. (depending on your version of Windows).   

That will open a back or blue box window, now start typing the command `SDR` and hit the tab key, this will auto complete the command to the .exe and then you just add `-s` and then name of your ini file.   

The full command is something like `.\SDRReceiver.exe -s 54w.ini` (Of course use your named .ini file).   
If you computer throws an error that it cant find the ini, then Windows might have saved it with a hidden .txt extension, so type this: `.\SDRReceiver.exe -s 54w.ini.txt` (Of course use the name of your .ini file)
It should work. If not, then you most likely did not put the .ini file in the same directory as the SDRReceiver software.  
      
You should now see a small spectrum window appear, click on the 'Start SDR' button and slowly the waveform will show up. If your SDR dongle requires bias-T to power an LNA, you can (if you are using an RTLSDRv3 silver dongle - hint, you should be) click the Bias-T button to turn it on.  
You should see something similar to what you are used to. Thin spikes from the 600/1200 channels on the left and fat spikes from the 10500 channels on the right.   

Do note that I have had issues using SDRReceiver with a NooElec SmarTee dongle (the ones with the bias-t always on), I use and recommend the flat silver RTLSDR v3 dongles.    
## Starting Jaero  

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

Now, the real key seems to be how to start Jaero.  
I don't know what satellite you are looking at, so I don't know how many VFO's you will need in your ini file. Just keep in mind you need to start as many Jaeros as you have VFOs in your SDRR .ini file. (You don't have to, but it would be nice to get all the data right?).   

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
  
  Looking at the settings top to bottom - a quick overview. More details on the [jaero](jaero.md) page.    

1. This just hides these message types from the live display window. Most people leave it as those listed messages can be hard to read or understand their purpose.  
2. This changes the format of the message in the main window, play around when you get it running, most people like format 3. If you are a software programmer, you might like the JSON option from this list - note, you can only select one message format type.  
3. Most people leave this checked. It seems the non text messages are link Pings or ACKs for L/C-Band messages and other system stuff that is not of interest to (most) humans.
4. Beeps are annoying when you get 18 Jaeros running - uncheck it for sanity.
5. This sends the ACARS messages to another computer using UDP. Note that Jaero can not use host names here, it must be an IP address and port number. Leave a space, then put in the next IP:port if you want to feed more than one server the ACARS messages.  
6. Is for when you have a satellite dish and are using Jaero on C-Band. This is the IP and port for your VRS or tar1090 to plot the aircraft positions on a map. (Not used on L-Band since there is no position data).  
7. Check it if you must log, it will slow down the starting of Jaero the longer it runs. It will also drive you nuts trying to view the logs of 18 different Jaeros, review the Node-RED page and see that there is a better way to build custom logs.
8. If you have a VRS with images, you can pick them up here if you are logging.
9. Never thought we would get here did you.... 
Leave your ini file as it shows: zmq_address=tcp://*:6003 (Note, some of the .ini files have different port numbers, thats fine, just be sure to match port for port. The port in your .ini must match the port you use in your Jaeros).  
The port is important. So in each jaero Check the ZMQ box and just put your home IP of `tcp://127.0.0.1:6003` and again, make sure the port matches your ini file.  
Lastly, the topic. In your .ini file each VFO has a name, you must make sure that the name in JAERO matches the names in the ini. If you have used the .ini file and the startJaero batch file I have here, they should be very close.  
Also **WATCH OUT!** Jaero likes to put a space at the start of the word VFO!! So **make sure** that the V is tucked up against the edge of his box!!!! (Ask me how I know this!!!!!!!!!! - No don't)  

For the tabs on the top, I like turn off logging and turn off voice decoding. You may do otherwise, but if you just want the data, logging and voice use up CPU that you don't need to waste for just getting data.   

Click Ok. Last few things to do here... make sure you select the right data rate in Jaero that matches the VFO in the ini file for that VFO.  

Click the blue bump to move the pale green box over it so it will start to decode.  

Lastly, click the black CPU square to turn it green and save some computer power (It just slows down the blue wave form update - but is well worth it) and if you want to save even more, select "None' from the drop down list under the constellation to turn that off. Make sure AFC is on.  

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/jaerocpusavemodes.png" height="400">   

Now, minimize that Jaero, and do that all over again on the next 17. Making sure you get the next VFO number and its matching decode rate.  
Each one will save its settings when you close it, so next time, just double click the start batch file and you will be up and running in a few seconds.


<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-HGJWTNL65R"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'G-HGJWTNL65R');
</script>