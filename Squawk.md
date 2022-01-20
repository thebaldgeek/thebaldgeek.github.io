# Background of the Squawk page.   
   
Navigation: [home](README.md)  

I have been sending 7700 (emergency) squawks to the Telegram bot while I test the Node-RED flow. While in that testing phase a guy on the ADSBExchange Discord server asked me if there was a place on my website for squawk codes... Duh..   

Both ADSB and ADSC data often (but not always in the case of satcom ADSC data) have squawk codes in them.  
    
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