# wardriving brain dump.   
   
Navigation: [home](README.md)  
   
Over simplifying, wardriving is about picking up as many Wifi SSID's as possible. Second to that is having them accurately GPS tagged, and striking the balance between range and accuracy.   
thebaldgeek joined Wigle around Dec 2015. Before then, he was actively wardriving for about 5 years with many different setups - Orinoco cards in a HP Jornada for example. He's been testing different setups and antennas and using the WIfi SSIDs broadcasts as signal sources since the RF aspect is a strong interest.   
Aug 2024 he got the bug again and started pushing for the 1 million mark (Nov 2024, 1/2 million Wifi discovered by thebaldgeek). Once again, this page is a messy brain dump of notes and current setups tbg is running.    

### Why wardrive?    
There are a lot of different goals and reasons to wardrive.     
For tbg, living in Southern California (high population density and thus high geek density means that a lot of SoCal has already been wardriven by different methods) means that the big wifi nuggets have been mined and picked over to various extent, so his goal is to build a rig/setup that will extract the flecks of wifi gold that others have missed from the same roads.   
This does NOT mean high gain antennas, but rather ensuring that each and _every_ wifi SSID is geotagged as accurately as possible. This means using sensable antenna gain, lower ground speed, higher speed wifi channel scanning and very good GPS signal / many GPS sats fixing each SSID that is heard.   
   
Your goals might be different. Take a pause to think about why you are wardriving, what your goals are, and how to reach them the most efficient and interesting way.  
   
    
## Android Phones running Wigle.   
Never throw out old Android phones. (But there are age limits.)   
Old old phones that are, say, more than 6-8+ years old struggle to have the right SSL certificates and so they can’t connect to the wigle.net servers, on some you can side load the old version of the wigle apk and get the app running, but generally it's a bit more hassle than it's worth.    
     
Safe to say that simply installing the Wigle app and letting your phone run day in day out is the easiest way to get going with wardriving.    
Do note that Google decided to throttle the wifi channel scanning speed to save a bit of battery power, it's up to you if you want to enable developer mode and disable that throttle or not. tbg turns it off and has not really noticed that much of a battery life hit, but just know that it's an option and be aware of the downsides. Of course, if it hurts your battery life, turn the throttle back on, experimentation is the name of the wardriving game.     
And sorry iPhone folks. Apple does not like its users playing on the other side of their walled garden. Ask some friends, family, co-workers if you can have / buy their old Android phones they have sitting in the top draw going unused.   

Phones that tbg has tested or currently uses:    
Note 9 - not great   
Pixel 5 - Okish   
Pixel 8 Pro - pretty good. Daily driver phone and in-car wigle map display    
Samsung G23 - solid. tbg sons daily driver. Tested in-car only.   
Samsung G20 - Beast. No, really, this phone is the best wardriving Android that tbg has found hands down.    
Nexus 7 - External antenna mod. Great setup, on the large size, but the external antenna mod makes it worth running. (Died Aug 2024 - display).   
   
3 phone example when warriding on an electric AT longboard   
(Right click - Open in new tab any photos to enbiggen)   

   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/wardrive/3phonewarride.png" height="320">   

Wardriving on an electric longboard. Top speed of 15mph, easy to quietly move around apartment complexes and other tight spaces.   
tbg currently runs three phones, the P8P in the car showing the wigle map - it’s also scanning of course, P5 and G20 are the main scanners.   
   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/wardrive/twoPhonewarDrive.png" height="320">

The P8P on the left: 2170   
Samsung S20 on the right: 3570   
Same drive. The S20 really is a wardriving beast.   
   
## Phone placement.    
Clearly, just having a phone in the car on a vent or suction cup mount is the safest and cleanest way to set things up.  
If you have one Android phone as your daily wardriver, then just running the wigle app while going about your life is fantastic and will be good fun.   
   
Once you start running three or more phones it gets a lot more fun and complicated keeping them charged and uploading after each run.    
tbg heard about one guy that runs 5 phones on every wardrive. 1 daily driver up front with him on the drivers side, one at the front of the car on the passenger side, 1 on the rear drivers side window, 1 on the rear passenger side window and 1 in the middle of the back window. Pretty solid setup.    
     
One thing tbg learned the hard way with L-Band ACARS is that often window tint can block Ghz signals. In the case of cars this includes the ceramic and 3M window tint (very popular in SoCal), or any brand that blocks UV radiation (heat).  Given this first hand experience from the placement of 1.7GHz satcom helix antennas, of course he figured he should test it with his wardriving phone setup.    
tbg figured the best place for a Ghz RF antenna is outside the car, outside the RF shield, getting an extra few feet of height does not hurt any either..   
   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/wardrive/rubberbandroof.png" height="320">

Magnets in the blue box floor holding it to the roof. Not the best long term solution, but for a 40mph max speed, 32mph average, 5 drive run, it proved the point.  
thebaldgeek then got his CAD / 3D printing guy on the job and this is what he has now…

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/wardrive/dualwiglefins.png" height="320">   
   
tbg wife wants matching wiglefin color to car colour, so tbg is printing another white and red setup....   

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/wardrive/foamclamp.jpg" height="320">   
    
