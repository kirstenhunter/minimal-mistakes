---
id: 845
title: Hacking a Philips Hue Remote API in Node
date: 2016-05-03T13:07:28+00:00
author: admin

guid: http://www.princesspolymath.com/princess_polymath/?p=845
tc-thumb-fld:
  - 'a:2:{s:9:"_thumb_id";s:3:"847";s:11:"_thumb_type";s:5:"thumb";}'
post_slider_check_key:
  - 0
dsq_thread_id:
  - 4797540560
categories:
  - API Codex
  - Geek Stuff
  - Irresistible APIs
  - Web APIs
---
I&#8217;m giving one of my favorite talks at [Stir Trek](http://stirtrek.com) this year &#8211; [Quantifying your Fitness](https://skillsmatter.com/skillscasts/6767-wrangling-the-internet-of-things-using-node-js).  Unfortunately, the IFTTT->Philips Hue connector has ceased to work and neither IFTTT nor Philips Hue has deigned to answer my plea for help.  So, while Quantifying your Fitness used to use Twitter as glue, I needed to create a remote API client that would run on [Modulus](http://modulus.io) in Node.js.

There are lots of people who have created clients in various languages, including Paul Shi, who wrote a [fabulous blog post](http://blog.paulshi.me/technical/2013/11/27/Philips-Hue-Remote-API-Explained.html), but I wanted to do this directly in Node, so that other people looking for guidance would understand exactly what they needed to create and send.

So here&#8217;s the tutorial for what I did:

### Get a Token

In order to interact with the unsupported/hidden remote API, you have to pretend to be a known partner.  I chose to masquerade as an iPhone for this particular exercise.

  1. Login to [meethue.com](http://meethue.com)
  2. Send a request to  <https://www.meethue.com/api/nupnp>. (or in [My bridge](https://www.meethue.com/en-US/user/preferencessmartbridge) page on the meethue website and by clicking on “Show me more”)
  3. Get your access token by sending a request to http://www.meethue.com/en-US/api/gettoken?devicename=iPhone+5&appid=hueapp&deviceid=\*\*BRIDGEID\*\* and then right click on &#8220;Back to the app&#8221; to find the token inside of the response (phhueapp://sdk/login/\*\*ACCESSTOKEN\*\*)
  4. I promise this is the grossest part of the process, but you do need to do this manually to get the API to respond correctly.

From here, you can do a tl;dr if you want and just checkout my [code on github](https://github.com/synedra/fitfood-demo-pluralsight).  Otherwise, let&#8217;s sally forth.

### Make a Call

  1. Now we have an access token and a bridge ID, so we can make a very easy call.  I&#8217;m using [httpie](http://httpie.org) for examples here, I strongly recommend it for any interaction with a REST API on the command line.
  2. First, let&#8217;s get the status for the bridge.  Make the following call:
  
    http &#8211;form POST https://www.meethue.com/api/getbridge token==\*\*ACCESSTOKEN\*\*
  3. If all has gone well, you will get information about your lights and the system.

### Make a Harder Call

  1. Now let&#8217;s turn all the lights off.
  2. The format for this call is pretty convoluted, but you can figure out what the actions/status items are by reading the [Philips Hue local API documentation](http://www.developers.meethue.com/philips-hue-api).
  3. Here&#8217;s a sample.  Copy it very carefully 🙂 
    <pre>http --form POST https://www.meethue.com/api/sendmessage token==**ACCESSTOKEN** clipmessage='{"bridgeId":**BRIDGEID*, "clipCommand": { "url": "/api/0/groups/0/action", "method": "PUT" , "body": {"on":false} }}'</pre>

  4. From here, you should be able to make calls against the API.  Again, the code on github is in node, and it&#8217;s part of my Quantified Fitness talk, but the juicy bits are all there for you to peruse and copy at will.
