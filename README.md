# Using Node-RED to manage ADSC, ADSB, ACARS, VDL2, HF-DL and other aircraft type messages.

Navigation: [autoTLE](autoTLE.md) : [OpenSkyAPI](OpenSkyAPI.md) : [VRS](vrs.md) : [MQTT](mqtt.md) : [VHF-VDL2](vhf-vdl2.md)

So many message types, so many different message paths and sources but all involving aircraft.

Pull them all together, add context and map them with Node-RED. Put all that on a central web dashboard.

### Raspberry Pi or Windows PC or Linux Box?

Begin with the end in mind as my boss used to say. Where you run Node-RED depends on how much you want your system to grow.

###  READ THIS!

My motto is 'fail fast, fail often'. I am NOT a programer. Do NOT use any of the code shown here. These pages and the code on them are for entertainment use only.

### Support or Contact

I will do my best to support your Node-RED aircraft spotting / tracking adventures, but please keep in mind, I am NOT a programmer. I honestly have no idea or right to be doing any of this, so your milage may vary. Also, since I am not a programmer (Have I mentioned I am not a programmer?), I have no idea what a 'pull request' is or how to deal with one, so if you raise one... yeah, sorry... I can't help.

This is an image of how to NOT hook up your linear actuator motor to your dish.   
Look at the top connection, see how its attached to pivot point, this means the up and down motion will not be the same.   
   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/linear%20actuator.PNG" height="500">