TPU sleve is in the works, but until then, just a foam cutout to protect the phone inside the wiglefin.   

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/wardrive/lowerintowiglefin.jpg" height="320">   
Lower the foam and phone into the fin....   

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/wardrive/phoneinfin.jpg" height="320">   
The phone is snug ready to have the fin lid put on...

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/wardrive/wiglefinlid.jpg" height="320">  

The commute to work is a good baseline. Same route at the same time each day.   
Make 5 runs and see what the average is with the phone on the in-car vent mount.   
Move the same phone outside and make the same baseline run 5 times and see what the difference is.   
P5 in-car 5 run average wifi SSIDs: 2456   
P5 roof 5 run average wifi SSIDs: 4971   
Stunning. Almost double the wifi SSID’s by having the phone on the roof of the car.  
Same drive, same time, 5 working day average. Pretty much consistently about double the number of SSIDs heard by the exact same phone just by mounting it on the roof of the car.  
  
If you want to print your own, this should give you a good head start.    
Let thebaldgeek know (contact on the home page here), he'd love to hear about it:  
[wiglefin body](https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/wardrive/wigleFinV3_body.stl)   
[wiglefin lid](https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/wardrive/wigleFinV3_lid.stl)   
[wiglefin lid pin](https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/wardrive/wigleFinV3_pin.stl)   

(As an aside, tbg thinks the 2019 Chevrolet Bolt is the best wardiving car — it’s quiet, cheap, has a good enough turning circle, and most of all, a one pedal driving mode that can't be beat).  
   
## Scanning Wifi channels.   
  
There are 14 channels on 2.4Ghz and 24 on 5Ghz. The ‘trick’ is to scan _all_ of them looking for the SSID broadcasts while driving down the road.   
If you have spent any time on the https://wigle.net/phpbb/ forums you would know that there is a lot of talk about what are the best scan speeds to try and push your phone(s) to pick up the most number of broadcasts for any given ground speed.   
tbg has seen one website that did the math of the typical range of wifi vs 20mph driving speed vs SSDI broadcast interval.    
In short, accept the wigle app default of 3sec and you are in the ballpark.   
  
Keep reading for information about the Wifydra that gets around the channel hopping issue - on 2.4Ghz at any rate.   
The limitations of the Android app scanning through all these channels (pausing on each one at a time for a short time) is why most hard core wardrivers run more than one phone.  
You will get a helpful overlap of each phone scanning different channels at different times. This is exactly why tbg runs three phones and the wifydra. It really increases the odds of getting every 2.4GHz SSID broadcast at any ground speed. Of course the phones also pick up the 5Ghz and Bluetooth. Building a 5Ghz wifydra is on the hit list for many wardriving folks. 
   
  
## wifhydra - scan ALL the 2.4Ghz channels ALL the time. #allTheWifi

https://github.com/lozaning/The_Wifydra

Build cost is about $120 to $210 USD depending on options.. (Note that the Wifydra in a box with whip antennas is going to cost around the same cost as a refurb Samsung S20 here in the USA).
BOM:
$30 5 x PCB (5 is the min order).  
$32 1 x [GPS board:](https://www.adafruit.com/product/746)  
$9 1 x [MicroSD breakout board:](https://www.adafruit.com/product/254)  
$34 1 x [Feather board:](https://www.digikey.com/en/products/detail/adafruit-industries-llc/5300/16584014)  
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
Blank PCB, you can see the 14 receivers on the desk. The antennas are mounted on the case.
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/wardrive/wifydragacks.jpg" height="240">   
Three wire jumpers are needed to route power to a few places that were missed on the OP board.   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/wardrive/handforscale.jpg" height="240">   
Wifydra in the hand.   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/wardrive/wifydrathermal.JPG" height="240">   
Just a bit of a 'for interest' photo. No hot spots. The board draws just over 1.3 Amps at 5vDC, its about 7 Watts, nothing hot, just everything slightly warm.    
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/wardrive/wifydrariding.jpg" height="240">   
The 4 magenets on the bottom of the box means that tbg can move the wifydra around from AT longboard to car and other places under 82Mph windspeed.   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/wardrive/wifydraandwiglefin.jpg" height="240">   

Program the dom.ino into the feather board.  
Note that we could not get the Dom to compile and download using the local IDE that we used for the Subs. Once we switched to the cloud based IDE, the dom compiled and downloaded without issue.   
  
Solder up the +v, gnd and two I2C pads on each sub and the pins on the GPS and SD card boards.  
Jumper each of the VCC, gnd and both sets of I2C pins on the main PCB.  
Apply the three gaks.   
tbg never figured out why, but he could not power the board from the Gnd and Vcc pins just above the Dom Feather module.  
The board will pull about 1.38 amps at 5 vDC. This is about 7 Watts.  
The board worked when powered via the USB-C connector on the Dom Feather module.  
(Not sure about why the tiny font on the Dom, if tbg ever works it out, will update this page).  
  
When there is no lock, the GPS will flash its fix LED every second. When the GPS has a fix, it will flash every 15 seconds.  
  
There is no ‘safely remove’ the SD card requirement, the code writes each new SSID to the CSV log file and closes the file, so the card can be ejected at any time that its activity LED is not on.  
Log into wigle and upload all the CSV files created during the run. Best to wipe them out of the SD card once uploaded so you can keep track of what you have sent after each wardrive.  
  
   

<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-HGJWTNL65R"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'G-HGJWTNL65R');
</script>