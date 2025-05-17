---
title : "A way to revive my PS/2 Model 90?"
layout : vintage
categories : vintage
---
<br/>


When I first got into vintage computers I started off with IBM's. Since my main source was LGR I would nonstop watch his videos on all the different IBM systems. The one that made me daydream was the model 90.

<br />

When I was able to go to VCF east, I purchased my first vintage computer. AND IT WAS A MODEL 90.

I could not have been more excited about my purchase, but the pain had just begun. Regardless of some people in the VCF IRC chat warning me not to get into the PS/2 line because they were "Difficult" I had no knowlege whatsover so I stupidly didn't inquire.

<br />

When I first booted it, I just got an error ADD THE ERROR HERE.

At first I thought the hard drive was dead. So I tried to use floppy drives to boot to at least something. But nothing worked even though the floppy was "reading". Then I suspected the floppy drive was dead and needed to be re-capped. But after I got an adapter to be able to attach any regular floppy drive, I put in a Gotek to no avail. Keep in mind almost nothing in this computer is compatable so even finding that one adapter was a pain.

<br />

I've already sunk quite a bit of time and money into this project, to no avail. I gave up for a while, the only option possibility I saw is doing something with the SCSI interface. Since my computer came with an MCA SCSI card. But the drives are hard to come by, and I have very little experience working with them (none). 

The options I came up with were.

1. LSA or PCI SCSI card to be able to write an OS into the drive with a different system then put it back into the PS/2
2. External SCSI floppy drive (too expensive)
3. SCSI to SD (too expensive and not availible)
4. External SCSI to IDE then IDE to CF. But that would have cost quite an amount and was not sure what else I would need.

<br />

More time passed. Then I was doing research and decided to look up SCSI to SD alternatives. Turns out there is an open source hat board that will use a Raspberry PI as an SCSI device. It should be compatable and will be a cheaper options. Plus I wont have to buy a drive.

I won't place an order right now, but I will soon.

I cannot wait and I really hope it works out!

https://github.com/akuker/RASCSI/wiki/Compatibility

