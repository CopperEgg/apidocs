---
layout: default
title: Custom Metrics - Metric Groups
---


## Overview
These are the API calls for listing, creating, updating and deleting Metric Groups.

----
### Definitions of Metric and Metric Group


A Metric for the purposes of this document is simply a quantity that we want to measure, record, chart and alert on. Each metric, whether 'built-in' or user-defined, is an object, characterized by a hash:

{% highlight sh %}
Metric Hash
  { "type"=> METRIC_TYPE,              # "ce_counter", "ce_gauge" or "ce_gauge_f"
    "name" => METRIC_NAME,             # built-in or user-defined, string
    "position" => METRIC_ARRAY_INDEX,  # position is an array index, assigned by Uptime Cloud Monitor
    "label" => METRIC_LABEL,           # user-friendly text describing the metric, string
    "unit" => METRIC_UNIT              # the units being measured, string
  }

For example, you will see this (Ruby-formatted) metric hash in a subsequent example:
  {
    "type"=>"ce_counter",             # METRIC_TYPE
    "name"=>"uptime",                 # METRIC_NAME
    "position"=>0,                    # METRIC_ARRAY_INDEX
    "label"=>"Uptime",                # METRIC_LABEL
    "unit"=>"Seconds"                 # METRIC_UNIT
  }
{% endhighlight %}

A Metric Group is a built-in or user-defined collection of Metrics, along with some metadata describing the group. Every Metric Group includes an array of metric hashes. The array of metric hashes must have at least one element.
In fact, a Metric Group is an object characterized by a hash:

Metric Group Hash (Ruby-formatted)
{% highlight sh %}
  {
    "id"=>METRIC_GROUP_ID,             # a unique Metric Group ID, assigned by Uptime Cloud Monitor
    "name"=>METRIC_GROUP_NAME,         # a unique name, built-in or user-defined, string
    "idp"=>INTERNAL_USE,               # internal use
    "label"=>METRIC_GROUP_LABEL,       # user-friendly text describing the metric group, string
    "frequency"=>POLLING_INTERVAL,     # polling interval in seconds; defaults to 60
    "metrics"=>[                       # the array of metrics that define this group (see above)
      {METRIC_HASH},
      {METRIC_HASH}
    ]
  }
{% endhighlight %}


Metric Group Hash (JSON-formatted)
{% highlight sh %}
  {
    "id":"redis",                     # METRIC_GROUP_ID
    "name":"redis",                   # METRIC_GROUP_NAME
    "idp":"custom|",
    "label":"Redis Metrics",          # METRIC_GROUP_LABEL
    "frequency":60,                   # POLLING_INTERVAL
    "metrics":[ {}, {} ]              # array of metrics hashes
  }
{% endhighlight %}

Summing up:
 * No metric stands alone. Every metric is defined in the context of a metric group.
 * A metric group exists to group metrics. A metric group must have at least one metric.
 * There is great power and flexibility in groups of metrics!
 * You can group metrics that you define, as well as in combination with system metrics from RevealCloud and website performance and availability metrics from RevealUptime.


-----
## Index

List all defined Custom Metrics Metric Groups.

#### Required parameters:
None.

#### Optional parameters:
None.

#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U https://api.copperegg.com/v2/revealmetrics/metric_groups.json

curl -s https://<APIKEY>:U@api.copperegg.com/v2/revealmetrics/metric_groups.json
{% endhighlight %}

#### CURL Response:

Response is a JSON array of Metric Group hashes. In this example, there is one metric group defined, which contains 6 metrics.
{% highlight sh %}
[
  {
    "id":"redis",               # METRIC_GROUP_ID, a unique identifier assigned by Uptime Cloud Monitor
    "name":"redis",             # METRIC_GROUP_NAME, user-defined metric group name
    "idp":"custom|",            # internal use only
    "label":"Redis Metrics",    # METRIC_GROUP_LABEL
    "frequency":60,             # POLLING_INTERVAL,  defaults to 60 seconds.
    "metrics":[                 # the array of metrics in this group
      {
        "type":"ce_counter",    # METRIC_TYPE
        "name":"uptime",        # METRIC_NAME
        "position":0,           # METRIC_ARRAY_INDEX
        "label":"Uptime",       # METRIC_LABEL
        "unit":"Seconds"        # the units of this metric
      },
      {
        "type":"ce_gauge_f",
        "name":"used_cpu_sys",
        "position":1,
        "label":"Used cpu sys",
        "unit":"Percent"
      },
      {
        "type":"ce_gauge_f",
        "name":"used_cpu_user",
        "position":2,
        "label":"Used cpu user",
        "unit":"Percent"
      },
      {
        "type":"ce_gauge",
        "name":"connected_clients",
        "position":3,
        "label":"Connected clients",
        "unit":"Clients"
      },
      {
        "type":"ce_gauge",
        "name":"connected_slaves",
        "position":4,
        "label":"Connected slaves",
        "unit":"Slaves"
      },
      {
        "type":"ce_gauge",
        "name":"blocked_clients",
        "position":5,
        "label":"Blocked clients",
        "unit":"Clients"
      }
    ]
  }
]
{% endhighlight %}

