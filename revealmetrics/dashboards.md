---
layout: default
title: Custom Metrics - Dashboards
---

## Overview
These are the API calls for retrieving, creating, updating and deleting Custom Metrics Dashboards.


----
#### Creating a Dashboard and populating it with Widgets


A Dashboard is specified by creating a Dashboard Hash, which contains one or more Widget Hashes. We'll start by describing how to specify a widget, then circle back to including them on a dashboard.

A Widget is an object that is characterized by a Widget Hash. There a variety of widgets available for you to choose from, with more on the way. All multi-metric widgets can be used to display one or more metrics. Single-metric widgets display one.
Today there are 3 widget sizes; let's refer to them as 1x, .5x and 2x. A 1X widget is the size of the widgets used in Systems and Probes dashboards. The .5x widget is sized such that 2 of them fit in the same space as a 1x widget. Likewise, a 2x widget consumes the same amount of space as two 1x widgets.

A (Ruby-formatted) Widget Hash looks like this:

{% highlight sh %}
  {
    "type"=>"metric_list",           # the type and style define which widget is used
    "style"=>"list",                 # this is a mult-metric widget
    "match"=>"tag",                  # this key-value pair allows selection of object by tag
    "label"=>"Cloud Portal Health",  # optional user-friendly widget label
    "metric"=>[                      # "metric" array specifying the metric to display
      "ce_probe_summary_v1",         # METRICGROUP_ID
      "6",                           # METRICGROUP_INDEX
      "health",                      # METRICNAME
      "rate"                         # optional modifier
    ],
    "match_param"=>"cloud"           # in combination with 'match', specifies selection of all objects with tag 'cloud'
  }
{% endhighlight %}


#### Single-metric widgets

Widget type 'metric'

These widgets are large enough to be readable from a distance. There are three styles of the 'metric' type widget:
 * 'value':    display the current metric value as a series of digits (.5x widget)
 * 'timeline': display a time-series sparkline of the metric changing over time (.5x widget)
 * 'both':     display both the current value numerically, and a time-series sparkline (1x widget)

In single-metric widgets, you will specify the source of the metric as follows:
 * assign the value 'select' to the 'match' key
 * assign the value 'object_id' to the 'match_param' key. The object_id my be a UUID, a PROBE_ID or a METRICGROUP_ID.

#### Multi-metric widgets

Widget type 'metric_list', style 'list'

This is a 1x widget that displays up to 7 single metrics, with both a current value and a small time-series sparkline. These are not intended for viewing from a distance.
The benefit of this style of widget lies in the visual presentation of a common metric from a number of sources.

Widget type 'timeline', style 'values'

This is a 2x widget that displays up to 7 metrics as lines on the same time-series chart.

For multi-metric widgets, the widget 'match' and 'match_param' keys are used to specify how to select the objects from which the widget will pull data.
 * 'match' == 'select'
    This will force the multi-metric widget to display a single metric. Using the multi-metric widgets this way is supported, but not encouraged.

 * 'match' == 'tag'
    All objects with the tag specified by the value of 'match_param' are selected. If more than 7 objects have matching tags, only 7 will be displayed.

 * 'match' == 'all'
    All objects are selected. The 'match_param' key-value pair is ignored (and may be left out). Again, if more than 7 objects are defined, only 7 will be displayed by the widget.

#### Specifying the Metric

As you can see in the above Widget Hash, there is a 'metric' hash key, with a value consisting of a three or four element array:
  "metric"=>\["ce_probe_summary_v1","6","health", "rate"\]

The 4 array elements are \[METRICGROUP_ID, METRICGROUP_INDEX, METRICNAME, "rate"\]
 * The METRICGROUP_ID is the unique identifier assigned by Uptime Cloud Monitor for a defined metric group.
 * The METRICGROUP_INDEX is the value of the 'position' key in the specified metric group.
 * The METRICNAME is the the same as the "name" defined in the metric group.
 * An optional field that may contain the word "rate"

***NOTE:***
 * "rate"
The word "rate" may be included as a fourth array element in the "metric" array. If included in a "metric" array specifying a counter metric, the counter value will be converted into a rate, and the rate will be displayed in the widget.
If the word "rate" is not included in a counter widget, the value of the counter is displayed.
"rate" should not be added to any "metric" array specifying a gauge metic.

 * You must supply the METRICGROUP_INDEX and the corresponding METRICNAME.
