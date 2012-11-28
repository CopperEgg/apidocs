---
layout: default
title: RevealMetrics - Samples
---


Overview
--------
These are the API calls for storing and retrieving data samples to/from RevealMetrics.


Storing a data sample
---------
To store a data sample, you POST the new value, referencing it using the metric name and metric group.

####Required parameters:
* the METRICGROUP_ID is specified as part of the path
* an "indentifier" which specifies the specific object of interest (server or probe)
* a "timestamp", which is a unix time stamp indicating the time of the data collection
* a "values" hash, containing one or more metrics to store (to the metric group specified by the METRICGROUP_ID).

####Optional parameters:
None


CURL Command:
{% highlight sh %}
curl -u APIKEY:U -H "Content-type: application/json" -XPOST https://api.copperegg.com/v2/revealmetrics/samples/METRICGROUP_ID.json -d '{"identifier": YOURIDENTIFIER,"timestamp": UNIXTIMESTAMP, "values": { METRICNAME: METRICVALUE}'
{% endhighlight %}

CURL Response:
A null response is returned

{% highlight sh %}
null
{% endhighlight %}



Reading one or more metrics from RevealMetrics
---------

####Required parameters:
* a "queries" hash, containing one or more metric group queries, where one or more metrics are requested from each metric group.

####Optional parameters:
* starttime: a unix time stamp indicating the first sample time of the series being requested. Default is NOW - 300 seconds.
* duration: the length of time for which data samples are being requested, in seconds. Default is 300 seconds.
* sample_size: Override the default sample size that is determined by the starttime/duration range. This will only work if you specify a sample_size larger than what is automatically calculated for the time range. If you specify a smaller sample_size, the default sample_size will be used. Default is 15s.

CURL Command:
{% highlight sh %}
curl -u APIKEY:U -XGET "https://api.copperegg.com/v2/revealmetrics/samples.json" -H "Content-Type: application/json" -d '{"queries":{"METRICGROUP_ID":[{"metrics":["METRICNAME"]}]}}'
{% endhighlight %}


CURL Response:
A Hash containing the requested data.

{% highlight sh %}
{
  "_ts":1354126050,             # unix timestamp indicating the first sample of this series (offset == 0)
  "values":{                    # a hash of all metrics returned
    "scottsmetrics_v2":[        # metric group id
      {
        "mymac":{               # server/probe identifier
          "0":[1354126055],"    # offset from starttime : data sample at that time
          15":[1354126070],
          "30":[1354126087],
          "45":[1354126102],
          "60":[1354126118],
          "75":[1354126134],
          "90":[1354126150],
          "105":[1354126166],
          "120":[1354126181],
          "135":[1354126197],
          "150":[1354126214],
          "180":[1354126232],
          "195":[1354126248],
          "210":[1354126263],
          "225":[1354126279],
          "240":[1354126295],
          "255":[1354126311],
          "270":[1354126327],
          "285":[1354126343]
        }
      }
    ]
  }
}
{% endhighlight %}

