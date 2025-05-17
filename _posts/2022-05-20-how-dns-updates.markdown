---
title : "How does DNS actually update?"
layout : post
categories : privacy thoughts
---
# How DNS actually update?

I won’t go into depth on DNS. But I’ll tell you what you need to know if you run a basic website 

# Introduction

First let's start with what DNS is. It stands for Domain Name System. For humans to access websites we use domain names such as

- google.com
- facebook.com

Whereas our computers communicate via IP (Internet Protocol) addresses. 

IPv4 : 192.168.0.0

IPv6: 2400:cb00:2048:1::c629:d7a2

Although IPv6 (IP version 6) is newer and better, IPv4 is still the main one used.

DNS translates the domain names to IP addresses.

# Using DNS Under the hood

On Mac we can use the command "dig" to see inside the box on how dns finds the corresponding IP address for a given domain name

```bash
dig leonardmelnik.com 
```

Will output

```bash
; <<>> DiG 9.10.6 <<>> leonardmelnik.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 8965
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
;; QUESTION SECTION:
;leonardmelnik.com.		IN	A

;; ANSWER SECTION:
leonardmelnik.com.	723	IN	A	50.21.186.219

;; Query time: 6 msec
;; SERVER: 172.20.10.1#53(172.20.10.1)
;; WHEN: Tue Dec 07 14:48:56 EST 2021
;; MSG SIZE  rcvd: 62
```

Lets break this down

```bash
; <<>> DiG 9.10.6 <<>> leonardmelnik.com
```

> This first line shows the version of DIG we are using, as well as what we are searching ( querying for)
> 

```bash
;; global options: +cmd
```

> This line just shows what options, I guess this is the default for no options?
> 

```bash
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 8965
```

> Finally we have something that looks more or less understandable.
> 

As you can see on status it says NOERROR. This means.. we had no errors. The other possibilities for status are 

- SERVFAIL - The domain name exists, but the there is no data
- NXDOMAIN - The domain name does not exist
- REFUSED - The DNS server does not have the information and they don't want to send you anything to make up for it

```bash
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1
```

> Then we have the flags, this is just to count what kind of results we have. What we want to see is the ANSWER: 1. In our case we had a direct answer. But normally it goes step by step. Basically you ask for information, one server doesn't have it, but it tells you who will have the information. And you keep asking the next server until you get the answer. ( I will make a post going much more in depth)
> 

```bash
;; QUESTION SECTION:
;leonardmelnik.com.		IN	A
```

> The question section basically repeats what you are asking for
> 

```bash
;; ANSWER SECTION:
leonardmelnik.com.	723	IN	A	50.21.186.219
```

> The answer section is exactly what we are looking for, or will tell us where to look next.
> 

Just to add titles our data is this

| Domain Name | Cache Time | Type | IP Address |
| --- | --- | --- | --- |
| leonardmelnik.com | 723 seconds | A | 50.21.186.219 |

If I repeat the command again I get the same answer except the Cache Time is lower (Since time past)

```bash
;; ANSWER SECTION:
leonardmelnik.com.	575	IN	A	50.21.186.219
```

Basically this means our computer or the DNS servers know what the IP for "leonardmelnik.com" is. This helps because since it remembers, if it wants to access "leonardmelnik.com" it can use the stored (cached) IP instead of asking all over to find it.

> But in 575 seconds it would have to delete it from its memory and will have to find it again.
> 

This is very important, because without asking for the IP every X seconds. How would we find the new IP if the website was updated?

## DNS Propagation is Pull not Push

The term "DNS Propagation" is wildly misleading.

To propagate is to spread something. Which means in you will receive without asking. In terms of DNS this means if I update a record on my domain (for example using goDaddy)

But when it comes to DNS, you only receive the new IP address for the domain if you ask for it.

A cool thing about this is, if you make a new domain record, and add all the information

![Screen Shot 2021-12-07 at 3.14.01 PM.png](/assets/dns/Screen_Shot_2021-12-07_at_3.14.01_PM.png)

> You may be wondering. What is the name field?? Well that is what goes before your domain. For goDaddy if you want no subdomain its just @ for example
> 

If we are editing the DNS Records for example.com

| Name | Final Domain |
| --- | --- |
| @ | example.com |
| hello | hello.example.com |
| goodbye | goodbye.example.com |
| even.two | even.two.example.com |

> We can choose the TTL (Time To Live) which basically tells DNS servers to search for the IP again after every _____ amount of time
> 

![Screen Shot 2021-12-07 at 3.15.31 PM.png](/assets/dns/Screen_Shot_2021-12-07_at_3.15.31_PM.png)

![Screen Shot 2021-12-07 at 3.17.01 PM.png](/assets/dns/Screen_Shot_2021-12-07_at_3.17.01_PM.png)

So I just added this record. The domain will be [testingdns.lennymelnik.com](http://testingdns.lennymelnik.com) 

and it will point to 111.111.111.111. But DNS servers should only remember that for 30 minutes.

After clicking the button 

> Add Record
> 

You would think the new information is spreading to all DNS servers worldwide? NOPE.

As we mentioned before, servers will only know if they ASK for it.

Therefore, if no one asks for it. No DNS will ever know what IP address the domain represents.

# Finding the IP for a new DNS Record

But lets try finding the IP of the record we had just created.

Ill run the same command as before, this time asking for the new domain name

```bash
dig testingdns.lennymelnik.com
```

And in the answer section we get

```bash
;; ANSWER SECTION:
testingdns.lennymelnik.net. 2252 IN	A	111.111.111.111
```

If you want to understand where this comes from look a bit above in the "Using DNS under the Hood Section"

So as you can see everything is here. And it was instant too. However, if the TTY has not yet timed out and you updated the IP. Then you will need to wait until it expires to be able to get the new IP.

However, there is an exception

# In order to get higher speed, some DNS service providers ignore TTY.

On one hand, this is good. Because it means that the DNS servers will remember the IP for longer and don't have to go snooping around to find it.

On the other hand it sucks because that means any updates will take forever.

Also its against common courtesy, since TTY is a standard that helps the internet function properly.

Just to sum it up

# I updated the IP in the DNS Record, why doesn't my service work?

- The TTL (Time to expire) of the old record has not yet occurred, so DNS servers are going off of memory
- The DNS service provider is ignoring TTL and not requesting the new IP