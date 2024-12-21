# Decoding ADSC, ADSB, ACARS, VDL2, Iridium, HF-DL and other aircraft type messages.

Navigation: [Inmarsat](Inmarsat.md) : [L-Band](L-Band.md) : [C-Band](C-Band.md) :  [VHF-ACARS/VDL2](vhf-acars.md) :  [dumpHFDL](dumpHFDL.md) : [Iridium](Iridium.md) : [STDC](stdc.md) : [Jaero](jaero.md) : [SDRReceiver](SDRReceiver.md) : [Radiosonde](radiosonde.md) : [DragonOS](DragonOS.md) : [autoTLE](autoTLE.md) : [OpenSkyAPI](OpenSkyAPI.md) : [VRS](vrs.md) : [MQTT](mqtt.md) : [Raspberry Pi](raspberrypi.md) : [Telegram Bot](telegram.md) : [UAV-Drone](UAV-Drone.md) : [Squawk](Squawk.md) : [wardrive](wardrive.md)

# The main ACARS website

You can search and live view a lot of satcom ACARS feeds (and some HFDL / VHF VDL ones as well) on the site:-    
    
[tbg.airframes.io](https://tbg.airframes.io/)   
The closest thing there is to a 'users guide' for the site is [here](https://community.airframes.io/t/website-overview-tbg-airframes-io/159)   
       
Please note that the website is a dumpster fire. (ie, full of bugs and glitches).   
    
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/dumpstaFire.png" height="320">    
   
Honestly, thats part of its quirky appeal. Jokes aside, tbg is not a programmer, he is the wrong guy to be doing this, but here we are...   
If you want a more solid ACARS website, check out [airframes.io](https://airframes.io), they are the real deal over there.   
The way we think of the two websites is that tbg.airframes is the scrappy ally cat that makes all the mistakes, ACARS on the bleeding edge. Airframes.io is the powerful puma, ACARS done right.   
The sites are not really 'connected' beyond they both are ACARS centric and run by good mates. thebaldgeek is gratefully hosted by airframes. It is CRITICAL that if you setup an ACARS station that you feed airframes.io first and foremost.         
    
Map with ADSC and ACARS plotted together:    
[tbgmap.airframes.io](https://tbgmap.airframes.io/)   
Tips for using the map - and you REALLY REALLY should read them - can be found here:   
[tbg map notes](https://tbg.airframes.io/dashboard/map)
    
  
# What even is ACARS??    
Get a solid intro by [reading this overview of ACARS](https://www.pentestpartners.com/security-blog/introduction-to-acars/). Its one of the best introductions of ACARS from signal to data I have ever come across.    
   
There are many osint folks and avgeeks that combine the usual ADSB/C data (aircraft pixels on a map) _with_ ACARS to really amplify both sources of data. The sum really is MUCH greater than the parts.   
   
Think of aircraft tracking this way:    
ADSB/C is the where.    
ACARS is the why.   

## About these GitHub pages  
This GitHub 'website' is just a tbg brain dump and rough help notes to assist others in getting the hardware and software together to receive and decode ACARS messages from the main modes and frequencies.    
Its not perfect, its not up to date, its not finished, its not polished, it never will be..... in time, these pages will fade as more helpful docs are written over at [docs.airframes.io](https://docs.airframes.io/)   

###  READ THIS!

tbg motto is 'fail fast, fail often'. thebaldgeek is NOT a programer. Do NOT use the site. Do not read these GitHub pages.  
The best way to put this is: `I don't know what I'm doing, but I for sure know that I don't know what I'm doing.`  


### Support    

I am happy to help those that try and help themselves.     
   
If you have some ideas about improving ACARS readability or decoding of ACARS for the site, here is my starting point - "A problem well stated is a problem half-solved. Charles Kettering - Inventer".   
In other words, the better you can describe your suggestion, the better chance you have of seeing it show up on the site.    
tbg did not come up with any of the pages on the website, each of them are ideas clearly explained by avgeeks around the world.   
Its YOUR website, not thebaldgeeks!          

### Contact  
thebaldgeek is most active on [X / Twitter](https://twitter.com/thebaldgeek). DM's are open.   
If your not on X, you can try the [website chat](https://tbg.airframes.io/dashboard/chat) to connect with tbg and chat about ACARS.  
Not as active, but tbg is also on <a rel="me" href="https://ioc.exchange/@thebaldgeek">Mastodon</a>   
Even less active, but also on [BlueSky](https://staging.bsky.app/profile/thebaldgeek.bsky.social)     
     
   
### Other resources   

Do note that tbg does not Tweet actual OSINT information... My site/tweets/role is to provide raw OSINT data. Ive found that most people that do osint often don't know where or how the raw data they use comes from, my goal is to help people understand how RF (radio frequency) signals can be converted into useful data for people to analyze and thus deepen the intel derived.   
    
If you have 15 minutes to look at some old real world examples of ACARS data, take look back through the [Reddit ACARS](https://www.reddit.com/r/ACARS/) sub.   

If you want more of a traditional forums, then airframesio has that as well, join the [airframes community](https://community.airframes.io/)   
The whole ACARS team is very active on the [airframes discord](https://discord.com/invite/airframes)  
    
For even more searchable ACARS data (over 3 Billion ACARS messages stretching back a few years) and information on how to feed the different ACARS modes, please support [airframes.io](https://app.airframes.io/about)   
You can also follow them on Twitter [AirframesIO](https://twitter.com/AirframesIO)   
   
<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-HGJWTNL65R"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'G-HGJWTNL65R');
</script>