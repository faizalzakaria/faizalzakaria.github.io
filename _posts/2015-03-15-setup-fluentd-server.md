
can also install fluentD using [Chef](https://www.chef.io/chef/), and I prefer to use [this](https://github.com/dmytro/fluentd-cookbook).

You can configure a fluentD chef role  as such:

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