-----
## Show

Show all details of a single Metric Group.

#### Required parameters:

METRIC_GROUP_ID as part of the path

#### Optional parameters:
None.

#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U https://api.copperegg.com/v2/revealmetrics/metric_groups/METRIC_GROUP_ID.json
{% endhighlight %}

#### CURL Response:

Response is single Metric Group Hash. In this example, the metric group is the same as that returned in the Index example.
{% highlight sh %}
[
  {
    "id":"redis",
    "name":"redis",
    "idp":"custom|",
    "label":"Redis Metrics",
    "frequency":60,
    "metrics":[
      {
        "type":"ce_counter",
        "name":"uptime",
        "position":0,
        "label":"Uptime",
        "unit":"Seconds"
      },
      {
        "type":"ce_gauge_f",
        "name":"used_cpu_sys",
        "position":1,
        "label":"Used cpu sys",
        "unit":"Percent"
      },
      {
        "type":"ce_gauge_f",
        "name":"used_cpu_user",
        "position":2,
        "label":"Used cpu user",
        "unit":"Percent"
      },
      {
        "type":"ce_gauge",
        "name":"connected_clients",
        "position":3,
        "label":"Connected clients",
        "unit":"Clients"
      },
      {
        "type":"ce_gauge",
        "name":"connected_slaves",
        "position":4,
        "label":"Connected slaves",
        "unit":"Slaves"
      },
      {
        "type":"ce_gauge",
        "name":"blocked_clients",
        "position":5,
        "label":"Blocked clients",
        "unit":"Clients"
      }
    ]
  }
]
{% endhighlight %}

------
## Create Metric Group

Create a new Metric Group.

#### Required parameters:
* You must include a metric group "name" string and an array of metrics. The metric group name can not contain spaces or periods.

* Each Metric hash must contain 3 key-value pairs: type, name, and unit. You can optionally specify a label.

#### Optional parameters:

* frequency
  if not included, the polling frequency will be once per minute. (polling period 60 seconds)

* label
  if not included, a default label will be created. Be descriptive!!!


#### Create Example 1: Create a small group of metrics using two of the metrics from the example above. We'll call this new metric group 'myredis'.
We'll also use the bare minimum required parameters, to demonstrate the defaults.


#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U -H "Content-type: application/json" -XPOST https://api.copperegg.com/v2/revealmetrics/metric_groups.json -d '{"name":"myredis","metrics":[{"type":"ce_counter","name":"uptime","unit":"Seconds"},{"type":"ce_gauge","name":"connected_clients","unit":"Clients"}]}'
{% endhighlight %}


#### CURL Response:

Response is Status 200, and the metric group hash created:
{% highlight sh %}
{
  "id":"myredis",
  "name":"myredis",
  "idp":"custom|",
  "label":"Myredis",
  "frequency":60,
  "metrics":[
    {
      "type":"ce_counter",
      "name":"uptime",
      "position":0,
      "label":"Uptime",
      "unit":"Seconds"
    },
    {
      "type":"ce_gauge",
      "name":"connected_clients",
      "position":1,
      "label":"Connected clients",
      "unit":"Clients"
    }
  ]
}
{% endhighlight %}


#### Create Example 2: Create a small group of metrics using two of the metrics from the example above. We'll call this new metric group 'newredis'.
This time we'll specify frequency and labels.

#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U -H "Content-type: application/json" -XPOST https://api.copperegg.com/v2/revealmetrics/metric_groups.json -d '{"name":"newredis","frequency":15,"label":"Well-Labelled Redis","metrics":[{"type":"ce_counter","name":"uptime","label":"UPTIME","unit":"Seconds"},{"type":"ce_gauge","name":"connected_clients","unit":"Clients"}]}'
{% endhighlight %}

#### CURL Response:

