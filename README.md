# lx-livestream

An incomplete experiment to provide streaming live lighting data to accompany a live performance (eg concert or sporting event) to users of home smart lighting (eg Philips hue) 

The idea is that you configure a number (in this example - four) of additional RGB fixtures on a lighting console (we used ETC Eos in testing) and output the data for them as Art-Net. 

The Art-Net data is received by a process on the lighting network which relays it to a cloud server. 

Clients connect to this cloud server and control local lighting devices (e.g. Philips Hue, LIFX) by API or present DMX / Art-Net data for larger venues that can connect this data to their existing lighting system.

## Components 

### Server

The server application is designed to run on a cloud based service, it's a very simple script that listens for connections from the transmitter and rebroadcasts them to any of the connected clients with a configureable delay.

Currently this uses WebSockets although in theory anything else could be used, including embedding within a media stream.

### Client
There are three clients at present;

lx-livestream-rx-hue: this is a simple client that connects to a hue bridge and changes the colour of a single connected lamp. (TODO: rewrite this to use Hue Entertainment Mode and support multiple lamps)

lx-livestream-rx-dmx: this will spit out RGB Art-Net data more or less as received for four channels

lx-livestream-rx-web: this displays a simple HTML page with four areas which correspond to the colours being sent. This was used in testing with good success with an app that allowed control of "ambilight" type TVs using an external input 

### Transmitter

This is designed to run on simple generic hardware on the production network, it listens to Art-Net traffic and effectively emulates three RGB fixtures. 

## Limitations / Improvements etc.

Far too many to list, this was a proof of concept and is here for future reference. It may or may not be developed into something that works more reliably in the future depending whether or not I need it for a future project. 

* The client apps need to be user-friendly, they aren't yet.
* The applications are not particularly tolerant to lossy networks
* The server is extremely primitive, especially the delay logic, and there's room for improvement
* More flexibiltiy in number of channels etc.
* Stablility! 

