# Moving ACARS data from Jaero to a remote server with MQTT.   
   
Navigation: [home](README.md)  

One of the problems with Jaero is that it can not use host names in any of its settings, only IP addresses.  
At first we simply used my web IP address, but it changes about 2-4 times a year and so you need to change the IP in around 20-30 Jaeros at each ground station, that gets old pretty quick.   
Thankfully most remote sites are happy to install Node-RED and so you can just put the Node-RED computer IP address into Jaero and you are done on that side of things. 
   
On the Node-RED side of things, you place a UDP input node (since Jaero uses UDP to send the ACARS messages) and connect its output to an MQTT output node. Configure the MQTT server hostname and port, add the user/pass and your done. Very quick, very clean, and no open ports at the remote site.  
Pick a high UDP port number, but something you can keep track of and is logical, say 40100 for the first one and go up from there.   
Use the same port number in each Jaero (unless you want to track which aircraft are using which channels on the satellite)
This is how it looks.   

![UDP to MQTT](img/udptomqtt.png) 

And here is a sample flow to you started:   
   
    [{"id":"875cf8f.c3aeb88","type":"udp in","z":"4118d274.45b1fc","name":"From Jaero","iface":"","port":"40100","ipv":"udp4","multicast":"false","group":"","datatype":"utf8","x":940,"y":960,"wires":[["56d3f153.db0608"]]},{"id":"56d3f153.db0608","type":"mqtt out","z":"4118d274.45b1fc","name":"To Broker","topic":"98w/Lband","qos":"","retain":"","broker":"7f9bce06.c1f8","x":1160,"y":960,"wires":[]},{"id":"7f9bce06.c1f8","type":"mqtt-broker","name":"MQTT_Broker","broker":"yourmqttbrokerhostname.com","port":"1883","clientid":"","usetls":false,"compatmode":false,"keepalive":"60","cleansession":true,"birthTopic":"","birthQos":"0","birthPayload":"","closeTopic":"","closeQos":"0","closePayload":"","willTopic":"","willQos":"0","willPayload":""}]

There are lots of reasons why MQTT is the right tool for the job, but the one I like the most is that I only need one open port on my router, no mater how many ground stations are feeding me data, or what kind of data, I just use different topics for the different stations and it all stays neatly sorted in the both the broker and in my server Node-RED instance.

If any readers of these pages are running an L-Band or C-Band ACARS Satcom station and would like to share their data via MQTT, just drop me a line and I will send you the broker details.