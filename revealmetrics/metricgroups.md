---
layout: default
title: RevealMetrics - Metric Groups
---


Overview
--------
These are the API calls for listing, creating, updating and deleting Metric Groups.


Definitions of Metric and Metric Group
--------

A Metric for the purposes of this document is simply a quantity that we want to measure, record, chart and alert on. Each metric, whether 'built-in' or user-defined, is an object, characterized by a hash:

{% highlight sh %}
Metric Hash
  { "type"=> METRICTYPE,              # today, "ce_counter", "ce_gauge" or "ce_gauge_f"
    "name" => METRICNAME,             # built-in or user-defined, string
    "position" => METRIC_ARRAYINDEX,  # position is an array index, assigned by RevealMetrics
    "label" => METRICLABEL,           # meaningful text describing the metric, string
    "unit" => METRICUNITS             # the units being measured, string
  }

For example, you will see this metric hash in a subsequent example:
  {
    "type"=>"ce_counter",
    "name"=>"uptime",
    "position"=>0,
    "label"=>"Uptime",
    "unit"=>"Seconds"
  }
{% endhighlight %}

A Metric Group is a built-in or user-defined collection of Metrics, along with some metadata describing the group. Every Metric Group includes an array of metric hashes. The array of metric hashes must have at least one element.
In fact, a Metric Group is an object characterized by a hash:

{% highlight sh %}
Metric Group Hash
  {
    "id"=>METRICGROUP_ID,         # a unique Metric Group ID, assigned by RevealMetrics
    "name"=>METRICGROUP_NAME,     # a unique name, built-in or user-defined, string
    "idp"=>INTERNAL_USE,          # internal use
    "label"=>METRICGROUP_LABEL,   # meaningful text describing the metric group, string
    "frequency"=>POLLINGINTERVAL, # polling interval in seconds; defaults to 60
    "metrics"=>[                  # the array of metrics that define this group (see above)
      {METRICHASH},
      {METRICHASH}
    ]
  }

For example, you will see the following metric group below:
  {
    "id":"redis",
    "name":"redis",
    "idp":"custom|",
    "label":"Redis Metrics",
    "frequency":60,
    "metrics":[ {}, {} ]
  }
{% endhighlight %}

Summing up:
* No metric stands alone. Every metric is defined in the context of a metric group.
* A metric group exists to group metrics. A metric group must have at least one metric.
* SPOILER #1: there is great power and flexibility in groups of metrics!
* SPOILER #2: you can group metrics that you define, as well as in combination with system metrics from RevealCloud and website performance and availability metrics from RevealUptime.



Index
-----
List all defined RevealMetrics Metric Groups.

####Required parameters:
None.

####Optional parameters:
None.

CURL Command:
{% highlight sh %}
curl -u APIKEY:U https://api.copperegg.com//v2/revealmetrics/metric_groups.json
{% endhighlight %}

CURL Response:

