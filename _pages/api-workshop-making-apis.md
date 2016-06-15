---
id: 680
title: API Workshop
date: 2014-09-26T08:31:04+00:00
author: admin
layout: single
guid: http://www.princesspolymath.com/princess_polymath/?page_id=680
dsq_thread_id:
  - 3056446951
layout_key:
  - 
post_slider_check_key:
  - 0
tc-thumb-fld:
  - 'a:2:{s:9:"_thumb_id";s:3:"746";s:11:"_thumb_type";s:5:"thumb";}'
---
# [<img class="alignleft wp-image-720 size-full" src="http://www.princesspolymath.com/princess_polymath/wp-content/uploads/2014/09/playground1.jpg" class="grouped_elements" rel="tc-fancybox-group680" alt="playground" width="405" height="270" srcset="http://www.princesspolymath.com/princess_polymath/wp-content/uploads/2014/09/playground1.jpg 405w, http://www.princesspolymath.com/princess_polymath/wp-content/uploads/2014/09/playground1-300x200.jpg 300w" sizes="(max-width: 405px) 100vw, 405px" />](https://www.flickr.com/photos/europedistrict/6034445855)
  
Making APIs

In this walk through we&#8217;re going to make some APIs and test them in various ways.  After doing this you&#8217;ll be able to create API mockups and blueprints, test them, and create actual APIs from those and deploy them to a cloud server.  Fun times!

## Step 1: Create a Mockup API

