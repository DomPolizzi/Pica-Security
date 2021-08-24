# Pica-Security
This project is to assist SecOp, and privacy Enthusiasts make a "Hardened" Rasberry Pi.

## The Goal

Pica-Security will be designed to be easily replicable and straightforward to follow and tweak. It will also be designed to allow for personal tweaking and have continuous integration, development, and deployment configured to keep the project relevant and up to date.

From my journey, this project has had to be reworked, redesigned, and started from scratch a few times due to lacking / dated support for ARM architectures. 
The internet is filled with enthusiasts; however, it is a wild mess to get proper and up-to-date answers for ARM/ Pi tutorials beyond single-use cases. PICA-Security will not be this way.



## The Environment:

A headless Rasberry Pi 4B running Ubuntu server will utilize virtualization and containers to host a DNS server, Proxy Server, IDS/IPS, and an IDE.

It will utilize DOCKER containers to manage the applications efficiently and allow for easy patching / Updates. 

Docker Applications include Tocker, Snort IDS/IPS, PiHole, and an IDE accessible via the web.


### Server Image:

All of this will run on Ubuntu Server ARM64 img:

https://ubuntu.com/download/server/arm


### Tools:

Docker on Rasberry Pi requires the ARM install; please follow the docs on Dockers site:

https://docs.docker.com/engine/install/ubuntu/



PiHole Docker image is located on the PiHole site

https://github.com/pi-hole/docker-pi-hole/#running-pi-hole-docker/




Code Serve is a "CLOUD" IDE that is hosted in a web browser (essentially cloud9.io but hosted on a LAN and not owned by Amazon):

https://github.com/cdr/code-server/



The Snort IDS/IPS is configured and operational (just needs to be containerized now):

https://upcloud.com/community/tutorials/install-snort-ubuntu/



Currently, the Docker Tor Proxy is configured, tested, and working smoothly:

https://github.com/DomPolizzi/Pica-Security/tree/main/Tocker

(If you want to create your own, it's easy ;)



## Current Status:

Update 8/23/21:
 I am not satisfied with the results yet to create it publicly available. 
 
 All the pieces are here, but the time and testing are what needs to be done now.
 
Currently, I am working on this privately, and more commits will be made in the following weeks.

~ Dom