Response is Status 200, and the metric group hash created:
{% highlight sh %}
  {
    "id":"newredis",
    "name":"newredis",
    "idp":"custom|",
    "label":"Well-Labelled Redis",        # our verbose label
    "frequency":15,                       # our non-default polling frequency
    "metrics":[
      {
        "type":"ce_counter",
        "name":"uptime",
        "position":0,
        "label":"UPTIME",                 # our non-default label
        "unit":"Seconds"
      },
      {
        "type":"ce_gauge",
        "name":"connected_clients",
        "position":1,
        "label":"Connected clients",
        "unit":"Clients"
      }
    ]
  }
{% endhighlight %}

#### Create Example 2: Attempt to create a metric group with name containing spaces.

#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U -H "Content-type: application/json" -XPOST https://api.copperegg.com/v2/revealmetrics/metric_groups.json -d '{"name":"new   redis","frequency":15,"label":"Well-Labelled Redis","metrics":[{"type":"ce_counter","name":"uptime","label":"UPTIME","unit":"Seconds"},{"type":"ce_gauge","name":"connected_clients","unit":"Clients"}]}'
{% endhighlight %}

#### CURL Response:

Response is Status 403 and an error message is returned:
{% highlight sh %}
{
	"error": true,
	"error_type": "message",
	"message": "error: Metric Group name can not contain spaces or periods."
}
{% endhighlight %}

------
## Update

Update an existing Metric Group.

#### Required parameters

METRIC_GROUP_ID as part of the path


#### Optional parameters

* frequency, if you want to alter it

* any labels that you want to alter

* add new metrics

#### CURL REQUEST
{% highlight sh %}
curl -su <APIKEY>:U -H "Content-type: application/json" -XPUT https://api.copperegg.com/v2/revealmetrics/metric_groups/<METRIC_GROUP_ID> -d '{<UPDATED_VALUES_HASH>}'
{% endhighlight %}

#### Update Example 1: Change frequency of the metric group created above to every 15 seconds.  (where id="myredis")

#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U -H "Content-type: application/json" -XPUT https://api.copperegg.com/v2/revealmetrics/metric_groups/myredis.json -d '{"frequency":15}'
{% endhighlight %}

#### CURL Response:

Response is Status 200, updated metric group hash:
{% highlight sh %}
{
  "id":"myredis",
  "name":"myredis",
  "idp":"custom|",
  "label":"Myredis",
  "frequency":15,
  "metrics":[
    {
      "type":"ce_counter",
      "name":"uptime",
      "position":0,
      "label":"Uptime",
      "unit":"Seconds"
    },
    {
      "type":"ce_gauge",
      "name":"connected_clients",
      "position":1,
      "label":"Connected clients",
      "unit":"Clients"
    }
  ]
}
{% endhighlight %}


#### Update Example 2: Add a metric to a metric group. (where id="myredis")
NOTE: You don't need to repeat the already-existing metrics.
{% highlight sh %}
curl -su <APIKEY>:U -H "Content-type: application/json" -XPUT https://api.copperegg.com/v2/revealmetrics/metric_groups/myredis4.json -d '{"metrics":[{"type":"ce_gauge","name":"connected_slaves","unit":"Slaves"}]}'
{% endhighlight %}

#### CURL Response:

Response is Status 200, updated metric group hash:

{% highlight sh %}
{
  "id":"myredis",
  "name":"myredis",
  "idp":"custom|",
  "label":"Myredis",
  "frequency":15,
  "metrics":[
    {
      "type":"ce_counter",
      "name":"uptime",
      "position":0,
      "label":"Uptime",
      "unit":"Seconds"
    },
    {
      "type":"ce_gauge",
      "name":"connected_clients",
      "position":1,
      "label":"Connected clients",
      "unit":"Clients"
    },
    {
      "type":"ce_gauge",
      "name":"connected_slaves",
      "position":2,
      "label":"Connected slaves",
      "unit":"Slaves"
    }
  ]
}
{% endhighlight %}

------
## Delete

Delete the specified Metric Group.

#### Required parameters

METRIC_GROUP_ID as part of the path

#### Optional parameters
None


#### CURL Command, and variations:
{% highlight sh %}
curl  -su <APIKEY>:U -XDELETE  https://api.copperegg.com/v2/revealmetrics/metric_groups/<METRICGROUP_ID>.json
{% endhighlight %}

#### CURL Response:

Response is Status 200, empty JSON:

{% highlight javascript %}
{}
{% endhighlight %}

