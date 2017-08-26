---
layout: post
title: Test Opsworks in Vagrant
date: 'Mon Sep 21 23:17:38 MYT 2015'
author: Faizal F Zakaria
header-img: img/post-bg-01.jpg
excerpt: How annoying it is to test Opsworks custom recipe in AWS ?
published: true
---

<h4>How Opsworks work?</h4>

Opsworks is built on top of Chef framework. It has its own cli, called
`opsworks-agent-cli`. You can send different Opsworks lifecycle event
(`setup`, `configure`, `deploy`, `undeploy`, `shutdown`) to the server
through this tool.

This tool will read a file from
`/var/lib/aws/opsworks/chef/*.json`. This file has the environment
configuration in json format.

To simulate this in Vagrant, we need to install this tool in the
vagrant instance (and of course you need a few other dependencies to
make this work). The easiest would be to just use
[vagrant-opsworks](https://github.com/wwestenbrink/vagrant-opsworks){:target:"_blank"}.

To setup `vagrant-opsworks`, you just have to follow the steps
mentioned in the README.

<h4>What to do next?</h4>

Assuming you have `vagrant-opsworks` up and running, then you can
create a `Vagrantfile` or just define new box as below:

{% highlight ruby %}
  config.vm.define :opsworks do |int_config|
    # git@github.com:wwestenbrink/vagrant-opsworks.git
    # rake virtualbox-build
    # rake virtualbox-install
    int_config.vm.box = "ubuntu1404-opsworks"

    config.vm.provision :shell, inline: "opsworks-agent-cli"
  end
{% endhighlight %}

(For more details, you can check
[here](https://github.com/codegarageco/Codegarage-Chef-Hosted/blob/master/Vagrantfile))

Then bring the box up as such:

{% highlight ruby %}
vagrant up
vagrant ssh
opsworks-agent-cli setup
{% endhighlight %}

Access to the vagrant shell and try out the cli, `opsworks-agent-cli`. If
the cli is missing, then there was an error during the `vagrant-opsworks`
box provision. You might need to restart the rake build process.

Then you need to get a sample of opsworks json file from one of your
server. You can get it through `opsworks-agent-cli` command, and the json file
would look something as below :

{% highlight ruby %}
{
  "ssh_users": {
    "2007": {
      "name": "faizal",
      "public_key": "....",
      "sudoer": true
    },
  "deploy": {
    ......
  },
  "unicorn": {
    "preload_app": true,
    "timeout": 60
  }
}
{% endhighlight %}

Feel free to get in touch with me to know more on how to do this.