Head over to [apiary.io](http://apiary.io) to get started.  Click the  &#8220;See How Apiary Works&#8221; icon near the top of the page.  Don&#8217;t get distracted by the cool spinning icon, just click it to get to the next section.

Scroll down to the bottom to either sign in with GitHub (super easy) or create an account with email.

If you&#8217;ve never used Apiary before, it&#8217;ll ask you to name your first API.  Go ahead and name it something like &#8220;myemailusername&#8221; or whatever works &#8211; the namespace is shared across all of apiary so we can&#8217;t all use the same one.  I&#8217;ll go with &#8220;synedra&#8221;.

There&#8217;s a message from Jakub there, welcoming you and asking for feedback.  You can give some (like to say you shouldn&#8217;t have to see the message) or just click &#8220;Close&#8221; to move on.

Now we&#8217;re in the meat of the thing.  From here you can edit your blueprint and change the behavior of your mocked up API.  The base API is designed to be a notes saving API, but we&#8217;re just going to use GET for this example so we can get through the whole thing sometime today.

Change the messages under the GET /notes resource to something more meaningful to you.  &#8220;Learn Kung Fu&#8221; or &#8220;Knit 27 sweaters&#8221; or &#8220;Pick up the Dry Cleaning&#8221;

## Step 2: Play with your fake API

Now that you&#8217;ve created your fake API, let&#8217;s play with it.  First, click the Documentation link to get to the interactive documentation page.  Check out the &#8220;GET /notes&#8221; by clicking on the GET.  Look, there&#8217;s your messages!  So exciting!  You can also test the POST, which will show you what the request and response would be for a POST.  Although it doesn&#8217;t really change anything &#8211; this is only interactive documentation and doesn&#8217;t have a real backend server.  Still, pretty fun!

Look over on the right, under Mock Server.  Copy and paste that string into your browser (probably want to use a new window for this) and&#8230; oh, crud, we didn&#8217;t make a / resource.  That&#8217;s ok, add /notes to the URL and see what happens.  There it is!  Your fake API, out there for all the world to see!  If you want to POST to the URL you&#8217;re kind of out of luck at this point unless you want to hack up some quick code. But let&#8217;s see if there&#8217;s a better way.

## Step 3: Test your API using Runscope

[Runscope](http://www.runscope.com) provides a set of tools for testing, monitoring and debugging your API.  Click on the &#8220;Try Runscope &#8211; Free&#8221; link (and as it points out, no credit card is required).  Once you&#8217;ve done that, you&#8217;ll want to pick &#8220;API Debugging&#8221; and follow the path through to get an idea what we&#8217;ll be doing.  Pick an existing product to check on (I like Github because, well, I like Github!).  Check out the response.  How helpful is that?  You can see the request as well, which is hugely useful when trying to debug why something isn&#8217;t working in your own personal application.  The next three pages you can skip through with &#8220;Next&#8221; and head straight to your Dashboard.

Here, Runscope has provided you with a default bucket for your Github call, which is pretty nice.  The Github API is most likely doing well, like it does, so you&#8217;ve got a 200 Ok represented, and the time the request took and a few other handy things.  But we&#8217;re not here to test Github, they&#8217;ve got people for that.  Let&#8217;s test out your mocked up API and see how that works.

Click the fancy blue &#8220;New Request&#8221; button to create a new request.  Put the base URL for your API there, and click &#8220;Launch Request&#8221;.  Oops, again, here&#8217;s our 404.  We didn&#8217;t create a base resource, so we get a 404.  Never fear, we&#8217;ll fix this right up. Add /notes onto the end of the request and see how that works out.  Hey, there they are, those messages.  We can click to see the request and the response, and find out what a successful request will look like.

At the top of the page, click &#8220;Traffic Inspector&#8221; and you&#8217;ll end up on a dashboard with all the calls in the bucket you&#8217;re in.  Now you can see the 404 we generated as well as the 200 when you asked for the notes.  Let&#8217;s try one more &#8211; the Apiary blueprint allows for POST actions as well, as we saw.  How will that work in Runscope?  Awesome, it works fine (although it didn&#8217;t do anything to the back end).

To finish up this section, head back to your Apiary page, and click Traffic Inspector.  Here we can see a list of the calls which have been made against your mocked API.  Again, failures are represented by red dots, and success by green dots.  Compare the inspectors between Apiary and Runscope.  They&#8217;re both perfectly reasonable tools &#8211; just use what works for you.

## Step 4: Setup App for Google Cloud

So now we&#8217;ve mocked up an API, but it doesn&#8217;t really do anything, and it&#8217;s not running on an actual server.

We&#8217;ll put something similar together on a real server next.
  
There are lots of cloud platform providers, but Google Cloud is the one I&#8217;m going to be working with today.  The first thing you&#8217;re going to need to do is get your account squared away and download the SDK for your system.  Head over to their [Getting Started](https://console.developers.google.com/start/appengine)  page to get started.  Name your project and scroll down a bit.  I use python so that&#8217;s what I selected, and my examples in class are going to leverage flask.  So unless you have a python allergy, that will be your easiest path (and the code is basically written for you).

Grab [the appropriate SDK](curl%20https://sdk.cloud.google.com/ | bash) for your system and follow the instructions on how to get it up and running.  Source your .bash_profile (or whatever profile resource file you used) and you&#8217;re ready to hit the ground running.  Pick Python/Flask then get your system authenticated:

`gcloud auth login`

The process here is pretty heavily modeled after the Sendgrid Tutorial with the same goals, so if you want a more complex setup you can check on [that](https://github.com/thinkingserious/api-design-with-apiaryio-python-and-flask).  But for now, we&#8217;re going with a simpler project just to see how these things work together.

First, edit the sample to have some different content. On the Apiary documentation page, there&#8217;s a block under the /notes endpoint that looks like this:

<pre>200 (OK)
Content-Type: application/json
[{
  "id": 1, "title": "Jogging in park"
}, {
  "id": 2, "title": "Pick-up posters from post-office"
}]
</pre>

So, to make this work, we&#8217;re going to have to actually edit the code. So far as I know, there&#8217;s no magic wand to make the blueprint spit out python code, but it&#8217;s really pretty easy. To do this, we&#8217;ll need to edit the appengine-try-python-flask/main.py file.

We want our new &#8220;real&#8221; API to return this stuff when &#8216;/notes&#8217; is hit. It&#8217;s cool to leave the &#8220;Hello World&#8221; for the base &#8216;/&#8217; resource, it&#8217;s friendlier than a 404. But we do need to change the flask code before grabbing it.

Make sure your system has [pip](http://pip.readthedocs.org/en/latest/installing.html) and flask installed:

pip install flask

First, update the import to get json functionality (that&#8217;s a comma there, not a period):
  
from flask import Flask,json

Add some new code directly after this section in the code:

<pre>@app.route('/')
def hello():
    """Return a friendly HTTP greeting."""
    return 'Hello World!'

@app.route('/notes', methods = ['GET'])
def get_notes():
	return json.dumps([{
          "id": 1, "title": "Presenting at FOWA"
        }, {
          "id": 2, "title": "Playing with Drone"
        }])
</pre>

Now run it again on your local system and admire the results that match the GET /notes on the mocked API. Do the Runscope and Traffic Inspector thing if you want, but we&#8217;re now ready to get this puppy out into the world.

So, grab the &#8220;Download this file&#8221; and it&#8217;ll plop into your Downloads directory, mostly likely.  You can move it somewhere else or just leave it there, it doesn&#8217;t make no never mind.

From the directory **above** that directory, type:

`dev_appserver.py appengine-try-python-flask`

Wait a few seconds until it says your system is up (hurray!) and you can visit your
  
API at the localhost:8080. That&#8217;s great for you, but not so great for other people who want to visit your site. In the meantime, let&#8217;s check that local server and see if it behaves as we expect (&#8216;hello world&#8217; on a &#8216;/&#8217;, gives you your notes on a &#8216;/notes&#8217; call. Great!

At this point you could deploy the system directly to the cloud and solve the problem where it&#8217;s kind of fragile, not available via the external world, and generally only good for quirky dev things. So let&#8217;s leverage Runscope again to create a passageway in the internet back to your home server. Download the appropriate [Passageway tool](https://www.runscope.com/docs/passageway) for your platform and start it up. Answer a few questions (remember we&#8217;re using port :8080) and then it&#8217;ll give you a gateway to be used to access your local system out in the wild.  Create a new endpoint or two in Runscape and watch what happens as you and others visit the page.

## Step 4: Deploy your app to the cloud

Back to the [Google Cloud](https://console.developers.google.com/start/appengine) page you go to get yourself finished.  Click on the &#8220;Create your Project&#8221; button and it will create the backend server for your cloud instance (and give you a snazzy server name with random words).  Wait a minute or so while it spins up, then deploy your code (again, from the directory above the directory with your code):

<pre class="ng-binding" style="color: #313131;">appcfg.py -A &lt;your assigned server name&gt; update appengine-try-python-flask</pre>

Note that there&#8217;s a minor typo in the Google Docs there, you&#8217;ll need to use &#8220;-flask&#8221; in order to deploy the right thing.

That&#8217;s it for this section of the workshop. Exercises left to the user are to get POST and DELETE working (for examples of this, see the send grid example above). Add some fancier python to do calculations or lookups, and increase the complexity of what you&#8217;re working with.

&nbsp;