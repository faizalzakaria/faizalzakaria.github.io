---
layout:     post
title:      "Intercept API requests with mitmproxy"
date:       2015-06-25 21:34pm
author:     "Faizal F Zakaria"
header-img: "img/post-bg-01.jpg"
excerpt:    "<h4>Wondering how you could crack your friend's API?</h4>
Mitmproxy could be very handy for that kind of job."
---

<h4>Quick introduction, what is Mitmproxy ?</h4>

Mitmproxy is a tool for you to intercept a request. Its a competitor
of Charles. Charles has UI while mitmproxy can be run through your
terminal. If you prefer terminal and simplicity, then I would suggest
to use mitmproxy.

It works on all devices, laptop, ios, android what so ever.

<h4>Prerequisites ?</h4>
<p></p>
* You need python
* You need pip
* Then just install mitmproxy as such:

{% highlight ruby %}
pip install mitmproxy
{% endhighlight %}

* And try run it, see if it works
{% highlight ruby %}
# Go to your terminal, then run this
mitmproxy
{% endhighlight %}
<p></p>

<h4>How to use it ? </h4>
<p></p>
* Make sure you are on the same network as your target device.
* Check your current ip as such:

{% highlight ruby %}
ifconfig
{% endhighlight %}

* Run mitmproxy
* Go to the target device, and add the proxy as such:

{% highlight ruby %}
IP = <Your host IP>
PORT = 8080 (default Port for mitmproxy)
{% endhighlight %}

* Now on the target device, try go to http://google.com, see if it
  works.
* You wont be able to browse https server, as you need the ssl
  cert. All you have to do is to just run this in your browser:
{% highlight ruby %}
# In your browser, go here
mitm.it
# Then choose your device OS (Android, IOS, etc)
{% endhighlight %}

* This will install the cert and now you should be able to access https
  server.
<p></p>
<h4>Lets crack a random App</h4>

(p/s: This is just tutorial purposes)

I'm going to use Android as my target device. Enable the proxy in your
target device, run mitmproxy and configure ssl cert.

Then run a random app, I'm going to run mudah.my App.

And here how it looks like the requests from the App.

![Example requests](/img/ExampleMitmproxy.png)

Then you can click any request, and you can see the detail of the
request/response.

Example of request:
![Example Request](/img/ExampleRequest.png)

Example of response:
![Example Response](/img/ExampleResponse.png)

You can see here, how to get listing from mudah.my through their API.

{% highlight ruby %}
GET
https://api.mudah.my/api/v2/list.json?app_id=mudah_android&hash=41b114fe6fa2161c86bcb57cc67c803b0ad6ec65&limit=10&o=20&
{% endhighlight %}

Although the API above is public, Mudah.my has some sort of security
implemented here, with that *hash* field. Interesting.

Enjoy!
