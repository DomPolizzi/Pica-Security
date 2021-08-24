# Pica-Security
This project is designed to assit SecOp and privacy Enthusiasts make a "Hardened" Rasberry Pi.

## The Goal

This project is meant to be easily replicatable and simple to follow and tweak. 

From my own journey, this project has had to be done from scratch a few times.

the internet is WILD and a mess to get proper answers for ARM/ Pi tutorial beyond single use cases.

easily replicatable and simple to follow and tweak. From my own journey, this project has had to be done from scratch a few times.


## The Environemnt:

A rasberry Pi running Ubuntu server, headless, will utilize virtualization and containers to host a DNS server, Proxy Server, IDS/IPS, and an IDE.


This headless device is still being tested; howeever, it will include a TOR docker Proxy, Snort IDS/IPS, PiHole, and a IDE accessible via web.


### Server Image:

All of this will run on Ubuntu Server ARM64 img:
https://ubuntu.com/download/server/arm


### Tools:

Docker on Rasberry Pi requires the ARM install, please follow the docks on Dockers site:
https://docs.docker.com/engine/install/ubuntu/


PiHole Docker image is also located on the PiHole site
https://github.com/pi-hole/docker-pi-hole/#running-pi-hole-docker

"CLOUD" IDE that is hosted in a webbrowser (essentially cloud9.io but hosted on a LAN and not owneded by amazon):
https://github.com/cdr/code-server

The Snort IDS/IPS is configured and operational:
https://upcloud.com/community/tutorials/install-snort-ubuntu/


Currently the Docker Tor Proxy is configured, tested, and working smoothly:
https://github.com/DomPolizzi/Pica-Security/tree/main/Tocker
(If you want to create your own its easy ;)



## Current Status:

Update 8/23/21:
 I am not satisfied with results yet to create publically available ISO. 
 
 All the pieces are here but the time and testing is what needs to be done now.
 
Currently I am working on this privately and more pushes will be made in the following weeks.

~ Dom