Response is a JSON array of Metric Group hashes. In this example, there is one metric group defined, which contains 6 metrics.
{% highlight sh %}
[
  {
    "id":"redis",               # unique identifier assigned by RevealMetrics
    "name":"redis",             # user-defined metric group name
    "idp":"custom|",            # internal use only
    "label":"Redis Metrics",    # metric group label; optionally may be user-defined
    "frequency":60,             # polling interval; defaults to 60 secondss.
    "metrics":[                 # the array of metrics in this group
      {
        "type":"ce_counter",    # metric types are defined in the Create section
        "name":"uptime",        # user-defined unique metric name
        "position":0,           # index of this element in the metrics array, assigned by RevealMetrics
        "label":"Uptime",       # metric label that will appear in the UI and reports; optionally may be user-defined
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


Show
-----
Show all details of a single Metric Group.

####Required parameters:
* metric group id, provided as part of the path name

####Optional parameters:
None.

CURL Command:
{% highlight sh %}
curl -u APIKEY:U https://api.copperegg.com//v2/revealmetrics/metric_groups/METRIC_GROUP_ID.json
{% endhighlight %}

CURL Response:

Response is single Metric Group hash. In this example, the metric group is the same as that returned in the Index example.
{% highlight sh %}
[
  {
    "id":"redis",               # unique identifier assigned by RevealMetrics
    "name":"redis",             # user-defined metric group name
    "idp":"custom|",            # internal use only
    "label":"Redis Metrics",    # metric group label; optionally may be user-defined
    "frequency":60,             # polling interval; defaults to 60 secondss.
    "metrics":[                 # the array of metrics in this group
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


Create Metric Group
------
Create a new Metric Group.

####Required parameters:
* You must include a metric group "name" string and an array of metrics.

* Each Metric hash must contain 3 key-value pairs: type, name and unit. You can optionally specify a label.

####Optional parameters:

* frequency
  if not included, the polling frequency will be once per minute. (polling period 60 seconds)

* label
  if not included, a default label will be created. Be descriptive!!!


####Create Example 1: create a small group of metrics using two of the metrics from the example above. We'll call this new metric group 'myredis'.
We'll also use the bare minimum required parameters, to demonstrate the defaults.

CURL Command:
{% highlight sh %}
curl -u APIKEY:U -H "Content-type: application/json" -XPOST https://api.copperegg.com/v2/revealmetrics/metric_groups.json -d '{"name":"myredis","metrics":[{"type":"ce_counter","name":"uptime","unit":"Seconds"},{"type":"ce_gauge","name":"connected_clients","unit":"Clients"}]}'
{% endhighlight %}


CURL Response:

Response is Status 200, empty JSON:

{% highlight javascript %}
{}
{% endhighlight %}

Now do an Index command, and see what we've created:

CURL Command:
{% highlight sh %}
curl -u APIKEY:U https://api.copperegg.com//v2/revealmetrics/metric_groups.json
{% endhighlight %}

In the response you will find:
{% highlight sh %}
  {
    "id":"myredis",         # the id assigned
    "name":"myredis",       # the name string we passed-in
    "idp":"custom|",
    "label":"Myredis",      # the default label created by RevealMetrics
    "frequency":60,         # the default polling interval
    "metrics":[
      {
        "type":"ce_counter",
        "name":"uptime",
        "position":0,       # position assigned by RM
        "label":"Uptime",   # label assigne by RM
        "unit":"Seconds"    # the unit string we passed-in
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


####Create Example 2: create a small group of metrics using two of the metrics from the example above. We'll call this new metric group 'newredis'.
This time we'll specify frequency and labels.


CURL Command:
{% highlight sh %}
curl -u APIKEY:U -H "Content-type: application/json" -XPOST https://api.copperegg.com/v2/revealmetrics/metric_groups.json -d '{"name":"newredis","frequency":15,"label":"Well-Labelled Redis","metrics":[{"type":"ce_counter","name":"uptime","label":"UPTIME","unit":"Seconds"},{"type":"ce_gauge","name":"connected_clients","unit":"Clients"}]}'
{% endhighlight %}

CURL Response:

Response is Status 200, empty JSON:

{% highlight javascript %}
{}
{% endhighlight %}

Now do an Index command, and see what we've created:

CURL Command:
{% highlight sh %}
curl -u APIKEY:U https://api.copperegg.com//v2/revealmetrics/metric_groups.json
{% endhighlight %}

In the response you will find:
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


Update
------
Update an existing Metric Group.

####Required parameters

* Metric Group id, returned from an Index command


####Optional parameters

* frequency, if you want to alter it

* any labels that you want to alter

* add new metrics


####Update Example 1: change frequency of the metric group created above to every 15 seconds.  (where id="myredis4")

CURL Command:
{% highlight sh %}
curl -u APIKEY:U -H "Content-type: application/json" -XPUT https://api.copperegg.com/v2/revealmetrics/metric_groups/myredis4.json -d '{"frequency":60}'
{% endhighlight %}

CURL Response:

Response is Status 200, empty JSON:

{% highlight javascript %}
{}
{% endhighlight %}


####Update Example 2: Add a metric to the metric group. (where id="myredis4")
NOTE: You don't need to repeat the already-existing metrics.

curl -u APIKEY:U -H "Content-type: application/json" -XPUT https://api.copperegg.com/v2/revealmetrics/metric_groups/myredis4.json -d '{"metrics":[{"type":"ce_gauge","name":"connected_slaves","unit":"Slaves"}]}'

CURL Response:

Response is Status 200, empty JSON:

{% highlight javascript %}
{}
{% endhighlight %}



Remove
-------
Remove the specified Metric Group.

####Required parameters

* Metric Group id, as part of the path


####Optional parameters
None


CURL Command:
{% highlight sh %}
curl  -u APIKEY:U -XDELETE  https://api.copperegg.com/v2/revealmetrics/metric_groups/METRICGROUP_ID.json
{% endhighlight %}

CURL Response:

Response is Status 200, empty JSON:

{% highlight javascript %}
{}
{% endhighlight %}


