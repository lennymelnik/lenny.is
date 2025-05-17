---
title : Building my Homelab - The Switch Challenge
---

As I mentioned in my previous post, this is not my first Homelab. My last one was huge, loud, and took so much power. But I loved it. 

Every time I would go into the closet it brought me so much joy, so I am trying to recreate that feeling (plus so much more) with my V2 Low Power / Volume homelab.


# The Challenge

When you don't know anything, its harder to start learning. You don't even know what questions to ask. Once you start learning and getting better, you realize how much you don't know and understand. Yet you have the ability to ask better questions and at least know what you need to learn.

This was my first time interacting with a Cisco device, let alone a managed switch.

I found my Cisco C3560CX off EBay for $150, while its much more expensive than a "Smart" managed home/small buisness switch off Amazon, the main goal with building this homelab is to learn.

The switch itself looks great and is fanless (which I intensionally looked for).

## Getting started

So as soon as I got the switch I wanted to plug it in and get going. Unfortunatly while the power port is pretty standard, it does require a notch in the cable (which I did not have), so I went ahead and ordered the cable off Amazon and waited a horribly long two days.

After first plugin I realized, shit how do I interact with this. To YouTube I went.

Luckily I had an old USB cable and was able to login to the console through that. But when the system prompted me for a password I had no idea what to put (It was a used system after all).

The solution was to hold the the 'mode' button on power on for as long as humanly possible until you see something popup on your screen about passwords. I had previously held it slightly less than humanly possible and that did not work out.

After that I copied the old configuration file, and reset the current one.

Then after resetting I was able to login to the switch!


## Actually using it

So what to do now, if I plug everything into the switch I get internet, but whats the fun in that?

I started looking into how to create VLAN's, I could not find a solution that worked (for a non-cisco router) so I turned to ChatGPT which was a complete waste of time.

The solution ended up being so simple.

1. Plug in router to switch

2. Create your VLANs
3. Enable ip routing so the devices on VLANs can communicate across VLANs
4. Assigned them an ip (192.168.XX.1) in my case
5. Assign an IP on the main subnet to the switch
6. Setup DHCP on each VLAN
7. Configure a Static Route that handles 192.168.xx.0 requests and sends them to the IP of the switch on the main subnet.

And bam it worked!

After that I changed my wifi router to function as an access point and put it on its own VLAN.

# Next steps
My next steps are to create a separate VLAN for my servers and homelab equipment (NAS, Proxmox).

Then I want to setup a bunch of different services to play around with and learn.

1. PiHole
2. OpenVAS
3. Graphana
... and many more

See you then!
