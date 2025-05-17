---
title: A fun hardware project - tracking BLE devices that pass by my window
---

# Intro

This semester my girlfriend is taking a class called wearable technology, she needed my help to build and code an arduino that would change colors on her earings based on what site she was on and whether someone could disturb her or not.

Helping her with that sparked something in me and made me want to tinker some more.

# The idea

The first thing that came to my mind is data. I love it, and love doing things with it. Since her project used bluetooth to communicate, thats where I started to.

The idea is to have an arduino that logs all the bluetooth devices it detects and the timestamp when it was detected, then send that data over wifi to a server that adds it to a database.

Then once I have the data, I can find out which devices are seen around that same times (and clean out the devices that are in my building). 

I am curious what I will find!

# Hardware

To start I am just planning on using an Arduino R4 (usb-c, wifi, BLE), and my mini-pc from my old homelab project to host the server with the database.

![The arduino R4](/assets/homelab/r4.jpeg)
![My Mini-pc](/assets/homelab/mini-pc.jpeg)


# Getting started

Honestly I didn't know much about Bluetooth, and I have been learning more. But I was particularly disapointed to learn that the bluetooth on the arduinio (BLE) may not be able to detect the phones and other normal bluetooth devices that pass by (not even 100% sure of this now still trying to learn).


I already got the arduino to connect to my wifi and detect BLE devices, next I want to setup the postgres database I will be using and start collecting data!


Next step was to setup a development environment on my Mini-PC with Ubuntu server as the OS.

My plan is to setup a postgres docker container, then use Bun.sh to run a simple webserver that will accept data from the arduino and push to to the DB.


![VM](/assets/homelab/setting_up_vm.png)


# The Arduinio code

When I build thing sI like to do it step by step, brick by brick.

So first I wrote the arduino code to detect nearby devices/peripherals. Once that was working I moved on to adding the ability to connect to wifi.

Since we were almost done, I moved onto setting up the app server.

I used postgres in a docker and set it up with a super simple schema, only collecting M.A.C address, local_name, and timestamp.

Recently I have fallen in love with using Bun for quick scripting so used it to spin up a simple web server that would accept the data as query params 

such as https://MYSERVER/?mac=THEMAC&local_name=LOCALNAME


# Data analysis


Now lets get to the fun part of the project. Playing around with all the data.

This usually is just an expirmentation process, until you develop a hypothesis or question and then develop a query/analysis to answer it.

Lets start by seeing which days of the week have the most traffc

# CREATE AND SHOW GRAPH VISUAL

Now lets see based on hour, which hours had more or less traffic.


# SHOW VISUAL DISCUS THE 

When breaking this down by specific days of the week, are there any days that experience anomolies or go outside of