# A few tips for running a Raspberry Pi as an ACARS station #   
   
Navigation: [home](README.md)

The Pi can support 3 USB dongles with a good quality power supply. Most people will want to run an ADSB dongle, an ACARS dongle and a VDL2 dongle.   
   
Here is how to set the Pi timezone / clock to UTC:   
First run `sudo raspi-config`  
From the main menu, slect option 5.   

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/pilocaloptions.png" height="470">   
   
Then select your Timezone menu option:  
   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/pitimezone.png" height="470">  

Then select 'None of the above' (yeah, not so obvious is it...):  
   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/pinoneoftheabove.png" height="470">  
   
Then select UTC:  
   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/piutc.png" height="470">   

- - - -

## Jume 2024. Ignore this section    
ZeroTeir is on tbg nasty list after doing a bait-and-switch. Ovoid them at all costs.       


## ZeroTeir ##
I access all my remote Pis (and a few Windows PCs needed for Jaero etc) via ZeroTier.com can not speak more highly of it.  
Here is how to quickly install it on a fresh Pi:  
`curl -s https://install.zerotier.com/ | sudo bash`  
`sudo systemctl enable zerotier-one`  
`sudo zerotier-cli status`  
`sudo zerotier-cli join YourZeroTeirNetworkID`  
Authenticate and name this Pi by going to your network on their website.  
`sudo zerotier-cli listnetworks`  
`sudo touch /var/lib/zerotier-one/networks.d/YourZeroTeirNetworkID.conf`  

<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-HGJWTNL65R"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'G-HGJWTNL65R');
</script>