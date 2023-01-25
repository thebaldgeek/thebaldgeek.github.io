# Decoding ADSC, ADSB, ACARS, VDL2, Iridium, HF-DL and other aircraft type messages.

Navigation: [Inmarsat](Inmarsat.md) : [L-Band](L-Band.md) : [C-Band](C-Band.md) :  [VHF-ACARS/VDL2](vhf-acars.md) : [Iridium](Iridium.md) : [STDC](stdc.md) : [Jaero](jaero.md) : [SDRReceiver](SDRReceiver.md) : [Radiosonde](radiosonde.md) : [DragonOS](DragonOS.md) : [autoTLE](autoTLE.md) : [OpenSkyAPI](OpenSkyAPI.md) : [VRS](vrs.md) : [MQTT](mqtt.md) : [Raspberry Pi](raspberrypi.md) : [Telegram Bot](telegram.md) : [UAV-Drone](UAV-Drone.md) : [Squawk](Squawk.md) 

# The main website

Live ACARS, VDL2, HF-DL, Inmarsat C-Band, L-Band and Iridium messages for most of the planet - broken down into different bands and types of aircraft's (like Military, Bizjets, UAV etc).  
<a href="https://acars.adsbexchange.com/" rel="noopener" target="_blank">https://acars.adsbexchange.com/</a>   

The site menu is on the top left (the three bars).  
On your first visit you should view each of the pages and see what is on offer. On future visits *pay attention to the update log page on the main 'Home' page* This is the best way of finding out any new features that has been added.   
Please don't bookmark any other pages other than the main one linked here. I have a habit of moving pages around, adding and subtracting pages and this will break your bookmarks. Just use the main URL and the site menu and you never have to worry.   
I am constantly working on the site. The site is a case of function over form. It is not really 'friendly', but it is rather powerful. For example, you can filter on commercial or military CPDLC messages, or ACARS messages in general. Tip: The site search page is a rolling buffer of the past 48 hours of ACARS messages. And no, I don't keep any other logs or history. 

## About the main website  
The Node-RED dashboard site is fed from Inmarsat 98W (4F3), 54W (3F5), 143E (4F1) and 25E (AF1). Each of these locations feed C-Band and L-Band data to the site via MQTT.   
There are a few people that generously share their data from different parts of the globe (Asia Pacific, the Americas and UK/Euro).  
  
While all of us work hard to keep our data feeds up and running 24*7 we are all just aviation enthusiasts with families and day jobs, please keep that in mind as you view the data.  
If you have an ADSC C-Band satellite dish setup and would like to feed your data to the site, please let me know.   

## About this website  
This website is just a brain dump and rough help notes to assist others in getting the hardware and software together to receive and decode ACARS messages from the main modes/frequencies.    
Its not perfect, its not finished, its not polished..... in time, these pages will fade as more help docs are written over at airframes.io
   
# About ACARS    
Please take the time to [read this ACARS description](https://www.pentestpartners.com/security-blog/introduction-to-acars/). Its one of the best overviews from signal to data I have ever come across.    


###  READ THIS!

My motto is 'fail fast, fail often'. I am NOT a programer. Do NOT use any of the code shown here. These pages and the code on them are for entertainment purposes only.   
The best way to put this is: `I don't know what I'm doing, but I know that I don't know what I'm doing.`  


### Support or Contact

I am happy to help those that try and help themselves.  

Check back often, this site is being updated randomly.   

I am pretty active on [Twitter](https://twitter.com/thebaldgeek) if thats your thing.     
Tip, my Tweets are public, so you don't need a Twitter account to read them.  
Free Twitter reader can be found [here](https://bird.trom.tf/search?f=tweets&q=thebaldgeek)   
Not as active, but am also on <a rel="me" href="https://ioc.exchange/@thebaldgeek">Mastodon</a>   
    
For ACARS data and feeding, please support [airframes.io](https://app.airframes.io/about) You can also follow them on Twitter [AirframesIO](https://twitter.com/AirframesIO)   
#thebaldgeek can be also found on the adsbexchange Discord server - mostly in the ACARS channels.
<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-HGJWTNL65R"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'G-HGJWTNL65R');
</script>