# Background of the Squawk page.   
   
Navigation: [home](README.md)  

I have been sending 7700 (emergency) squawks to the Telegram bot while I test the Node-RED flow. While in that testing phase a guy on the ADSBExchange Discord server asked me if there was a place on my website for squawk codes... Duh..   

Both ADSB and ADSC data often (but not always in the case of satcom ADSC ACARS messages) have squawk codes in them. VDL2 messages only have squawk codes in them when they originate from a ground station, ie they tell the aircraft what to squawk. So you really are limited to ADSB messages for squawk codes.  
    
### Squawk codes for UK
Code meanings are very regional. I have found a list for the UK only at this stage. You can find the [flat list here:](https://github.com/thebaldgeek/thebaldgeek.github.io/blob/main/img/squawk/UKsquawkcodes.csv)   
Until I get lists for other regions, I can only look up aircraft codes for the UK and a bit of Europe. Here is the bounding box that the site is using for squawk code look ups:   

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/squawk/ukbox.png" height="380">  
   
   Do note that we have seen aircraft squawk say 0130 for example as they leave Germany, but they keep squawking 0130 as they flew over Scotland and got ready for the oceanic clearance. They they dropped off ADSB and did not run ADSC so I don't know if they changed codes at any stage. Point is, its up to the pilot to choose the code and where/when they change or set it.  

### Node-RED function block code   
I use the following mess in a function node to check incoming messages for the word squawk or code: and go from there.    
     
```   
// Check if we have a message with the word squawk in it.
if (msg.raw.includes('SQUAWK')){

    skip = msg.raw.indexOf('SQUAWK');
    start = msg.raw.indexOf(' ',skip)+1;
    end = msg.raw.indexOf('' ,start)+4;
    msg.squawk = msg.raw.substring(start,end);
    
    // Check if the squawk code we just found is all numbers (ie valid)
    if (/^\d+$/.test(msg.squawk)){
            msg.payload = {
            Timestamp: msg.payload.Timestamp,
            ICAO: msg.payload.ICAO,
            Rego: msg.payload.Rego,
            Type: msg.payload.Type,
            Desc: msg.payload.Desc,
            ADSBEx: msg.link = "https://globe.adsbexchange.com/?icao="+ msg.payload.ICAO,
            Raw: msg.raw,
            Squawk: msg.squawk,
            Sat: msg.payload.Sat
        }
    
        return msg;
    }
    
    
    // L-Band often has the squawk code formatted differently
    skip = msg.raw.indexOf('CODE:');
    start = msg.raw.indexOf(' ',skip)+1;
    end = msg.raw.indexOf('' ,start)+4;
    msg.squawk = msg.raw.substring(start,end);
    
    // Check if the squawk code we just found is all numbers (ie valid)
    if (/^\d+$/.test(msg.squawk)){
        msg.payload = {
            Timestamp: msg.payload.Timestamp,
            ICAO: msg.payload.ICAO,
            Rego: msg.payload.Rego,
            Type: msg.payload.Type,
            Desc: msg.payload.Desc,
            ADSBEx: msg.link = "https://globe.adsbexchange.com/?icao="+ msg.payload.ICAO,
            Raw: msg.raw,
            Squawk: msg.squawk,
            Sat: msg.payload.Sat
        }
    
        return msg;
    }
}    
```
From there it simply is routed to a FIFO node and the ui_table node. For once a simple 3 node flow.

<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-HGJWTNL65R"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'G-HGJWTNL65R');
</script>