---
title: Bluetooth LE Tracking Progress. I don't trust the numbers
layout: post
---



# Weird Numbers

Before we get started, this is how the Arduino looks from outside my building, not suspicious at all.
![[Pasted image 20241211194735.png]]

After about 2 weeks of my server not shutting down I was finally feeling confident to graph some of the data I received.

However it did not turn out the way I expected.

When I mapped the average distinct devices per hour.

<pre><code class="language-sql">

SELECT to_char(to_timestamp(("timestamp" / 1000)::double precision), 'Day'::text) AS day_of_week,
    avg(count(DISTINCT mac)) OVER (PARTITION BY (EXTRACT(dow FROM to_timestamp(("timestamp" / 1000)::double precision)))) AS avg_distinct_mac_count,
    EXTRACT(dow FROM to_timestamp(("timestamp" / 1000)::double precision))::integer AS sort_order
   FROM bluetooth_data
  WHERE to_timestamp(("timestamp" / 1000)::double precision) > '2024-11-24 00:00:01.121829+00'::timestamp with time zone
  GROUP BY (to_char(to_timestamp(("timestamp" / 1000)::double precision), 'Day'::text)), (EXTRACT(dow FROM to_timestamp(("timestamp" / 1000)::double precision)))
  ORDER BY (EXTRACT(dow FROM to_timestamp(("timestamp" / 1000)::double precision))::integer);

 </code></pre>
I saw this:
![[distinct_device_per_hour.png]]

While a decrease in traffic after 1am makes sense. What did not make sense was the lack of difference between 8am and 9am.

My expectation was since everyone is heading to work at 7-9. There should be a growth in distinct devices.

This discrepancy may be due to a difference in behavior for BLE devices. 

Which would be cars, IOT Devices, Cameras, and other such things.

# Breaking it down further


Lets break it down a bit more. What if we averaged the traffic by distinct mac addresses per day of the week?
![[Pasted image 20241211195059.png]]

This is not as hard to explain logically, but the sudden spike from Saturday to Sunday is a bit strange.

I have to check the data a bit more as maybe the time on my server is improperly configured?

Honestly there is not enough here for me to see any real patterns/make some conclusions. Lets dig even deeper.


# Moooreee
What if we saw the distribution of traffic across hours. But grouped by day of the week?


# MAC (MAC Address Magic)

Since we have so many unique mac addresses. Lets try to make that data usefull. Apparently MAC addresses are like IP's and the IEEE assigns them.

Lets see if I can join the data they have into our database and get some numbers on hardware manufacures

http://standards.ieee.org/develop/regauth/oui/oui.txt

On first look, it does look parsable. But lets see if we can find a CSV format:
![[Pasted image 20241211201032.png]]


# some time later
While trying to see more into the brands, this graph came up (when I match company name with distinct mac addresses):
![[Pasted image 20241211210438.png]]

Now the weirdest part about this. Is out of 300k + Unique MAC addresses. Only 1.6k of them match to an organization via prefix with these lists I found
