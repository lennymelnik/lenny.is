---
title : "A weird addition to authentication - keyboard biometrics?"
layout : post
categories : projects idea
---

## Just a preface

This is just my ramblings and ideas, I don't even have a hypothesis yet. 


## Why do we need a different kind of authentication

Passwords have been failing us for a while, or more likely we have failed them. They should not be reused, yet they are. Making them significantly weaker and tracable. Not just that but the amount of metadata that can be extracted from them (once breached) is insane.

Can we make a new password for each service thats not just THEPASSWORD_THESERVICE? Well, I don't think we as humans can memorize that, the age of needing to memorize phone numbers is over (I don't know if I ever lived in that age even), so memorizing passwords for hundreds of accounts is not an option. Saving the passwords in your browser lets anyone who has access to your computer have access to everything, and saving in a password store is better but still offers a centralized way to get everything.

Now, the weak parts of passwords are and have been addressed by MFA. Not only do you need the password, but also a device (If they have your device they might as well have everything already). MFA is an amazing solution and without a doubt needs to be in use everywhere, yes its a bit annoying. But it also makes you and everyone around you safer.

## My Idea

I was sitting on the train just thinking of fun projects, and I thought of the idea of doing some "Authentication" using biometrics/behavior. The first method that came to my head was typing, mostly becuase I type a lot differently than my parents and S.O.

But what do we measure? What is unique? How can this be used?

### How can this be used

I was thinking this could be used in CONJUNCTION with other password/authentication methods, and instead of just approving someone based on typing pattern, it would rather be used for anomoly detection and alerting, better safe than sorry right?

## What do we measure?

At first I wanted to measure how fast a person click a key, (time difference between keyup and down). But thats hard to measure, plus is limited to a small count (If a key is pressed long enough it will repeatttt (intended)). 

Then I decided to switch focus and measure the difference in time between keyup for key/letter pairs. So seeing how fast a person can go from each key to each other key. I have implemeneted a pretty simple method to measure this for now, but I will be working on it over time. 



# Whats next?

Well, a lot of testing. Primaraly building out a little single page site with javascript that measures key-pair speeds, and then compared them to a last attempt to try to determine if it is the same person.

I was thinking was finding the difference between historical/live key-pair speeds and then running a standard devation. Or doing a std before on the non-subtracted values.

This project will get pretty complicated, and may go no where. But I think it is interesting and gives me the opportunity to really scratch my brain and hopefully come up with a cool demo.