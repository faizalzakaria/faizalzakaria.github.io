---
layout:     post
title:      "Heroku deployment"
date:       2015-06-09 3:00pm
author:     "Faizal F Zakaria"
header-img: "img/post-bg-01.jpg"
excerpt:    "You have a lot of heroku instances but forgot which of which ?"
---

Heroku is awesome, free for 5 apps for each user. Free stuff is always
great, so far Heroku does not block a unique user to have more than 5
apps. So all you have to do is to have more than 1 Heroku account. But
this get very tricky, when you have to handle > 1 Heroku account.

Heroku-deployment comes in handy. You could easily configure/deploy
your apps to Heroku, without worrying about the repetition works, and
memorize which Heroku account of each app belongs to.

This tools is written with Rake framework using Ruby.

You can get the code [https://github.com/faizalzakaria/heroku-deployment](https://github.com/faizalzakaria/heroku-deployment)

Pre-requisites

{% highlight ruby %}
bundle install
{% endhighlight %}

Then to get all the tasks:

{% highlight ruby %}
bundle exec rake -T
{% endhighlight %}

The tool will read the config.yml file in your root folder.

You could just copy the config.yml.sample, and configure your apps.


This is a list of apps that you want to handle

{% highlight ruby %}
:tasks: [ idonethis, vinti ]
{% endhighlight %}

This is the config for each app

{% highlight ruby %}
:idonethis:
  :github: 'git@github.com:faizalzakaria/idonethis.git'
  :branch: 'master'
  :scales: ['web']
  :staging:
    :envs:
      TEST1: 'test'
      TEST2: 'test'
    :accounts:
      - :name: 'phaibusiness'
        :apps:
          - 'idonethis3'
  :production:
    :accounts:
      - :name: 'phaibusiness'
        :apps:
          - 'idonethis-prod'

:vinti:
  :github: 'git@github.com:faizalzakaria/vinti.git'
  :branch: 'master'
  :scales: ['web']
  :staging:
    :branch: 'master1'
    :accounts:
      - :name: 'phaibusiness'
        :apps:
          - 'vinti'
  :production:
    :envs:
    :accounts:
      - :name: 'phaibusiness'
        :apps:
          - 'vinti-prod-1'
{% endhighlight %}

It also handles different environment, staging and production.

Then you could deploy your app as such:


{% highlight ruby %}
bundle exec rake deploy:idonethis[staging]
or (for short form)
bundle exec rake deploy:idonethis[s]
{% endhighlight %}

I hope this is helpful.
