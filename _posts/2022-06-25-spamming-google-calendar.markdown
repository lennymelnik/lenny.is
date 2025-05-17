---
title : "Spamming Google Calendar"
layout : post
categories : unsecured
---
# Spamming Google Calendar

A simple tool to spam someones Google Calendar

# Inspiration

I got tired of automatically being added to events that I didn't care about. So I decided to see if I could use a random email and invite someone to an event. For said event to show up on their calendar without confirming or ever being contacted from the anonymous email before.

When I realized this worked I had the idea to automate it. Inviting a specific email to an event ever minute absolutely filling up their schedule.

# Implementation

I did some research, and it should be pretty simple to do utilizing the Google Calendar API.

Ill be using Node.js 

# Ideas

To be able to input anybody's email and have it work without being blocked

Turn it into a web service, where people can input an email or a set of emails to target.

# The story

Communicating with the API

I just got the Get Started code from Google themselves. Setup the google developer account and downloaded my credentials.

![Untitled](/assets/spamming-cal/Untitled.png)

Boom, it worked and I was able to see all my calendar events. Next we need to try to create one.

I copied and pasted and edited the following function. Basically it creates an event, with all of its metadata. Then will add it.

<pre><code class="language-js">

function createEvent(auth) {
    const calendar = google.calendar({version: 'v3', auth});
    var event = {
        'summary': 'Testing Calendar Spam',
        'location': '800 Howard St., San Francisco, CA 94103',
        'description': 'We are just testing the calendar spam product',
        'start': {
          'dateTime': '2021-12-06T09:00:00-07:00',
          'timeZone': 'America/Los_Angeles',
        },
        'end': {
          'dateTime': '2021-12-06T12:00:00-07:00',
          'timeZone': 'America/Los_Angeles',
        },
        'recurrence': [
          'RRULE:FREQ=DAILY;COUNT=2'
        ],
        'attendees': [
          {'email': 'leonardmelnik@gmail.com'},
        
        ],
        'reminders': {
          'useDefault': false,
          'overrides': [
            {'method': 'email', 'minutes': 24 * 60},
            {'method': 'popup', 'minutes': 10},
          ],
        },
      };
      
      calendar.events.insert({
        auth: auth,
        calendarId: 'primary',
        resource: event,
      }, function(err, event) {
        if (err) {
          console.log('There was an error contacting the Calendar service: ' + err);
          return;
        }
        console.log('Event created: %s', event.htmlLink);
      });
      
  }
</code ></pre>

As you can see. If it succeeds it will say output

<pre><code class="language-js">Event Created: EVENT LINK HERE
</code ></pre>

Instead what I see is

![Untitled](/assets/spamming-cal/Untitled%201.png)

But lets check the calendar

![Untitled](/assets/spamming-cal/Untitled%202.png)

And there it is! The event has been created and shows up on an unrelated email.

Lets play around with the settings a bit.

### Making an event reoccur

If we change the count here. (This is in the event object)

Since the event frequency is "DAILY", increasing count makes it happen for more days.

<pre><code class="language-js">'recurrence': [
          'RRULE:FREQ=DAILY;COUNT=4'
        ],
</code ></pre>

When this is run we get this

![Untitled](/assets/spamming-cal/Untitled%203.png)

Although this may seems like a convenience, where we can just make one event per time and just set the COUNT to like 100. But there is an issue. Because it is a reoccurring event, it can be deleted with one click. Since if an event is reoccurring, when you delete one, Google Calendar gives you this option

![Untitled](/assets/spamming-cal/Untitled%204.png)

### Looping and creating multiple events

It should be as simple as a for loop.

First we need to establish our date range

<pre><code class="language-js">var start = new Date("12/06/2021")
var end = new Date("12/12/2021")
</code ></pre>

Then we need to establish the date that we are currently on

<pre><code class="language-js">var current = new Date(start)
</code ></pre>

Finally we loop through and add to current until we get to end

<pre><code class="language-js">while(current <= end){
	var addedDate = current.setHours(current.getHours() + 1);
	current = new Date(addedDate);
}
</code ></pre>

Lets work backwards in. First we get the current hour of current and add 1 to it. Then we set it with .setHours() and finally assign the added value to addedDate.

Finally we create a new date object using addedDate and assign it back to current.

If I add a 

<pre><code class="language-js">
console.log(current)
</code ></pre>

to the loop. We will be given the following

![Untitled](/assets/spamming-cal/Untitled%205.png)

It works! As you can see we are moving one hour at a time!

Lets plug this into the createEvent function

![Untitled](/assets/spamming-cal/Untitled%206.png)

Oops. Looks like runs too fast and Google just stops it.

I initialized a timer function

<pre><code class="language-js">const timer = ms => new Promise(res => setTimeout(res, ms))
</code ></pre>

and then made it wait after each loop

<pre><code class="language-js">await timer(1000);
</code ></pre>

![Untitled](/assets/spamming-cal/Untitled%207.png)

![Untitled](/assets/spamming-cal/Untitled%208.png)

Success!!!! Seems like a second is enough for each event. Without google rate limiting me.

Now I had a bit of a heart attack, because I remembered that API costs exist. But after some research I can say with 99 percent confidence that it does not cost anything (as long as I don't upgrade limits)

![Untitled](/assets/spamming-cal/Untitled%209.png)