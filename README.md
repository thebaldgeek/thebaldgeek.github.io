# Using Node-RED to manage ADSC, ADSB, ACARS, VDL2, HF-DL and other aircraft type messages.

Navigation: [Inmarsat](Inmarsat.md) : [L-Band](L-Band.md) : [C-Band](C-Band.md) :  [VHF-ACARS](vhf-acars.md) : [Jaero](jaero.md) : [SDRReceiver](SDRReceiver.md) : [autoTLE](autoTLE.md) : [OpenSkyAPI](OpenSkyAPI.md) : [VRS](vrs.md) : [MQTT](mqtt.md) : [Raspberry Pi](raspberrypi.md): [Telegram Bot](telegram.md) : [DragonOS](DragonOS.md) : [UAV-Drone](UAV-Drone.md) : [Squawk](Squawk.md) : [Iridium](Iridium.md)

# Node-RED Dashboard - The main website

Live ACARS, VDL2, HF-DL, Inmarsat C-Band, L-Band and Iridium messages for most of the planet - broken down into different bands and types of aircraft's (like Military, Bizjets, UAV etc).  
<a href="https://acars.adsbexchange.com/" rel="noopener" target="_blank">https://acars.adsbexchange.com/</a>   

The site menu is on the top left (the three bars).  
On your first visit you should view each of the pages and see what is on offer. On future visits *pay attention to the update log page on the main 'Home' page* This is the best (and only?) way of finding out any new features that has been added.   
Please don't bookmark any other pages other than the main one linked here. I have a habit of moving pages around, adding and subtracting them and this will break your bookmarks. Just use the main URL and site menu and you never have to worry.   
I am constantly working on the site. The site is a case of function over form. It is not really 'friendly', but it is rather powerful.
For example, you can filter on commercial or military CPDLC messages, or ACARS messages in general. Tip: The site search page is a rolling buffer of the past 48 hours of ACARS messages. And no, I don't keep any other logs or history. 

## About  
The Node-RED dashboard site is fed from Inmarsat 98W (4F3), 54W (3F5), 143E (4F1) and 25E (AF1). Each of these locations feed C-Band and L-Band data to the site via MQTT.   
There are a few people that generously share their data from different parts of the globe (Asia Pacific, the Americas and UK).  
  
While all of us work hard to keep our data feeds up and running 24*7 we are all just aviation enthusiasts with families and day jobs, keep that in mind as you view the data.  
If you have an ADSC satellite dish setup and would like to feed your data to the site, please let me know.

###  READ THIS!

My motto is 'fail fast, fail often'. I am NOT a programer. Do NOT use any of the code shown here. These pages and the code on them are for entertainment purposes only.   
The best way to put this is: `I don't know what I'm doing, but I know that I don't know what I'm doing.`  


### Support or Contact

I am happy to help those that try and help themselves.  

Check back often, this site is being updated randomly.   

I am pretty active on [Twitter](https://twitter.com/thebaldgeek) if thats your thing.  
Tip, my Tweets are public, so you don't need a Twitter account to read them.   
    
For ACARS data and feeding, please support [airframes.io](https://app.airframes.io/about) You can also follow them on Twitter [AirframesIO](https://twitter.com/AirframesIO) 
<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-HGJWTNL65R"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'G-HGJWTNL65R');
</script>