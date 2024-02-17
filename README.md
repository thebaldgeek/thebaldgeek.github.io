# Decoding ADSC, ADSB, ACARS, VDL2, Iridium, HF-DL and other aircraft type messages.

Navigation: [Inmarsat](Inmarsat.md) : [L-Band](L-Band.md) : [C-Band](C-Band.md) :  [VHF-ACARS/VDL2](vhf-acars.md) :  [dumpHFDL](dumpHFDL.md) : [Iridium](Iridium.md) : [STDC](stdc.md) : [Jaero](jaero.md) : [SDRReceiver](SDRReceiver.md) : [Radiosonde](radiosonde.md) : [DragonOS](DragonOS.md) : [autoTLE](autoTLE.md) : [OpenSkyAPI](OpenSkyAPI.md) : [VRS](vrs.md) : [MQTT](mqtt.md) : [Raspberry Pi](raspberrypi.md) : [Telegram Bot](telegram.md) : [UAV-Drone](UAV-Drone.md) : [Squawk](Squawk.md) 

# The main ACARS website

You can search a lot of satcom ACARS feeds (and some HFDL / VHF VDL ones as well) on the site:-    
[tbg1.airframes.io](https://tbg1.airframes.io/)   
Site menu is in the top left corner (three bars), be sure and check out all the pages, there is a bit of a mashup there - even some marine data.   
Please note that the website is now under 'feature freeze'.    
The code base that Node-RED used to build it on is end of life. I will consider bug fixes, but new features will be warmly welcomed for v2 of the site which I am actively building. No ETA on its launch, but there are a lot of very compelling reasons why I am locking development of the v1 site and working on v2.   
The main feature I am looking to impliment in v2 is to have the site responsive. The v1 site currently does not resize itself to match the browser resolution, thus its a real drag to use on a phone (which a crazy number of people do).
   
## About this website  
This website is just a brain dump and rough help notes to assist others in getting the hardware and software together to receive and decode ACARS messages from the main modes/frequencies.    
Its not perfect, its not finished, its not polished, it never will be..... in time, these pages will fade as more help docs are written over at [docs.airframes.io](https://docs.airframes.io/)   
   
# About ACARS    
Please take the time to [read this overview of ACARS](https://www.pentestpartners.com/security-blog/introduction-to-acars/). Its one of the best introductions of ACARS from signal to data I have ever come across.    


###  READ THIS!

My motto is 'fail fast, fail often'. I am NOT a programer. Do NOT use any of the code shown here. These pages and the code on them are for entertainment purposes only.   
The best way to put this is: `I don't know what I'm doing, but I know that I don't know what I'm doing.`  


### Support or Contact   

I am happy to help those that try and help themselves.... In other words, if you don't read these pages and ask questions that are clearly answered here then my responses will be limited.     
   
If you have some ideas about improving the site, here is my starting point - "A problem well stated is a problem half-solved. Charles Kettering - Inventer".   
The better you can describe your suggestion, the better chance you have of seeing it show up on the site.    
   
Check back often, this site is being updated randomly.   
    
I am pretty active on [X / Twitter](https://twitter.com/thebaldgeek).       
The best way to keep updated with the goings on of all things ACARS is via X. There are many #osint folks on X that combine the usual ADSB (aircraft on a map) with ACARS to really amplify both sources of data. The sum really is MUCH greater than the parts.   
Do note that I don't Tweet actual OSINT information... My site/tweets/role is to provide raw OSINT data. Ive found that most people that do osint often don't know where the data they use comes from, my goal is to help people understand how RF (radio frequency) signals can be converted into useful data for people to analyze.   
Tip, my Tweets are public, so you don't need a Twitter account to read them.  
Free Twitter reader can be found on [nitter](https://nitter.net/thebaldgeek/with_replies)   
    
Not as active, but am also on <a rel="me" href="https://ioc.exchange/@thebaldgeek">Mastodon</a>   
If you have 15 minutes to look at some real world examples of ACARS data, look back through the [Reddit ACARS](https://www.reddit.com/r/ACARS/) sub.   
Less active, but I'm also on [BlueSky](https://staging.bsky.app/profile/thebaldgeek.bsky.social)   

   
If you want more of a traditional forums, then airframesio have that as well, join us over at the [airframes community](https://community.airframes.io/)   
The whole ACARS team is very active on the [airframes discord](https://discord.com/invite/airframes)  
    
For even more searchable ACARS data (over 2 Billion ACARS messages stretching back a few years) and information on how to feed the different ACARS modes, please support [airframes.io](https://app.airframes.io/about)   
You can also follow them on Twitter [AirframesIO](https://twitter.com/AirframesIO)   
   
<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-HGJWTNL65R"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'G-HGJWTNL65R');
</script>