This is duplicate information; the duplication exists in v2 of the API for backward compatibility. It will be eliminated in an upcoming API release.


### The Dashboard Hash
As you can see below, the dashboard hash is an object that contains a hash of Widget Hashes, along with some metadata.
A JSON-encoded single-widget Dashboard Hash is provided below, as it would be delivered to you from Uptime Cloud Monitor, for example in response to a Create command:

{% highlight sh %}
  {
    "id":80,                          # unique dashboard id assigned by Uptime Cloud Monitor   NOTE: this is a numeric field
    "name":"SingleProbe",             # the display name of this dashboard, string
    "data":{                          # the widget data hash, containing two key-value pairs
      "widgets":{                     # a hash of widgets,
        "1":{                         # each widget hash must have a unique string representation of a numeric key
          "type":"metric",
          "style":"value",
          "label":"TestProbe",        # optional user-friendly lablel that you may add
          "metric":{
            "ce_probe_summary_v1":[   # METRICGROUP_ID
              [
                "1",                  # METRICGROUP_INDEX
                "connect_time",       # METRICNAME
                "rate"                # optional modifier
              ]
            ]
          },
          "match":"select",
          "match_param":"4ff7e3682ca1fc0c72000038"
        }
      },
      "order":["1"]                   # defines the order in which the widgets appear on this dashboard; NOT optional
    },
    "tags":[],                        # an optional list of tags to apply to this dashboard.
    "created_at":1354035004,          # time created, unix timestamp, UTC
    "updated_at":1354042044           # last time updated, unix timestamp, UTC
  }
{% endhighlight %}


NOTES:
 * The JSON-encoded Dashboard Hash that you provide in a Create or Update command is not identical to the JSON-encoded Dashboard Hash delivered in response, or in response to an Index command.
 * The "created_at" and "updated_at" fields are never included in any request, but are always returned in all response.
 * Also notice that the "metric" definition in a widget is specified in an array, but the response metric definitions are always in the form of a hash.

#### The "metric" array in a Widget Hash in a Dashboard Create command:

{% highlight sh %}
"metric":[
  "ce_probe_summary_v1",
  "1",
  "connect_time"
]
{% endhighlight %}


#### The "metric" hash in a Widget Hash in the Response from the above Create command:

{% highlight sh %}
"metric":{
  "ce_probe_summary_v1":[
    [
      "1",
      "connect_time"
    ]
  ]
}
{% endhighlight %}

The difference in the structures is mentioned at this point to avoid confusion when describing the commands and responses below.
The reason for the difference in structures has to do with new functionality which will be available in an upcoming API release.

-----
## Index

List all defined Custom Metrics Custom Dashboards.

#### Required parameters:
None.

#### Optional parameters:
None.

#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U https://api.copperegg.com/v2/revealmetrics/dashboards.json

curl -s https://<APIKEY>:U@api.copperegg.com/v2/revealmetrics/dashboards.json
{% endhighlight %}

#### CURL Response:

Response is a JSON-encoded array of Dashboard Hashes. In this example, there is one dashboard defined, which displays 4 widgets.
{% highlight sh %}
[
  {
    "id":61,                                                # unique dashboard ID, assigned by Uptime Cloud Monitor
    "name":"Service Monitoring",                            # Dashboard name, string
    "data":{                                                # the data hash consists of two key-value pairs, widgets and order
      "widgets":{                                           # array of widget hashes
        "0":{                                               # widget id
          "type":"timeline",                                # widget type
          "style":"values",                                 # widget style
          "match":"tag",                                    # what category to select on
          "label":"Cloud Portal Response Time (total)",     # Widget label
          "metric":{                                        # The "metric" hash
            "ce_probe_summary_v1":[
              [
                "0",
                "time"
              ]
            ]
          },
          "match_param":"cloud"                             # which member of the category to select on
        },
        "1":{
          "type":"metric_list",
          "style":"list",
          "match":"tag",
          "label":"Cloud Portal Health",
          "metric":{"ce_probe_summary_v1":[["6","health"]]},
          "match_param":"cloud"
        },
        "2":{
          "type":"timeline",
          "style":"values",
          "match":"tag",
          "label":"Social Sites Response Time (total)",
          "metric":{"ce_probe_summary_v1":[["0","time"]]},
          "match_param":"social"
        },
        "3":{
          "type":"metric_list",
          "style":"list",
          "match":"tag",
          "label":"Social Sites Health",
          "metric":{"ce_probe_summary_v1":[["6","health"]]},
          "match_param":"social"
        }
      },
      "order":["0","1","2","3"]                   # the order of the widgets on the screen |  0  1  2  |
    },                                            #                                        |  4  5  6  |
    "tags":[],
    "created_at":1353891562,                      # time created, unix timestamp, UTC
    "updated_at":1353938713                       # last time updated, unix timestamp, UTC
  }
]
{% endhighlight %}

