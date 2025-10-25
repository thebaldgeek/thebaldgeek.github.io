# wardriving brain dump.   
   
Navigation: [home](README.md)  
   
Oct 2025.   
tbg finds VSCode / GitHub io a horrible platform for blogging.    
As such he has moved this blog, and massivly expanded it, over on his main blog platform.   
You can find it here: https://k6thebaldgeek.blogspot.com/2025/09/wardriving.html   
The notes that remain here are just about the WigleFin and wifydra build parts list.   
   
## WigleFin.
  
If you want to print your own, this should give you a good head start.    
Let thebaldgeek know, he'd love to hear about it:  
[wiglefin body](https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/wardrive/wigleFinV3_body.stl)   
[wiglefin lid](https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/wardrive/wigleFinV3_lid.stl)   
[wiglefin lid pin](https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/wardrive/wigleFinV3_pin.stl)   
   
The print has been designed to take the 150lb pull magnets from Amazon, these here: [Magnet set](https://www.amazon.com/dp/B0CC5HC4NG)  
Depending on your printer, you may or may not need to glue them in.  
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/wardrive/wiglefinmagetfit.png" height="320">   
Im my case, this red print they are pretty much a perfect fit.   
TIP: try and get them as close to the bottom as possible. You want the max pull force onto the surface and the closer you get them the stronger the pull.   
In other words, don't get any glue between the bottom of the print and the roof of the car. Just the non-slip grip.   
      
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/wardrive/bottomofwiglefin.png" height="320">  
The kitchen draw liner really helps keep the fin from moving around and also stops the magnets from hitting the roof of the car.   
Just be sure to check the bottom of the fin each time before you place it, you might have picked up some small metal hitchhikers and they might scratch the roof. 
   
  
## wifydra - scan ALL the 2.4Ghz channels ALL the time. #allTheWifi

[allTheWifi with Wifydra](https://github.com/lozaning/The_Wifydra)   
Dec 2024. NOTE! DO NOT USE the dom.ini that is in the repo (main.zip). It has errors and will NOT work. ONLY use the dom.ini that is in thebaldgeek issue comments at the bottom of [this](https://github.com/lozaning/The_Wifydra/issues/7) thread.   
   
Build cost is about $120 to $210 USD depending on options.. (Note that the Wifydra in a box with whip antennas is going to cost around the same cost as a refurb Samsung S20 here in the USA).
BOM:
$30 5 x PCB (5 is the min order).  
$32 1 x [GPS board](https://www.adafruit.com/product/746)  
$9 1 x [MicroSD breakout board](https://www.adafruit.com/product/254)  
$34 1 x [Feather board](https://www.digikey.com/en/products/detail/adafruit-industries-llc/5300/16584014)  
$68 14 x [ESP32C3](https://www.seeedstudio.com/Seeed-XIAO-ESP32C3-p-5431.html)  
Note1: the ESP32C3 each come with a small flexible ‘patch’ antenna on a short coax cable.  
Note2: tbg went for the cheaper ESP as the phones get Bluetooth already and the cheap board is the same price as the expensive board without an antenna.  
Note3: the GPS module uses a CR1223 battery to retain GPS data between power cycles. Its highly recommended to buy a battery and put in the module as it will make cold start GPS lock a LOT quicker (less SSIDs saved with 000.000 lat / lon).  

Extra tbg Options;  
14 x [2.4Ghz antenna and SMA adaptor](https://www.seeedstudio.com/2-4GHz-2-81dBi-Antenna-for-XIAO-ESP32C3-p-5475.html)  
1 x [GPS active antenna](https://www.amazon.com/Waterproof-Active-Antenna-28dB-3-5VDC/dp/B00LXRQY9A)  
1 x [GPS SMA adaptor cable](https://www.amazon.com/dp/B00XW2LKNO)  
1 x [microSD card extender](https://www.amazon.com/dp/B07WWVBK8V)  
1 x [Hard case](https://www.amazon.com/dp/B094W9266D)  
1 x [Magnet set](https://www.amazon.com/dp/B0CC5HC4NG)  

Before you start the parts collection / build process, you should take a read of the following github issue.   
The wifydra software took a bit of tweaking to make work with wigle.net and you should be aware of the need to manually 'fix' the CSV file before you upload it each and every time.   
[Correct and working dom.ini in the bottom comment](https://github.com/lozaning/The_Wifydra/issues/7)  

Program the sub.ino into each ESP, make sure you edit the .ino (its a text file) and change the board number - look for the obvious comment a few lines into the file. They MUST be numbered 1 through 14, don’t use any other number system, the numbers are tied to the code in the dom.ino file in the feather board.  
tbg labeled the boards so if he had an issue, he’d know which one it was, not required, but not a bad idea.  
The sub boards are numbered on the main PCB, but any sub can go in any location.  
  
It's slow(ish) to program all 14 subs because the IDE has to compile for every board just due to changing the one line boardID, and just FYI, we had to set the specific board type in the IDE.  
It auto-detects as "ESP32 Family Device" but won't compile unless you select "XIAO-ESP32-C3".   
  
Only thing of note is that we had three of the 14 subs throw this message:  
 — Failed uploading: uploading error: exit status 2  
Thankfully both worked on retry.  
1 Sub ESP32 totally failed. Tip, buy 1-2 extra and save having to reorder and extra shipping.  
  
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/wardrive/blankpcb.jpg" height="240">   
Blank PCB on the right, you can see the 14 receivers on the desk in the middle. The Wifi antennas and GPS active puck antenna is mounted on the empty case.    
  
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/wardrive/wifydragacks.jpg" height="240">   
Three wire jumpers are needed to route power to a few places that were missed on the OP board.   
Make sure you install these or the board will not fully power up.      
   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/wardrive/handforscale.jpg" height="240">   
Wifydra in the hand.   
   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/wardrive/wifydrathermal.JPG" height="240">   
Just a bit of a 'for interest' photo. No hot spots. The board draws just over 1.3 Amps at 5vDC, its about 7 Watts, nothing hot, just everything slightly warm.    
   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/wardrive/wifydrariding.jpg" height="240">   
The 4 magnets on the bottom of the box means that tbg can move the wifydra around from AT electric longboard to car and other places under 82Mph windspeed.   
   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/wardrive/wifydraandwiglefin.jpg" height="240">   

Program the correct dom.ino into the feather board. As of Dec 3rd 3 2024, the correct dom is at the bottom of the github issue linked above. DO NOT use the dom in the main zip file!   

Note that we could not get the Dom to compile and download using the local IDE that we used for the Subs. Once we switched to the cloud based IDE, the dom compiled and downloaded without issue.   
  
Solder up the +v, gnd and two I2C pads on each sub and the pins on the GPS and SD card boards.  
Jumper each of the VCC, gnd and both sets of I2C pins on the main PCB.  
Apply the three gaks.   
tbg never figured out why, but he could not power the board from the Gnd and Vcc pins just above the Dom Feather module.  
The board will pull about 1.38 amps at 5 vDC. This is about 7 Watts.  
The board worked when powered via the USB-C connector on the Dom Feather module.  
(Not sure about why the tiny font on the Dom, if tbg ever works it out, will update this page).  
  
When there is no lock, the GPS will flash its fix LED every second. When the GPS has a fix, it will flash every 15 seconds.  
  
There is no ‘safely remove’ the SD card requirement, the code writes each new SSID to the CSV log file as it comes in and then closes the file, so the card can be ejected at any time that its activity LED is not on.  
Log into wigle and upload all the CSV files created during the run. Best to wipe them out of the SD card once uploaded so you can keep track of what you have sent after each wardrive.  
  
After each wardrive, power off the wifydra pop the SD card, open it in a text editor, delete the top SSDIs that have a lat lon of 0.0 / 0.0, optionally also remove the top few SSIDs that have an error (last number before the WIFI at the end of each line) greater than 100.0. Save the file and then upload it to wigle.net.   
   

<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-HGJWTNL65R"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'G-HGJWTNL65R');
</script>