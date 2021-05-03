---
title: "\"Hacking\" Amazon Dash Buttons in the UK"
date: 2015-10-18T13:29:00Z
draft: false
---

Love them or loath them, [Amazon Dash buttons](https://www.amazon.com/oc/dash-button) are pretty cool little devices. What most people consider to be nothing more than a simple way to stock up on [Gatorade](http://goo.gl/C5uXAF) and [nappies](http://goo.gl/U8anI3) are actually [one of the cheapest 802.11b/g/n devices on the market](http://www.amateurradio.com/inside-the-802-11bgn-amazon-dash-button/) - which makes them an extremely interesting proposal for home automation. 

By now, videos and blog posts of people abusing the low-low price of $5/button for their own ends are all over the internet. From [tracking baby metrics](https://medium.com/@edwardbenson/how-i-hacked-amazon-s-5-wifi-button-to-track-baby-data-794214b0bdd8), to [controlling Tesla's](https://www.youtube.com/watch?v=e1hmjyNwrCQ) - once again, the internet doesn't disappoint. 

<iframe width="560" height="315" src="https://www.youtube.com/embed/e1hmjyNwrCQ" frameborder="0" allowfullscreen></iframe>

There is, however, one small obstacle to those of us in Europe and abroad wishing to get our hands on our very own Dash button to play around with. The buttons are only available to American Amazon Prime subscribers, and the retailer has so far announced no plans to change that. Yuck. That said, these things are just standard WiFi devices right? Shouldn't it be relatively simple to get them set up abroad? Fortunately, that turns out to be (more or less) the case.

The first hurdle was getting my hands on a physical device. As mentioned before, they are currently only available to US-based Amazon Prime customers. Fortunately, a number of US-based mail relay companies exist to solve exactly this problem (with [ShipItTo](https://www.shipito.com/) being my personal favourite) and Amazon, as a generous internet company, are all too happy to offer free trials of Amazon Prime (sorry Amazon).

![](/blog/img/amazonPrime-1.png)

Amazon Dash buttons are currently available at $4.99 a pop. The cost of three buttons, plus Economy airmail delivery to the UK ended up being ~$20. Not quite the $1-and-free-shipping you'd have found in the US a few months ago - but still pretty affordable.

![](http://charts.camelcamelcamel.com/us/B00WJ12MQ8/amazon.png?force=1&zero=0&w=725&h=440&desired=false&legend=1&ilt=1&tp=all&fo=0&lang=en)

Once the buttons arrived, the next challenge presented itself. Dash buttons have a very slick set-up process, either using WiFi to connect to the Amazon Android app, or 'ultrasound' to pair up with the Amazon app on iPhone (probably due to Apples restrictive policy on apps accessing WiFi settings programmatically). However, both these methods require you connect the buttons to an *American* Amazon account. Fortunately, we had to set one of these up earlier to order the buttons in the first place, and (at least the Android) Amazon App allows for easy region switching right in the app.

<div class="container">
    <div style="float:left;width:49%">
        <img src="/blog/img/2015-10-18-13-59-48.png">
    </div>
    <div style="float:right;width:49%">
        <img src="/blog/img/2015-10-18-14-07-11.png">
    </div>
</div>

To kick off the setup process (using Android App v6.0.0.100), simply select 'Your Account' from the hamburger menu on the left-hand side of the app, scrolls down to the 'Dash Devices' section and hit 'Set up new device'

<div class="container">
    <div style="float:left;width:49%">
        <img src="/blog/img/2015-10-18-14-00-23.png">
    </div>
    <div style="float:right;width:49%">
        <img src="/blog/img/2015-10-18-14-10-46.png">
    </div>
</div>

Following the wizard is pretty self-explanatory - put the device into setup mode by long-pressing the single top button (wait for the blue flashing light), and wait for your phone to discover and connect to the WiFi (incidently, the basic web page for WiFi setup can be viewed by browsing to http://192.168.0.1/ whilst connected to the 'Amazon ConfigureMe' hotspot the device broadcasts whilst in setup mode). Select your WiFi hotspot, and provide your connection details - and you should be rewarded with...

An App Crash.

Turns out (at least in my case), that trying to configure a Dash button on an internet connection which identifies as being outside of the United States, results in the Amazon App crashing out. Bummer. The simple way around this, however, is to simply connect to a US-based VPN during setup. I used the excellent [OpenVPN](https://openvpn.net/), running on a US-based Azure VM. With that out of the way, you should be able to complete the rest of the wizard. 


<div class="container">
    <div style="float:left;width:49%">
        <img src="/blog/img/2015-10-18-14-16-18.png">
    </div>
    <div style="float:right;width:49%">
        <img src="/blog/img/2015-10-18-14-22-03.png">
    </div>
</div>

Be sure to cancel the setup once you've established a WiFi connection, and before you're asked to choose an actual product to order one each button press. As fun as it would be to get charged international shipping for an industrial-sized order of nappies every time you try to [order Dominos](http://www.theverge.com/2015/9/28/9407669/amazon-dash-button-hack-pizza) - it's not necessary to be able to pick up the fact that a button was pressed somewhere on your network, which is what we'll cover in the next blog post.