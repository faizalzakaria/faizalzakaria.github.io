---
layout:     post
title:      "Chef handler that send notification to slack/hipchat"
date:       2015-06-19 3:45pm
author:     "Faizal F Zakaria"
header-img: "img/post-bg-01.jpg"
excerpt:    "Chef handler to notify the run status of your command to slack and/or hipchat"
---

<h4>Have you wondered how could you send report about your command on
every success / failed chef run?</h4>

Well Chef has a feature called handlers, and there are few handlers
that it could support,

* exception
* report
* start

You could extend the Chef::Handler class, and overwrite the handlers,
and run your own piece of code.

Example:

{% highlight ruby %}
# chef/handler/my_own_handler.rb
class MyOwnHandler < ::Chef::Handler

  def report
    puts 'Hello World'
  end
end
{% endhighlight %}

Then you can load your chef handler in your own cookbook like below:

{% highlight ruby %}
# recipes/default.rb
chef_handler 'MyOwnHandler' do
  source 'chef/handler/my_own_handler'
  action :enable
end
{% endhighlight %}

<p></p>
<h4>My Goal ?</h4>

Here, I'm interested to send repot to slack and hipchat. Well we had
Hipchat back then, but we moved to slack. So my main goal right is
slack, but I keep the support to hipchat regardless.

The report is sent to slack as an attachment, that could be easily
identified, that its coming from Chef.

Example of outputs are as below:

<h4>Failed build</h4>
![Failed build](/img/Failed.png)

<h4>Success build</h4>
![Success build](/img/Success.png)

The handler implementation can be found
[here](https://github.com/faizalzakaria/chef-handler-status_notifier).

I split out the implementation from the cookbook, to easily test this
seperately and indepandantly.

The cookbok can be found
[here](https://github.com/faizalzakaria/chef-run-notifier)

The implementation is pretty straight forward,

{% highlight ruby %}
# recipes/default.rb

include_recipe "chef_handler"

# Install our gem that has the handler, to send report to slack/hipchat
chef_gem 'chef-handler-status_notifier' do
  action :upgrade
end

require 'chef/handler/status_notifier'

# Install the handler as such.
chef_handler 'StatusNotifierHandler' do
  source 'chef/handler/status_notifier'
  arguments [node[:run_notifier][:slack], node[:run_notifier][:hipchat]]
  action :nothing
end.run_action(:enable)
{% endhighlight %}

Sample of usage of this cookbook, if you create a simple cookbook
wrapper, and you could easily reuse that wrapper cookbook on all of
your instances:

{% highlight ruby %}
# attributes/default.rb

default[:run_notifier][:hipchat] = {}
# Disable hipchat
default[:run_notifier][:hipchat][:enabled] = false
default[:run_notifier][:slack] = {}

# Enable slack
default[:run_notifier][:slack][:enabled] = true
default[:run_notifier][:slack][:webhook_url] = "https://hooks.slack.com/services/ABCDEFG/HIGJKELKJG"
default[:run_notifier][:slack][:channel] = "#ci-all"
{% endhighlight %}

{% highlight ruby %}
# recipes/my_notifier.rb

include_recipe 'run-notifier'
{% endhighlight %}

I hope this helps.

![Sample](/img/samples.png)
