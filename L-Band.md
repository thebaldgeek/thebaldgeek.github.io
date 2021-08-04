# How to build an L-Band ground station.   
   
Navigation: [home](README.md)  

The easiest way to get started with satcom ACARS is to build an L-Band setup.   
The L-Band is around 1.5GHz and the signal footprint from each Inmarsat is broad enough that you do not require any antenna tracking. Simply point it at the middle of the satellite orbit and you can start receiving the signal and decoding ACARS messages.   
To see what Inmarsat satellite(s) are over your location, review the [Inmarsat](Inmarsat.md) page.  
   
Here is the big picture of what we are going to review:   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/lbandoverview.jpg" height="580">   
   
The full signal path will be covered on another page, but the most import thing to know about L-Band is that you are picking up the ACARS messages *from* the airline dispatch or ground support staff *to* the aircraft.   
The way I describe it to friends and family is L-Band is *from land*. C-Band is *from Cockpit*.   
I take pains to explain this now before we get stated so that you understand what sort of messages you can expect to see from your efforts.    
Here is a typical sort of message you might see:   
`AES:4249EA GES:50 2 .VQ-BLQ ! RA G
QUHDQASRU~1
DEAR CREW,
PLEASE REQUEST ROUTE AND
DESCENT WIND SEPERATELY,
AND REPORT BACK WILL YOU
SUCCESSFULLY RECIEVE IT?
YES/NO
THANK YOU
`  
You can clearly see that this is a message from ground crew talking to the aircraft.   
But, don't be disapointed, there are a LOT of very interesting messages that come from ground staff and get sent up to the flight crew. Here is a hint, this is a CPDLC message to the same aircraft:   

`AES:4249EA GES:50 2 .VQ-BLQ ! H1 C
#MD/AA GDXE1XA.AT1.VQ-BLQ6192D0E622C960EC18
FANS-1/A CPDLC MESSAGE:
CPDLC UPLINK MESSAGE:
HEADER:
MSG ID: 3
MSG REF: 9
TIMESTAMP: 13:03:38
MESSAGE DATA:
CRUISE CLIMB TO [ALTITUDE]
FLIGHT LEVEL: 330`  
   
Here you can see the ground request that the aircraft climb to FL330.   
   
If your interest is military aircraft, L-Band has a ton of good information for you too.   
Here is an interesting ground staff message to the flight crew:   
`TC AES:3B75A8 GES:D0 2 .F-UJCH ! AA R
/OAKODYA.AT1.F-UJCH2545FAEA4AA1CF9D1A4D29A82A59A11504F8C819A08D263C8A9169208326
943A506354415E4D49082CCFAA0290
FANS-1/A CPDLC MESSAGE:
CPDLC UPLINK MESSAGE:
HEADER:
MSG ID: 10
TIMESTAMP: 17:31:43
MESSAGE DATA:
[FREETEXT]
CONFIRM TYPE OF 3 FIGHTER AIRCRAFT WITH YOU`   
This is from a French dispatch operator to a tanker that was towing 3 Rafael fighter aircraft around Tahiti.   
Since L-Band is from the ground to the aircraft, you will also see 'commands' given to flight crews for course changes, or even future flights, so you will know about a flight plan before it is flown. Here is one such example:  
`-06-21UTCAES:AE07EAGES:022.50107A!H1C-#MDWXR/ID50107A,RCH240,AJZF102SD173/MR3,11/MTKHMN,1610,TAFKHMN221610ZVRB06KT9999FEW240QNH3016INST26C-AUTORESPONSEBASEDONAVAILABLEDATA-CONTACTC2AGENCYFORADDITIONALINFO9FAD`  
Here we see RCH240 being instructed to fly to KHMN.   
    
There is more, but I will save it for the Military page (when I get to writing it).   
     
## Building or buying the hardware ##   
Some people build, some people buy their antennas. With L-Band, you can do either.    
    
Here is a selection of L-Band antennas that I have used at some point in time:   

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/PXL_20210418_192625210.jpg" height="580">      

