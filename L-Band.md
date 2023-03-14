# How to build an L-Band ground station.   
   
Navigation: [home](README.md)  

The easiest way to get started with satcom ACARS is to build an L-Band setup.   
The L-Band is around 1.5GHz and the signal footprint from each Inmarsat is broad enough that you do not require any antenna tracking. Simply point it at the middle of the satellite orbit and you can start receiving the signal and decoding ACARS messages.   
To see what Inmarsat satellite(s) are over your location, review the [Inmarsat](Inmarsat.md) page.  
   
Here is the big picture of what we are going to review:   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/lbandoverview.jpg" height="580">   
   
The full signal path will be covered on another page, but the most import thing to know about L-Band is that you are picking up the ACARS messages *from* the airline dispatch or ground support staff *to* the aircraft.   
The way I describe it to friends and family is L-Band is *from land*. C-Band is *from Cockpit*. (If you are interested in listening to audio, you will hear the voice of the dispatch operator and silence while the flight crew are talking, you will *not* hear a full duplex conversation, just the ground side only).   

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
But, don't be disappointed, there are a LOT of very interesting messages that come from ground staff and get sent up to the flight crew. Here is a hint, this is a CPDLC message to the same aircraft:   

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
   The most popular buy option is the RTL-SDR v2 patch antenna. 
The other options are smaller antennas which is strongly not recommended! (Small size = low price = low performance ie very low signal). Some (including myself) have even tried and tested modified GPS antennas. Generally these are too small and do not have enough gain to be of real value. You might get up and running with a few scratchy signals on some of the stronger 600/1200 data channels, but you will soon be disappointed. In short, any of the small hockey puck sized patch antennas are to be avoided no matter how attractive the low price.   

If you do go ahead with the v2 patch antenna (and if the patch is your 'only' option for the installation you have in mind - then the v2 is the only one worth considering) be sure and replace the ultra thin and very lossy coax it comes with. More than one report of the coax simply not working out of the box is floating around on the Internet - thats how poor quality that coax is. There are many sellers / sources for quality coax with SMA connectors on each end. Remember, L-Band is around 1.5GHz, the higher the frequency, the more signal loss in the coax.
Also note that the v2 patch antenna has a built in LNA that requires Bias T to power it up. Do NOT run a second LNA in front of this antenna as it will block the DC and you will not get a signal from the antenna. (Yes, the antenna has a USB power option, you need to drill a hole in the case to use that power option).   

If your interest is listening to voice calls, you are going to need a pretty good antenna, the v2 patch antenna is marginal, more gain is required for good consistent decodes of the audio. Just keep in mind that the more gain an antenna has, the more directional it becomes. You may get to the point where your L-Band antenna has so much gain that the satellite orbit takes it off your antenna sweet spot and you need to track it or move each time you want to decode some voice messages. Note that this can even happen with a poorly installed patch antenna, here is an example: 

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/patchorbit.png" height="320"> 
  
Note how the message rate drops to zero when the satellite is at the top if its orbit. In this case, the patch mount should be tilted down a little so that the signal/message rate is consistent with aircraft movements. (Overnight, in the early mornings, aircraft movements die down, but your message rate should never go to zero).  
Another reason for these dropouts could be an obstruction between you and the satellite, for example a house or tree. If you recall from the [Inmarsat](Inmarsat.md) page the satellite orbit over ~24 hours is a '8', both up and down and side to side.
   
Another aspect to consider is your long term interest in L-Band ACARS. If you just want to set something up and use it for an hour or so then pull it down, something like the V2 patch antenna might be Ok.   
If you just want to listen to one downlink channel a time, then your antenna configuration does not change much, but your software setup becomes a LOT simpler.  
If you only have an indoor antenna option, then more antenna gain is something you really need to consider.   
  
  My goal was to setup a system that had 24 x 7 x 365 coverage and catch every downlink message possible from every data channel on the satellite.   
## Build     
My current preferred, recommended antenna for L-Band is a 3D printed 7 turn Helix.  
Here is a close up of the antenna while connected to a NanoVNA.  

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/nanovna.png" height="580">  
    
The hard work of getting the spacing is taken care of by the 3D printed white framework.   
You can download the file from thingverse here: <https://www.thingiverse.com/thing:4980180>  
Take care to download and print the correct type, there are 11 to chose from.   
Since I am **not** shooting into a dish, I need right-hand circular polarization. I also really like the version with the extra leg support at the top of the three legs, so I use file: <https://cdn.thingiverse.com/assets/d0/70/24/9c/3a/1542R_7T_0.11S_4.7D_10-90M_ACARS.stl>   

