---
published: true
---
## Heartbit of my laptop.

### Briefly the context

Since I quit as a CTO of Duriana.com (acquired by [Carousell.com](https://carousell.com/)), which was around Nov 2015, I've been working remotely, travelling around the world, to name a few, Turkey 2 weeks, small island in Thailand for 2 weeks, Japan 2 weeks, Ho Chi Minh 3 weeks, Bali & Lombok 3 weeks, Australia 1 month, Chiang Mai 1 month, etc, from one coffee shop to another, to work, in a very unique way as much as possible, but yet still keep my productivity high.

But things that I realized was, it was a challenge for me to stay in a 1 coffee shop for a longer period of time, when I'm working alone. Why ? Because every 3 hours, I would defenitely need a restroom, to do a quick business. Leaving my laptop unattended is just too risky (or maybe I don't have worry that much). And most of the time, I ended up packing up my bag and just leave and hop on to the next coffee shop. Sometimes I just don't feel like moving to another coffee shop, but I'm just too paranoid to leave it unattended although all I need is just in average likely 5 - 10 minutes.

### How HeartTop was borned ?

So HeartTop was borned upon my frustration of working alone in a coffee shop, working space or a public area. Why the name of HeartTop ? Well, it stands for Heartbit of my Laptop. Likely I could come up with a better name, but who cares ?

It was borned in [Punspace](http://www.punspace.com/), an awesome co-working space in Chiang Mai, I had my weekend without my wife, and I quickly hack it to make it works before the night market started. So I took a good 1 to 2 hours, and came out with a prototype, make it pluginable as much as possible, and leverage the Slack webhook and notification infrastructure, to ping my laptop heart bit every 10 seconds.

### So how it works ?

Well right now, it only supports Slack as a plugin, its pretty much straight forward, you run the HeartTop with Slack incoming Webhook url (assuming you have slack installed in your mobile). Once run, leave your laptop open, run the screensaver, lock it, and enjoy walking around the City without your laptop. Isn't awesome ?

### Why [slack](https://slack.com/) ? 

Its a very obvious reason, I only need a notifications infra, using [Slack](https://slack.com/), I don't have to build the Mobile app, plus [Slack](https://slack.com/) is very responsive on incoming webhooks, pretty much reliable, on every 10 seconds it sends push notification to my phone without almost a miss.

### Conclusion

I feel relax since, less worried about my laptop, I can just pretty much walking around, without it. It feels like my laptop is just so close to me, that I can feel its breathing every 10 seconds. I also tested this in any co-working space in Malaysia, leave it unattended, and just walk around the Mall, with less worry, I just feel more relax. :).

So for those who work remotely, somewhere, in a random area, likely this could be very helpful to you.

Of course, people might think, someone can just steal it, but at least I know something just not right, as soon as the heartbit stops. Just like when you leave your kids at home, it could be good if you could feel the hearbit of your kids every N seconds, right ? 

Few things I think it could be improved, 

- Likely to send picture of the surrounding every N seconds
- Run in in the driver layer.

If you feel like contributing, here is the link, https://github.com/faizalzakaria/heart_top .


Enter text in [Markdown](http://daringfireball.net/projects/markdown/). Use the toolbar above, or click the **?** button for formatting help.
