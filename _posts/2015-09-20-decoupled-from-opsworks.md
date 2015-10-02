---
layout:     post
title:      "Why I moved out from Opsworks to Capistrano"
date:       Sun Sep 20 11:07:33 ICT 2015
author:     "Faizal F Zakaria"
header-img: "img/post-bg-01.jpg"
excerpt:    "Opsworks is a great tool to setup & deploy your
App to production server as soon as possible but its not easy to extend its functionalities
to support SOA (Service Oriented Architecture)."
---

<h4>What Opsworks for?</h4>

Most of the startup started with only 1 engineer, and they started to hire
more engineers when they see traction and/or the investor(s) started
to throw money on them.

In the early stage, with only one engineer on board, its hard to move
fast without setting up a proper tools to push the code out to
production. So this is where Opsworks comes in very handy.

Opsworks help startup to easily setup/provision a server, and deploy
the code through a simple button clicking. To scale the App
horizontally, all you have to do is just add a new server, and click a
start button. Awesome, that sounds easy.

<h4>How Opsworks work?</h4>

Opsworks uses Chef framework to provision and deploy to the server. The cookbooks can
be found [here](https://github.com/aws/opsworks-cookbooks){:target="_blank"}.

It seperated to 5 lifecycle events of which all of them are self explanatory.

- Setup
- Configure
- Deploy
- Undeploy
- Shutdown

Good thing is, you don't have to know how Chef works to start using
this. All you have to know is that 5 lifecyles, especially the `deploy`
lifecyle event. As the name stated, this is where and how you deploy
your code to the server, just trigger this event in the Opsworks dashboard, and it
will do all the magic for you.

<h4>The motivation behind my decision to decouple our infra setup from Opsworks?</h4>

Duriana API & services are built on top of Ruby based framework, e.g:
Sinatra. You can find out our stack
[here](https://github.com/duriana/the-team){:target=_blank}. We used
Opsworks for the deployment. It was very helpful and easy to setup and
we managed to scale easily our API when we need to. Due to the fact
that we don't have that much of budget, so some non critical
services are hosted in Heroku.

In the early stage, in Opsworks, we have only 1 API app, 1 frontend
app. Then the app grows and we decided to decouple a few features to
its own service. E.g: Callback service, workers etc. So we need to add
these services to Opsworks. Thats where Opsworks started to fail to support our need.

In order to cater our need, I've to modify/extend Opsworks cookbooks,
especially the `deploy` cookbook.

This reason alone is not enough for me to finally decided to move out
from Opsworks as I really like the fact that we can easily scale our
App with just a click of a button. Plus we can roll up a few servers
only during the peak hours. So I extended Opsworks, with my
own/custom cookbooks, up to now I've around 16 custom cookbooks for Opsworks.

There are also a few other reasons:

- If we ever decided to move out from EC2, then its hard to do so due
  to the fact that we coupled too much with Opsworks.
- Opsworks was down, and due to auto heal, Opsworks left our servers
  hanging without an ELB, and led to a downtime for 1 - 2 hours for a
  recovery process.
- We have free credits from Softlayer, $10k / month for a
  year. Thats a lot, and we have plan to try this out.

<p></p>
<h4>How it looks like to extend/improve Opsworks to support Duriana's
need?</h4>

So this is how it looks like to extend the cookbook,

- Git Clone the `opsworks-cookbooks`.
- Read the code, and understand how it works.
- Add custom cookbooks in the Opsworks UI.
- Write your own custom cookbooks or overwrite the cookbook from
  opsworks-cookbooks.
- modify / copy  etc.
- Push the code to your repository.
- In the Opsworks UI, add your recipe, in one of these lifecyles, e.g:
  `deploy`.
- In the Opsworks UI, run the `update the custom cookbooks`.
- Then click the `deploy`, and it should already uses your custom
  cookbook on top of the `opsworks-cookbooks`.

But of course, first time you try it, it might not turn out as what
you have expected. So you might need to do this back and forth until
you get it right.

So this is where I started to feel, its too overkill to deploy using
Chef. Chef process is long, a lot of unecessary steps, to test your
custom cookbooks is not very efficient and you become unproductive due
to those waiting time.

So I moved this testing process to Vagrant, you can use
[vagrant-opsworks](https://github.com/wwestenbrink/vagrant-opsworks){:target:"_blank"},
to simulate `Opsworks lifecycle events`. I won't elaborate this in here. This
increase the dev efficiency but still to deploy with Chef is
overkill. With `m3.large` instance, to deploy our code took around `3 - 8
minutes`. If we need to be agile, and deploy 10 - 50 times per day,
then 3 - 8 minutes is too long for us.

(p/s: If you would like to learn more on how to simulate Opsworks in
Vagrant, you can check out [here](http://faizalzakaria.github.io/todo).)

<h4>How I use Capistrano to support/deploy Duriana's services easily?</h4>

There are few other tools that can replace Opsworks, but I've been
using Capistrano for a while and its easy to extend knowing that we
have engineers that know well Ruby.

We don't use Capistrano to just deploy one App, but we use Capistrano to
deploy all our apps, from backend, workers to frontend, with different
environments, instances and branches.

This is how it looks like architecturely:

![Autotomy](/img/posts/autotomy_capistrano.png)

I know Capistrano 3.0 is out there, but it seems still new and lacking
of support from the common libraries that I want to use.

<p></p>
<h4>What we improved so far on our deployment pipeline?</h4>

<p></p>
- From `3 - 8 minutes` deployment to `less than a minute` deployment. We
cached the code, so it improves the deployment time.
- To extend our deployment process is piece of cake. All written in
  Ruby, testing is straight forward and fast.
- More verbose to the developpers.
- More reliable, to restart the unicorns, resques workers etc take
  only a few seconds.

Of course nothing is perfect, eventually when we have 30 - 40 servers
to deploy to, then we might to think about other option. But for now, its
more than enough for us to be agile and deploy as much as we want.