# BOM (Bill of Materials)
1 x 8 inch pizza pan. <https://www.amazon.com/gp/product/B08N4VQ9BM/>  
(Note, you can go larger, but no smaller on the reflector. Does not need to be stainless, but they last longer - and are harder to drill).   
1 x 2m soft copper 4mm tube. <https://www.amazon.com/gp/product/B07FXMY5DJ>    
(You will have a little left over, but 2m is the right length. You can go a little smaller diameter, but no bigger. Tube is easier to work with than solid).   
1 x Male SMA bulk head connector. <https://www.amazon.com/gp/product/B06Y5ZMNSJ/>   
Assorted stainless nuts, bolts, screws. (<https://www.amazon.com/gp/product/B06X1FNS96> <https://www.amazon.com/gp/product/B00B3RIH5E> <https://www.amazon.com/gp/product/B07D1L38HD> <https://www.amazon.com/gp/product/B01B1OD6MW/> )

Order the 4mm copper tube off Amazon and the base is a stainless steel 8 inch pizza pan also from Amazon. The hardware is stainless steel from Home Depot or Amazon (2 large for the 3D formwork, two small for the SMA bulkhead ). The antenna connector is a SMA male bulkhead connector from Amazon.
Note, the 8 inch pizza pan is the smallest you should go. The reflector is an important part of the antenna performance. You can go bigger, but no smaller.    
The key to building the antenna is to pre-form the copper on a cylinder that is very close to the final size.   
As it happens, a Vegemite jar is perfect (I am Australian - I had it close to hand).   

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/lbandpreformcopperwind.png" height="320">  

Once you preform the copper to the right size, you can then wind it on the framework very smoothly.  

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/lbandpreformcopper.png" height="460">  
    
Trim the turns to roughly 7 and a bit turns (close to 8) and then drill the two large holes for the 3D frame, then mark and drill the bulkhead connector mount near the left hand side support - you go near the left side of the frame so you can run the first 2/3rds of the copper parallel to the base, this improves the match and lowers the SWR. Solder the copper pipe to the connector and you are done building the antenna.   
Once built, trim the total length to get the VNA dip on frequency and move the first 2/3rds of a turn close to the reflector to get the SWR nice and low and you are done.   


   <img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/7turnhelixantennas.jpg" height="460">

   While it can work Okish on its own, it really shines with a Nooelec L-Band low noise amplifier (LNA) mounted directly behind it. I buy my LNAs from Amazon. You can use Bias-T from the SDR dongle to power the amplifier or a micro USB power lead if your SDR device does not offer Bias-T as an option. Keep in mind that not all SDR Bias-Ts are equal. For example, I found out (the hard way) that the RSP1a Bias-T is not powerful enough to run the Nooelec LNA, but the RTLSDRv3 runs it just fine. (As does the Nooelec SmarTee SDR).   
Here is the link to Amazon USA for the L-Band LNA that I really like and highly recommend. <https://www.amazon.com/gp/product/B07K1NMC23>   
To give a feel for how the three antennas work, here are the three waterfalls centered around the 10500 channels.  

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/98wasov1patch.png" height="320"> 


<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/98wasov2patch.PNG" height="320">   

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/98wasocopperhelix.png" height="320">   
    
No antenna is going to work its best indoors, but if its your only option, then more gain will help.

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
Here is a great shot from a helix owner - looks like the ultimate L-Band antenna shoot out... I have asked for some results, so check back for those...  

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/antennaFarm.jpg" height="320">   
   
   From left to right. We have the ever popular RTLSDR v2 patch, the out of stock Othernet patch, long boom yagi (18 dBi and a length of 1,67 meters) and my  7 turn helix.  
   The results are interesting. Keep in mind these are just 'desktop' measurements as you see in the photo. I like them because they are real world, but should not be taken as hard and fast numbers: (Your install mileage may vary).   
  


| Antenna        | Jaero 600 dBuV  | Jaero 1200 dBuV  | Jaero 10500 dBuV        | Jaero 8400 dBuV  | Voice Decode  |
| ------------- |:-------------:| :-----:| :-------------: |:-------------:| :-----:|
| Helix      | 61.1 | 54.1 | 46.3  | 46.2 | yes |
| Yagi      | 62.4 | 61.5 | 50  | 48.1 | yes |
| Othernet | 53.2 | 54.7 | 39.5 | 35.8  |  no |
| v2 Patch | 56.2 | 58.4 | 46.2 | 48 | occasionally |

The gentleman that owns all the antennas kindly provided the numbers and used the same SDR and software to run the test for a few minutes on each antenna.   
It clearly shows that a big high gain antenna like the yagi is king of the L-Band, but keep in mind that it has such a narrow beam width that you will probably need to 'track' the satellite to some extent to keep the signal peaked. Also don't forget that the yagi is not circular polarized so is losing some gain there as well.  
It also shows that the data channels are not all equal. The 10500 and 8400 voice channels are the weakest. (And arguably the most interesting - despite the fact that I personally don't find one sided conversations interesting.)  
## Which SDR?
   In regard to SDRs, I like the silver v3 RTL-SDR, but in this case, because of the requirement to use Bias-T to power the LNA, I use the Nooelect SmarTee SDR as it has Bias-T always on without needing to run the v3 bat file to turn it on. The performance of the two SDRs seems to be identical. With that said, I have had some issue using the SmarTee with [SDRReceiver](SDRReceiver.md) that I am still working through. Also note that I have tested the RSP1a on L-Band and the more expensive SDR showed no benefit at all over the cheaper RTLSDr v3. This is mostly due to the fact of using the LNA, a more sensitive SDR does not perform any better since the system noise is not limited by the SDR. In short, use the cheaper SDR on L-Band and the other on HF where the difference in performance between the two is dramatic.    
## Mounting       
How you mount the antenna is up to you. A few people have put them under a flowerpot and mounted them outside and used a bracket that is pointing at their satellite. 
Some have attached them to camera tripods and used them inside their apartment's. In this case, you do not need to weatherproof the antenna, but it comes at a signal strength drop. Also experiment with positioning, a **window may not offer the best signal**.   
Bottom line, the antenna and LNA are *NOT* water proof and you must put it under cover.   
## Coax
Be sure and run some quality coax. The longer the length required to get from the antenna to the SDR, the more you should spend on the coax. 1.5GHz is rather lossy, more so than the 1090MHz from an ADSB antenna that you might be used to. (And even more so than the VHF ACARS frequency of around 130MHz). If in doubt, LMR-400 is the coax to use.   
   
   Ok, so you have the antenna mounted and pointed roughly in the [right direction](Inmarsat.md), now where to tune the SDR software?

## Inmarsat L-Band Frequencies and Data Rates ##  

### 4A4F4 25-East
1545.1150 GES:90 600  
1545.1200 GES:90 600  
1545.1250 GES:90 1200  
1545.1300 GES:90 600  
1545.1600 GES:C5 600  
1545.1650 GES:C5 600  
1545.1850 GES:C5 600  
1545.1900 GES:C5 600  
1545.2150 GES:C1 600  
1545.2200 GES:C1 600  
1545.2250 GES:C1 600  
1546.0130 GES:90 10500  
1546.0270 GES:90 10500  
1546.0430 GES:C1 10500  
1546.0920 GES:C1 10500  
1546.1080 GES:C5 10500  
1546.1200 GES:C5 10500  
     
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/alphasatLband.PNG" height="400">       

### 3F5 54W  
1545.0300 GES:43 600  
1545.0350 GES:44 1200      
1545.0400 GES:43 600  
1545.0450 GES:44 1200    
1545.0950 GES:44 600  
1545.1000 GES:02 600  
1545.1350 GES:44 600  
1545.1400 GES:43 1200  
1545.1790 GES:43 600  
1546.0550 GES:44 10500  
1546.0700 GES:43 10500  
1546.0850 GES:44 10500  
   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/54wL-Band.png" height="380">  

### 4F3 98W  
1545.0500 GES:05 600  
1545.0600 GES:D0 600  
1545.0650 GES:D0 600  
1545.0750 GES:D0 1200  
1545.0800 GES:05 600  
1545.0850 GES:D0 600  
1545.0900 GES:05 600  
1545.1000 GES:02 600  
1545.1700 GES:02 600  
1545.1750 GES:02 600  
1546.0050 GES:D0 10500  
1546.0200 GES:D0 10500  
1546.0630 GES:02 10500  
1546.0780 GES:05 10500      
  
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/98w_L-Band_rtlsdr_activepatch.PNG" height="380">  

### 4F1 143E  
1545.025 GES:50 600   
1545.030 GES:82 600  
1545.035 GES:82 600   
1545.040 GES:85 600   
1545.045 GES:85 600   
1545.055 GES:50 600   
1545.070 GES:50 1200    
1545.095 GES:85 600   
1545.135 GES:50 600   
1545.140 GES:50 600   
1545.145 GES:50 600   
1545.150 GES:50 600   
1545.155 GES:85 600   
1545.180 GES:82 600   
1545.210 GES:82 600   
1546.005 GES:50 10500   
1546.035 GES:50 10500   
1546.055 GES:85 10500   
1546.070 GES:82 10500   
1546.085 GES:50 10500   
   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/143eL-Band.png" height="380"> 
     
## Software setup and tweaks    
With the antenna mounted and the coax run, we can focus on the software side of things.   
I am going to proceed as if you are going to set up and monitor all data channels around the clock and you are going to feed your data to your local Node-RED for message filtering (ie just Military aircraft) and reporting / alerting.   

In sort you need to run Jaero, thats the only software package that can decode the AERO data. You can run it on Windows or Linux.  
You also need to run some SDR dongle sofware, on either Windows or Linux there are lots of options.    
Each has their own page from my [Home](README.md) page.


<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-HGJWTNL65R"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'G-HGJWTNL65R');
</script>