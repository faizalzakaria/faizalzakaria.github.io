---
layout:     post
title:      "How to setup FluentD with S3"
date:       2015-03-14 3:45pm
author:     "Faizal F Zakaria"
header-img: "img/post-bg-01.jpg"
excerpt:    "This post is briefly to show you how we could setup the fluentD server with S3"
---

This post is briefly show you how we could setup the fluentD server with S3.

### Im going to use:

- digital ocean, a cheap server of $5 / month
- fluentD Chef cookbook, [this](https://github.com/dmytro/fluentd-cookbook)
- fluentd_service chef cookbook, [Chef](https://github.com/faizalfikhri/fluentd_service-cookbook)

You can configure a fluentD chef role as such:

{% highlight json %}
{
  "name": "fluentd_server",
  "description": "",
  "json_class": "Chef::Role",
  "default_attributes": {
  },
  "override_attributes": {
    "fluentd": {
      "plugins": [ "s3" ],
      "configs": {
        "source": [
          {
            "type": "forward",
            "port": "24224",
            "tag": "forward_24224"
          }
        ],
        "match": [
          {
            "match": "td.duriana_db.requests.production",
            "type": "s3",
            "aws_key_id": "YOUR AWS KEY",
            "aws_sec_key": "YOUR AWS SECRET KEY",
            "s3_bucket": "YOUR S3 BUCKET NAME",
            "s3_region": "ap-southeast-1",
            "store_as": "gzip",
            "path": "fluent/phonebook-backend/logs",
            "buffer_path": "/var/log/fluent/buf/s3/phonebook",
            "time_slice_format": "%Y/%m/%d/%H",
            "time_slice_wait": "10m",
            "format": "json",
            "include_time_key": "true"
          },
          {
            "match": "debug.test",
            "type": "stdout"
          },
        ]
      }
    }
  },
  "chef_type": "role",
  "run_list": [
    "recipe[fluentd]"
  ],
  "env_run_lists": {
  }
}
{% endhighlight %}

But there is a limitation on this chef cookbook. I'm extending it through fluentd_service-cookbook, where it would use my own template to create match and source conf files.
