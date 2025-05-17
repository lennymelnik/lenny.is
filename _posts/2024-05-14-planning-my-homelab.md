---
title : "Planning my Homelab"
layout : post
categories : projects homelab 
---
I love tinkering. Infact the only thing I may love more than tinkering is looking at what I have tinkered with. When I was deep into vintage computing, even taking a look at some of my systems would make me feel glee (Primaraly the IBM PC AT with a Model M Keyboard), using or observing them in action was even better.

For a while my projects have soley been software development. However I would like to take up another hobby that makes me use my hands more, as well as have something phsycical that I can observe in my workspace.


## Reasons
So....I am going to make a homelab. I have a couple of reasons for this in no particular order:

1. to learn more about networking and network/system implementation
2. to learn and practice architecting simple to complex systems
3. to have something secure my network and devices
4. to have a more robust backup system/monitoring in place
5. to have a lab to test and learn all sorts of technologies

Because I know what my reasons are, it makes it easeir to plan and budget. Something even better is that I know I don't want to do something big and loud, as thats something I did before (before I was paying for my own eletricity).

## Requirements

The setup has to have the following requirements:

1. Low power and quiet
2. Take up little space
3. Be able to run multiple VM's
4. For every component to be fully managed


## Hardware
Given all this information, I have selected the following components for my homelab:

1. CISCO C3560CX
- Uses CISCO IOS (I heard it called) command line, will give me an oportunity to use and learn what is actually needed in Cisco enterprises. Apparently there are other switches that maybe easier to use, but are just Linkseys rebranded as Cisco and are not the real deal.
- Layer 3, so will let me create the VLANS as well as direct traffic between them
- Got the switch for $150 on EBay which based on what I can see was a decent deal

2. APC UPS Battery Backup & Surge Protector, 600VA
- Just something basic to start off with so that my components don't get damaged just incase

3. TP-Link ER605 V2
- Will be configuring this as a basic firewall/VPN access remotely, but idealy I would like to replace it with Cisco down the line (My current thought but that may and will change)

4. Beelink SER6 Mini PC,AMD Ryzen 9 6900HX
- Wanted a mini-pc with relativly the latest mobile Ryzen processors to run Proxmox on
- Comes with 16gb RAM but I will upgrade that down the line
- For use running a Windows server to practice and learn AD, as well as any other virtualization I need done without needing to use my beefy and powerful desktop.


## Process

I really am going to go around this in a curiosity first way, I want to poke and prod whatever I feel like and really get to understanding these technologies more.

However while I am setting them up, I also will be going through a a CCNA textbook to really understand and practice the knowledge.

Just to make this continued learning and not something I will forget, I want to try to have a massive Anki deck of everything I learn (from this project and others) and do like 30 minutes a day of random cards to make sure as much stays active in my head as possible.

Super excited and cannot wait to get started on all this!