At the front we have the RTL-SDR v1 patch. Next is the V2 patch, then a prototype of the 3D printed helix and then a second prototype.   
## Buy
   The most popular buy option is the RTL-SDR v2 patch antenna. In June 2021 it was out of stock globally for the next many months.    
The other options are smaller antennas. (Not recommended) Some (including myself) have tested modified GPS antennas. Generally these are too small and do not have enough gain to be of real value. You might get up and running with a few scratchy signals, but will soon be disappointed.  
If your interest is listening to voice calls, you are going to need a pretty good antenna, the v2 patch antenna is marginal, more gain is required for good decodes of the audio. Just keep in mind that the more gain an antenna has, the more directional it becomes. You may get to the point where your L-Band antenna has so much gain that the satellite orbit takes it off your antenna sweet spot and you need to track it or move each time you want to decode some messages.   

   
Another aspect to consider is your interest in L-Band ACARS. If you just want to set something up and use it for an hour or so then pull it down, something like the V2 patch antenna might be Ok.   
If you just want to listen to one downlink channel a time, then your antenna configuration does not change much, but your software setup becomes a LOT simpler.  
If you only have an indoor antenna option, then more antenna gain is something you really need to consider.   
  
  My goal was to setup a system that had 24 x 7 x 365 coverage and caught every downlink message possible from every channel on the satellite.   
## Build     
My current preferred, recommended and in stock antenna for L-Band is a 3D printed 7 turn Helix.  
Here is a close up of the antenna while connected to a NanoVNA.   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/nanovna.png" height="580">  
    
The hard work of getting the spacing is taken care of by the 3D printed white framework.   
You can download the file from thingverse here: <https://www.thingiverse.com/thing:4834929>  
Take care to download and print the correct type, there are 4 to chose from.   
Since I am not shooting into a dish, I need right-hand circular polarization. I also really like the version with the extra leg support at the top of the three legs, so I use file: NH1542R2   
Order the 4mm copper tube off Amazon and the base is a stainless steel 8 inch pizza pan also from Amazon. The hardware is stainless steel from Home Depot. The antenna connector is a SMA male bulkhead connector from Amazon.
Note, the 8 inch pizza pan is the smallest you should go. The reflector is an important part of the antenna performance. You can go bigger, but no smaller.    
The key to building the antenna is to pre-form the copper on a cylinder that is very close to the final size.   
As it happens, a Vegemite jar is perfect (I am Australian - I had it close to hand).   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/lbandpreformcopperwind.png" height="320">    
Once you preform the copper to the right size, you can then wind it on the framework very smoothly.  
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/lbandpreformcopper.png" height="460">  
    
Trim the turns to exactly 7 and then drill the two large holes for the 3D frame, then mark and drill the bulkhead connector mount near the left hand side support - you go near the left side of the frame so you can run the first 2/3rds of the copper parallel to the base, this improves the match and lowers the SWR. Solder the copper pipe to the connector and you are done building the antenna.   
## Contact thebaldgeek if you want to buy a pre-made and tested helix   
   If don't have access to a 3D printer (try your local public library or 3D printing service) and would rather just buy a fully built and tested antenna I am selling them for $50 including shipping to mainland USA. Drop me an email if you would like to buy one: bmorchard at g mail dot com. If you are not in the USA and would like to buy one, still go ahead and drop me an email and we will do our best to ship one to you. I accept payment via PayPal, but if you must do a check, we can probably work with you on that.      
      <img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/7turnhelixantennas.jpg" height="460">

   While it works Ok on its own, it really shines with a Nooelec L-Band low noise amplifier (LNA) mounted directly behind it. I buy my LNAs from Amazon. You can use Bias-T to power the amplifier or a micro USB power lead if your SDR device does not offer Bias-T as an option. Keep in mind that not all SDR Bias-Ts are equal. For example, I found out (the hard way) that the RSP1a Bias-T is not powerful enough to run the Nooelec LNA, but the RTLSDRv3 runs it just fine. (As does the Nooelec SmarTee SDR).   
