---
title : "Old Habits Die Hard"
layout : post
categories : thoughts technology
---
When we are learning a trade, we usually learn a method of doing things. That method becomes our default, so much so that we disregard alternatives that might be better, because currently we are so efficient in the original method it would "waste" time with what is perceived to be "minimal benefits".

However one of the best qualities we can have is an open mind that evolves with the times. Not just with things that are easy, but going out of our way to improve on what is hard.

I recently had such an experience with authenticating systems. For 4ish years I have built all my software/sites with my own authentication system. Something that I just copy and paste, is secure, and just works. But for a while I have been wanted to use auth0, but I didn't know where to start. I would check out the documentation and just think "How can this fit into my current workflow, I'll probably have to change out a lot more of my code around the authentication system to make this work". But eventually I decided to just jump the gun and give it a try for a new project. 

At first things were starting to make sense, but then I hit a point where I would have to authenticate the frontend with my API and I was lost. Yes I can verify a token is valid, but how do I associate it with a user in my database? Sure I can use the /user API route to get all the info I need, but to do that every time I need to see who a token belongs too would take forever. It took a while of research, but eventually after finding the latest documentation I was able to discover the answer right in-front of my eyes. The JWT included a base64 included set of values, of which includes the userId that Auth0 used. Now what I can do, is just search for this userId (which is already authenticated and verified) and find the associated user in my database, if no user exists, then I can fetch the information from the /userinfo route and add it to my database. Boom, now it works seamlessly with all my other routes and actually simplified all my code because I got to get rid of my authentication logic and have so many more built in features like:
1. Social login
2. Password Reset
3. Email Verification
4. and more!

I'm looking forward to learning new things and challenging and mixing up the way I do things. Maybe I'll even give HTMX a go for a small project or admin dashboard!