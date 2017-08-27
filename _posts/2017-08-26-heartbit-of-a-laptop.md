---
layout: post
title: Heartbit of my laptop
author: Faizal F Zakaria
header-img: img/heartbit.jpg
excerpt: >-
  <h4>Heartbit of my laptop ?</h4> Do you work from a coffee shop, co working
  space, or a public area ? And you need a quick trip to restroom ? Isn't
  annoying that none can help you to keep an eye on your laptop ? The source of
  your income.
published: true
---

### Briefly the context

Since I quit my job as a CTO of Duriana.com (acquired by
[Carousell.com](https://carousell.com/)), which was around Nov 2015,
I've been working remotely, travelling around the world with my wife, to name a
few, Turkey 2 weeks, small island in Thailand for 2 weeks, Japan 2
weeks, Ho Chi Minh 3 weeks, Bali & Lombok 3 weeks, South Korea 1
month, Australia 1 month, Chiang Mai 1 month, etc, from one coffee shop to another, to work, in a very unique way as much as possible, but yet still keep my productivity high.

I won't say that I'm fully Nomad, but I try to enjoy life while I
can. The things that drive me the most is work and travel.

But things that I realized was, it was a challenge for me to stay in a
1 coffee shop for a longer period of time, when I'm working alone. Why
? Because every 3 hours, I would definitely need a restroom, to do a
quick business or sometimes worst, I need a quick dump. Leaving my laptop unattended is just too risky (or
maybe I just too paranoid). And most of the time, I ended up packing
up my bag and leave, and then hop on to the next coffee shop. Sometimes I just don't feel like moving to another coffee shop, but I'm just too paranoid to leave it unattended although all I need is just in average likely 5 - 10 minutes.

### How HeartTop was borned ?

So HeartTop was borned upon my frustration of working alone in a coffee shop, working space or a public area. Why the name of HeartTop ? Well, it stands for Heartbit of my Laptop.

It was borned in [Punspace](http://www.punspace.com/), an awesome co-working space in Chiang Mai, I had my weekend without my wife, and I quickly hack it to make it works before the night market started. So I took a good 2 hours, and came out with a prototype, make it pluginable as much as possible, and leverage the Slack webhook and notification infrastructure, to ping my laptop heartbit every 10 seconds.

### So how it works ?

Well right now, it only supports Slack as a plugin, its pretty much straight forward,

- you run the HeartTop with Slack incoming Webhook url (assuming you have slack installed in your mobile).
- Once run, leave your laptop open,
- run the screensaver,
- lock the screen,
- and enjoy walking around the City without your laptop. Isn't awesome ?
- Or you can dump calmly. :)

Well I tried running it for 60 minutes, walked around the night
market, worry less, left my laptop unattended at the co-working space.

Why [slack](https://slack.com/) ? It is a very obvious reason, I only
need a notification infra, by using [Slack](https://slack.com/), I don't have to build the Mobile app, plus [Slack](https://slack.com/) is very responsive on incoming webhooks, pretty much reliable, every 10 seconds it sends push notification to my phone almost without a miss.

![Heartbit](/img/heartbit1.jpg)

### Conclusion

I feel relaxed since, less worried about my laptop, I can just pretty
much walk around, without it. It feels like my laptop is just so close
to me, that I can feel its breathing every 10 seconds. I also tested this in a co-working space in Malaysia, [worq](https://worq.space/), and I've been using it since.

So for those who work remotely, somewhere, in a random area, likely this could be very helpful to you.

Of course, people might think, someone can just steals it, but at
least I know something is just not right, as soon as the heartbit stops. Just like when you leave your kids at home, it could be good if you could feel the hearbit of your kids every N seconds, no ?

Few things that I think it could be improved,

- Likely to send picture of the surrounding every N seconds
- Run in in the driver layer.

If you feel like contributing, here is the link,
[https://github.com/faizalzakaria/heart_top](https://github.com/faizalzakaria/heart_top).
Just keep in mind, the code is still in MVP mode.