------
## Create Dashboard

Create a new Dashboard

#### Required parameters:
 * You must include a dashboard "name" string, and a data hash, including both a widget hash and an order hash.
 * The widget hash must be one or more key-value pairs, where each key is a string-formatted number starting with "0"; each of these keys must have an associated widget hash value.
 * Each widget hash must include 'type', 'style', 'match' and a 'metric' value array. 'match_param' is not required for "match":"all"
 * order array, for laying out the widgets


#### Optional parameters:
 * label
 if not included, a default label will be created. Be descriptive!!!


#### Create Example; Create a new dashboard with a single widget. The dashboard will be named "My First Dash".
We'll also use a metric group named "ce_probe_summary_v1" which is a 'built-in' metric group. (You may have noticed this metric group in the Index example).


#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U -H "Content-type: application/json" -XPOST https://api.copperegg.com/v2/revealmetrics/dashboards.json -d '{"name":"My New Dash","data":{"widgets":{"0":{"type":"metric","style":"value","match":"tag","metric":["ce_probe_summary_v1","6","health"],"match_param":"cloud"}},"order":["0"]}}'
{% endhighlight %}


Please notice the format of the "metric" hash in the Create request:

{% highlight sh %}
"metric":[
  "ce_probe_summary_v1",
  "6",
  "health"
]
{% endhighlight %}


#### CURL Response:
Response is a JSON-encoded Dashboard Hash. Once again notice the format of the "metric" hash:

{% highlight sh %}
{
  "id":89,
  "name":"My New Dash",
  "data":{
    "widgets":{
      "0":{
        "type":"metric",
        "style":"value",
        "match":"tag",
        "metric":{"ce_probe_summary_v1":[["6","health"]]},
        "match_param":["cloud"]
      }
    },
    "order":["0"]
  },
  "tags":[],
  "created_at":1354048053,
  "updated_at":1354048053
}
{% endhighlight %}

------
## Update

Update an existing Dashboard and/or the widgets it displays.

#### Required parameters
 * Dashboard id, returned from an Index command or in response to the create command

#### Optional parameters
 * change the Dashboard label
 * modify existing widgets
 * add new widgets


#### Update Example: Add a widget to the dashboard created above.

#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U -H "Content-type: application/json" -XPUT https://api.copperegg.com/v2/revealmetrics/dashboards/<DASHBOARD_ID>.json -d '{"name":"My New Dash","data":{"widgets":{"0":{"type":"metric","style":"value","match":"tag","metric":["ce_probe_summary_v1","6","health"],"match_param":"cloud"},"1":{"type":"metric","style":"value","match":"tag","metric":["ce_probe_summary_v1","6","health"],"match_param":"onprem"}},"order":["0","1"]}}'
{% endhighlight %}

#### CURL Response:
Response is a JSON-formatted Dashboard hash.

{% highlight javascript %}
{
  "id":89,
  "name":"My New Dash",
  "data":{
    "widgets":{
      "0":{
        "type":"metric",
        "style":"value",
        "match":"tag",
        "metric":{"ce_probe_summary_v1":[["6","health"]]},
        "match_param":["cloud"]
      },
      "1":{
        "type":"metric",
        "style":"value",
        "match":"tag",
        "metric":{"ce_probe_summary_v1":[["6","health"]]},
        "match_param":["onprem"]
      }
    },
    "order":["0","1"]
  },
  tags":[],
  "created_at":1354050492,
  "updated_at":1354050561
}
{% endhighlight %}

-------
## Delete

Delete the specified Dashboard.

#### Required parameters
 * Dashboard id, as part of the path

#### Optional parameters
None


#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U -XDELETE  https://api.copperegg.com/v2/revealmetrics/dashboards/<DASHBOARD_ID>.json
{% endhighlight %}

#### CURL Response:

Response is Status 200, empty JSON:

{% highlight javascript %}
{}
{% endhighlight %}

