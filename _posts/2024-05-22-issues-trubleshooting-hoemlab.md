---
title : Just a HomeLab Log
---

In my last post I was able to get VLAN's working on my Cisco C3560CX switch as well as inter-vlan networking.

## 05-22-24

Was able to get all my homelab servers on their own VLAN. Currently I only have a:
1. Proxmox Server - BeeLink
2. Synology NAS

But I will probably add some RPI's (and cluster them)


After I finished setting up the Proxmox box to work on the correct interface I created two virtual machines:
1. PiHole - DNS Sinkhole to prvent unwanted ads on all devices on the network
2. OpenVAS - An open source Vun scanner
	- Was able to set this up to run against my Synology NAS, and then setup a nightly scan for my remote webservers

The next vm I would like to make is for Graphana, but I might save that for the raspberry pi's


## 05-23-24

Because I am still learning, I may be attemping to solve a problem that does not need to be solved.

Right now I have my switch connected to my router, and everything works great.

I setup a VPN on the router so I can connect from anywhere with my Laptop. From the VM I can connect to the Router and the Cisco Switch, but for some reason I cannot reach any of the devices within the Cisco VLAN's. I know VLANs are meant to be isolated so maybe this behavior makes sense, however I would really want to be able to manage all my servers/network devices remotely.

I will take a look at some more resources and do some more learning, but a simple solution would also just be to have a Proxmox VM that functions as a VPN. That way I will already be inside the Cisco switch and networking between VLAN's should work perfectly. (Inside the VLAN can also access devices outside the vlan).
