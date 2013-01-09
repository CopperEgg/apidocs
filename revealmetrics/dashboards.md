---
layout: default
title: Custom Metrics - Dashboards
---


Overview
--------
These are the API calls for listing, creating, updating and deleting Custom Metrics Dashboards.


Creating a Dashboard and populating it with Widgets
--------

A Dashboard is specified by creating a Dashboard hash, which contains one or more Widget hashes. We'll start by describing how to specify a widget, then circle back to including them on a dashboard.

A Widget is an object that is characterized by a Widget hash. There a variety of widgets available for you to choose from today, with more on the way. All multi-metric widgets can be used to display one or more metrics. Single-metric widgets display one.
Also note that today there are 3 widget sizes; let's refer to them as 1x, .5x and 2x. A 1X widget is the size of the widgets used in Systems (RevealCloud) and Probes (RevealUptime) dashboards. The .5x widget is sized such that 2 of them fit in the same space as a 1x widget. Likewise, a 2x widget consumes the same amount of space as two 1x widgets. (At CopperEgg, we refer to the 2x as a 'doublewide'.)

A complete widget hash is presented here for your convenience:

{% highlight sh %}
Widget Hash
  {
    "type"=>"metric_list",           # the type and style define which widget is used
    "style"=>"list",                 # this is a mult-metric widget
    "match"=>"tag",                  # this key-value pair allows selection of object by tag
    "label"=>"Cloud Portal Health",  # optionally user-defined
    "metric"=>["ce_probe_summary_v1","6","health"],      # here the metric to display is specified
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
 * assign the value 'object_id' to the 'match_param' key. The object_id my be a SYSTEM_ID, a PROBE_ID or a METRICGROUP_ID.

#### Multi-metric widgets
Widget type 'metric_list', style 'list'
This is a 1x widget that displays up to 7 single metrics, with both a current value and a small time-series sparkline. These are not intended for viewing from a distance.
The value of this style of widget lies in the visual presentation of a common metric from a number of sources.

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
As you can see in the above Widget Hash, there is a 'metric' key, with a value consisting of a three-element array:
  "metric"=>["ce_probe_summary_v1","6","health"]
The 3 array elements are [METRICGROUP_ID, METRICGROUP_INDEX, UNIT_STRING]
 * The METRICGROUP_ID is the unique identifier assigned by CopperEgg for a defined metric group.
 * The METRICGROUP_INDEX is the value of the 'position' key in the specified metric group.
 * The UNIT_STRING describes the units of this metric, string.


The Dashboard Hash
As you can see below, the dashboard hash is an object that contains a hash of widget hashes, along with some metadata.
A single-widget Dashboard hash is provided below, for easy reference:

{% highlight sh %}
Dashboard Hash
  {
    "id":80,                      # unique dashboard id assigned by CopperEgg
    "name":"SingleProbe",         # the display name of this dashboard, string
    "data":{                      # the widget data hash, containing two key-value pairs
      "widgets":{                 # a hash of widgets,
        "1":{                     # each hash has a unique, CopperEgg-provided numeric key
          "type":"metric",                                        #
          "style":"value",                                        #
          "label":"TestProbe",                                    # a widget hash,as defined above
          "metric":["ce_probe_summary_v1","1","connect_time"],    #
          "match":"select",                                       #
          "match_param":"4ff7e3682ca1fc0c72000038"                #
        }
      },
      "order":["1"]                                               # defines the order in which the widgets appear on this dashboard
    },
    "created_at":1354035004,      # time created, unix timestamp, UTC
    "updated_at":1354042044       # last time updated, unix timestamp, UTC
  }
{% endhighlight %}


Index
-----
List all defined Custom Metrics Custom Dashboards.

####Required parameters:
None.

####Optional parameters:
None.

CURL Command:
{% highlight sh %}
curl -u APIKEY:U https://api.copperegg.com/v2/revealmetrics/dashboards.json
{% endhighlight %}

CURL Response:

Response is a JSON array of Dashboard hashes. In this example, there is one dashboard defined, which displays 4 widgets.
{% highlight sh %}
[
  {
    "id":61,                                              # unique dashboard ID, assigned by CopperEgg
    "name":"Service Monitoring",                          # Dashboard name, string
    "data":{                                              # the data hash consists of two key-value pairs, widgets and order
      "widgets":{                                         # array of widgets
        "0":{                                               # widget id
          "type":"timeline",                                  # widget type
          "style":"values",                                   # widget style
          "match":"tag",                                      # what category to select on
          "label":"Cloud Portal Response Time (total)",       # Widget label
          "metric":["ce_probe_summary_v1","0","time"],        # metric: [METRIC_GROUP_ID, METRIC_INDEX, METRIC_LABEL]
          "match_param":"cloud"                               # which member of the category to select on
        },
        "1":{
          "type":"metric_list",
          "style":"list",
          "match":"tag",
          "label":"Cloud Portal Health",
          "metric":["ce_probe_summary_v1","6","health"],
          "match_param":"cloud"
        },
        "2":{
          "type":"timeline",
          "style":"values",
          "match":"tag",
          "label":"Social Sites Response Time (total)",
          "metric":["ce_probe_summary_v1","0","time"],
          "match_param":"social"
        },
        "3":{
          "type":"metric_list",
          "style":"list",
          "match":"tag",
          "label":"Social Sites Health",
          "metric":["ce_probe_summary_v1","6","health"],
          "match_param":"social"
        }
      },
      "order":["0","1","2","3"]                   # the order of the widgets on the screen |  0  1  2  |
    },                                            #                                        |  4  5  6  |
    "created_at":1353891562,                      # time created, unix timestamp, UTC
    "updated_at":1353938713                       # last time updated, unix timestamp, UTC
  }
]
{% endhighlight %}


Create Dashboard
------
Create a new Dashboard

####Required parameters:
* You must include a dashboard "name" string, and a data hash, including both a widget hash and an order hash.
* The widget hash must be one or more key-value pairs, where each key is a string-formatted number starting with "0"; each of these keys must have an associated widget hash value.
* Each widget hash must include 'type', 'style', 'match', 'match_param' and a 'metric' value array.

####Optional parameters:
* order array, for laying out the widgets
  if not included, CopperEgg will order them automatically.
* label
  if not included, a default label will be created. Be descriptive!!!


####Create Example; Create a new dashboard with a single widget. The dashboard will be named "My First Dash".
We'll also use a metric group named "ce_probe_summary_v1" which is a 'built-in' metric group. (You may have noticed this metric group in the Index example).


CURL Command:
{% highlight sh %}
curl -u APIKEY:U -H "Content-type: application/json" -XPOST https://api.copperegg.com/v2/revealmetrics/dashboards.json -d '{"name":"My New Dash","data":{"widgets":{"0":{"type":"metric","style":"value","match":"tag","metric":["ce_probe_summary_v1","6","health"],"match_param":"cloud"}},"order":["0"]}}'
{% endhighlight %}

CURL Response:
Response is a JSON-formatted Dashboard hash.

{% highlight sh %}
{
  "id":89,
  "name":"My New Dash",
  "data":{
    "widgets":{
      "0":{
        "type":"metric",
        "style":"value",
        "match":"select",
        "metric":["ce_probe_summary_v1","6","health"],
        "match_param":PROBE_ID
      }
    },
    "order":["0"]
  },
  "created_at":1354048053,
  "updated_at":1354048053
}
{% endhighlight %}

Update
------
Update an existing Dashboard and/or the widgets it displays.

####Required parameters
* Dashboard id, returned from an Index command or in response to the create command

####Optional parameters
 * change the Dashboard label
 * modify existing widgets
 * add new widgets


####Update Example: Add a widget to the dashboard created above.

CURL Command:
{% highlight sh %}
curl -u APIKEY:U -H "Content-type: application/json" -XPUT https://api.copperegg.com/v2/revealmetrics/dashboards/89.json -d '{"name":"My New Dash","data":{"widgets":{"0":{"type":"metric","style":"value","match":"tag","metric":["ce_probe_summary_v1","6","health"],"match_param":"cloud"},"1":{"type":"metric","style":"value","match":"tag","metric":["ce_probe_summary_v1","6","health"],"match_param":"onprem"}},"order":["0","1"]}}'
{% endhighlight %}

CURL Response:
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
        "match":"select",
        "metric":["ce_probe_summary_v1","6","health"],
        "match_param":PROBE_ID1
      },
      "1":{
        "type":"metric",
        "style":"value",
        "match":"tag",
        "metric":["ce_probe_summary_v1","6","health"],
        "match_param":PROBE_ID2
      }
    },
    "order":["0","1"]
  },
  "created_at":1354050492,
  "updated_at":1354050561
}
{% endhighlight %}


Remove
-------
Remove the specified Dashboard.

####Required parameters
* Dashboard id, as part of the path

####Optional parameters
None


CURL Command:
{% highlight sh %}
curl  -u APIKEY:U -XDELETE  https://api.copperegg.com/v2/revealmetrics/dashboards/DASHBOARD_ID.json
{% endhighlight %}

CURL Response:

Response is Status 200, empty JSON:

{% highlight javascript %}
{}
{% endhighlight %}