Here is the link to Amazon USA for the L-Band LNA that I really like and highly recommend. <https://www.amazon.com/gp/product/B07K1NMC23>   
Also keep in mind that if plan to mount this helix outside (and I strongly suggest you do) it will need to be weather proofed. Here are some photos of some customer solutions....   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/lbandhelixglueinpot.png" height="320">   
The silicon did not hold as well as they hoped, so they ended up screwing the base to the sides of the pot:    
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/lbandhelixscrewinpot.png" height="320">   
Very low tech final resting place here, but its looking straight at the satellite and gives great around the clock decoding message rate:   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/lbandhelixondish.png" height="320">   
Here is another flowerpot solution, this one is a little more stealth (HOA rules):   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/lbandhelixpotfence.png" height="320">    
Lastly, here is how the LNA is mounted in both cases - just tuck it up out of the weather:    
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/lbandhelixpotback.png" height="320">    
If you are indoors, you have more options:    
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/lbandhelixtripod.png" height="320">   
   In regard to SDRs, I like the silver v3 RTL-SDR, but in this case, because of the requirement to use Bias-T to power the LNA, I use the Nooelect SmarTee SDR as it has Bias-T always on without needing to run the v3 bat file to turn it on. The performance of the two SDRs seems to be identical.   
      
How you mount the antenna is up to you. A few people have put them under a flowerpot and mounted them outside and used a bracket that is pointing at their satellite. 
Some have attached them to camera tripods and used them inside their apartment's. In this case, you do not need to weatherproof the antenna, but it comes at a signal strength drop. Also experiment with positioning, a window may not offer the best signal.   
Bottom line, the antenna and LNA are *NOT* water proof and you must put it under cover.   
Be sure and run some quality coax. The longer the length required to get from the antenna to the SDR, the more you should spend on the coax. 1.5GHz is rather lossy, more so than the 1090MHz from an ADSB antenna that you might be used to. (And even more so than the VHF ACARS frequency of around 130MHz). If in doubt, LMR-400 is the coax to use.   
    
## Software setup and tweaks    
With the antenna mounted and the coax run, we can focus on the software side of things.   
I am going to proceed as if you are going to set up and monitor all channels around the clock and you are going to feed your data to your local Node-RED for message filtering (ie just Military aircraft) and reporting / alerting.   
That said, if you just want to monitor now and then, and you want to use the Jaero aircraft database and logging, you need to skim over what follows and pick up how to set up the database and ADSBExchange link in Jaero for the best experience.   
   
## Download and unzip Jaero   
We want to be sure to be using the 1.0.4.13-Alpha version of Jaero which was updated in August 2021.   
Go to the Jaero GitHub page: <https://github.com/jontio/JAERO/releases> and under the list of 'Commits' bullet points (at the top of the page) there is a small 'Assets' drop down, expand it and download the file you need.   
## Jaero on Linux
A quick word here on Linux. While there is a Jaero build for linux (I have instructions to do this on the [jaero](jaero.md) page), there are a few issues.
1. If you want to run the SDRReceiver software (which you do - its the best way) then you MUST use the .13 version of Jaero.   
2. As yet, there are no clear instructions to build that version on the Raspberry Pi. (the reason is because Jaero uses qt5 for the GUI and the version of qt5 on the Pi is old and out of date, so Jaero can be built or installed on the Pi).  
Please let me know if you find a way to get the .13 version of Jaero built and installed on a Pi.   
3. The old v11 version of Jaero builds Ok, but uses so much CPU when its running that  myself and others have not managed to run the required 12 or so instances on Linux. One or two is fine, but as you add more, the message decode rate starts to drop until they are running but not decoding. I have had to stick to Windows for all my satellite decoding adventures.   
## To install and run Jaero on Windows   
To get up and running on Windows using SDRReciver, look at the dedicated page here:    
   
    
### Decode some data already    
Once you have SDRReceiver installed and running and your Jaeros up and decoding, its just a matter now of moving the data where you want it.