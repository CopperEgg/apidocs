---
layout: default
title: RUM - Real User Monitoring
---

## Overview

There is a single API call for retrieving RUM data samples.

Using curl:

{% highlight sh %}

curl -s https://<API key>:U@api.copperegg.com/v2/revealapp/samples.json \
-H "Content-Type: application/json" -d '<query parameters>'

{% endhighlight %}

The API key is a unique key that identifies each customer.
You can obtain it by clicking the Settings tab while logged on to Uptime Cloud Monitor UI.
It is presented at the bottom of the screen under “User API Access”.

## Query Parameters

Parameters are specified in JSON format as follows:

{% highlight sh %}
{"starttime": <start_time>, "endtime": <end_time>, "group": 0,
  "queries": [{<query 1>},{<query 2>}, {<query n>}]}
{% endhighlight %}

start_time and end_time should be specified as an integer UNIX timestamp (seconds since epoch).
When omitted, the last 15 minutes will be queried.
When multiple queries are specified, all will share the same timeframe.

## Required Parameters

group
: must be specified as 0 (zero).

queries
: at least one query must be specified.

## Query format

{% highlight sh %}
{"idvs": ["<instrumentation key 1>|", "<instrumentation key n>|"], "keys": ["<key1>", "<keyn>"]}
{% endhighlight %}

idvs allows specifying an array of instrumentation keys. At least one instrumentation key must be specified.
To obtain Web App’s instrumentation key:


1. Click “Details” button on the desired Web App in Web App Dashboard view
2. Click the “Edit” link to open the Web App Edit screen
3. In the third line of JavaScript code look for:
{% highlight sh %}
BACON.id = '<instrumentation key>';
{% endhighlight %}


<b>Attention:</b> You must concatenate “|” character at the end of every instrumentation key.

## Keys
The key is the type of results that will be returned. Multiple keys can be specified. At least one is mandatory. Result type (key) should one of:

* <b>user_times</b> - returns Web App level counters per interval
* <b>top_urls</b> - returns a list of top requests per interval
  Contains both Ajax and Page requests
* <b>top_locations</b> - returns a list of top countries per interval. Also contains states for US only
* <b>top_browsers</b> - returns a list of top browsers per interval

## Sample request: last 15 minutes Web App counters for one Web App

{% highlight sh %}
curl -s https://<APIKEY>:U@api.copperegg.com/v2/revealapp/samples.json \
-H "Content-Type: application/json" \
-d '{"group": 0, "queries": [{"idvs": ["<instrument key>|"], "keys": ["user_times"]}]}'
{% endhighlight %}

##### The response has the following format:

{% highlight sh %}
[[{
  "idv":"XdS31haJMPZJvDhY|",       # instrument key
  "hid":0,                         # hidden? true == 1, false == 0
  "a":                             # baked attributes
    {"p":1387125305},              # most recent update time (ts)
  "_ts":1387073040,                # baseline timestamp, for offet 0
  "_bs":60,                        # actual interval size in seconds. See sample_size
  "user_times":{                   # response for the 'user_times' key
    "0":[                          # timestamp - offset from _ts
      1,                           # requests count
      0,                           # avg web server time in milliseconds
      2882,                        # avg transfer time in milliseconds
      126,                         # avg rendering time in milliseconds
      0,                           # avg req. send time in milliseconds
      1.0,                         # avg apdex score
      1.0,                         # avg requests per minute
      3008,                        # total response time (sum of all requests)
      3008,                        # max (worst) response time
      1.0,                         # total apdex
      60,                          # interval size in seconds
      3008                         # avg response time in milliseconds
    ],
    "60":[                         # timestamp - offset in seconds from _ts
       1,
     ...
    ],
   ...
}
}]]
{% endhighlight %}

<b>Note:</b> Twelve counters are returned per interval.
When charting an overtime graph, averages are sufficient.

To calculate average response time of the entire timeframe, sum the total response time of all intervals and then divide by the sum of requests counts of all intervals.

##### If “top_urls” key was specified, the response for the key has the following format:

{% highlight sh %}
"top_urls":{                               # response for the 'top_urls' key
   "0":{                                   # timestamp - offset from _ts
      "L2d1aS9HZXREYXRhU2VydmxldA==":[     # request URL, encrypted in base64 encoding
        {"c":11,"t":3709,"h":890,"l":47},  # response time in ms (count, total, hi, and lo)
        {"c":11,"t":2500,"h":700,"l":20},  # server time in ms (count, total, hi, and lo)
        {"c":11,"t": 209,"h":121,"l":10},  # transfer time in ms (count, total, hi, and lo)
        {"c":11,"t": 750,"h":307,"l":15},  # rendering time in ms (count, total, hi, and lo)
        {"c":11,"t": 150,"h": 40,"l": 0},  # req. send time in ms (count, total, hi, and lo)
        {"c":11,"t":  10,"h":1,"l":0.5},   # Apdex score (count, total, hi, and lo)
        {"title":"Online Shopping",        # page title
         "domain":"http://my.site.com",    # protocol and domain
         "ajax":"T"                        # "T" for Ajax requests or "F" for Page requests
        }],
     "L2dwL3ZpZGVvL3dhdGNobGlzdC9hamF4L2hvdmVyYnViYmxlLmh0bWw=":[  # next request same interval
      …
     ]
   }
   "60":                                 # Timestamp - offset from _ts
      ...
}
{% endhighlight %}

You can use atob() in JavaScript to decode request URL from base64 encoding.
To calculate Apdex score, divide its total by its count.

To calculate avg response time, divide its total by its count.

<b>Note:</b> Each interval reports its own top requests. Each request might be reported in multiple intervals on the same timeframe. To calculate average Apdex score on the entire timeframe for specific request, sum all its totals and then divide by sum of all its counts.

##### If “top_locations” key was specified, the response for the key has the following format:

{% highlight sh %}

"top_locations":{                          # response for the 'top_locations' key
   "0":{                                   # Timestamp - offset from _ts
      "376":[                              # country code. See http://en.wikipedia.org/wiki/ISO_3166-1
        {"c":11,"t":3709,"h":890,"l":47},  # response time in ms (count, total, hi, and lo)
        {"c":11,"t":2500,"h":700,"l":20},  # server time in ms (count, total, hi, and lo)
        {"c":11,"t": 209,"h":121,"l":10},  # transfer time in ms (count, total, hi, and lo)
        {"c":11,"t": 750,"h":307,"l":15},  # rendering time in ms (count, total, hi, and lo)
        {"c":11,"t": 150,"h": 40,"l": 0},  # req. send time in ms (count, total, hi, and lo)
        {"c":11,"t":  10,"h":1,"l":0.5}],  # Apdex score (count, total, hi, and lo)
     "840.Colorado":[ … ],                 # If the country code is USA (840), the state name is concatenated
   }
   "60": ...                               # Next interval - offset in seconds from _ts
}
{% endhighlight %}

##### If “top_browsers” key was specified, the response for the key has the following format:

 {% highlight sh %}

 "top_browsers":{                          # response for the 'top_browsers' key
   "0":{                                   # Timestamp - offset from _ts
      "Chrome":[                           # Browser type.
        {"c":11,"t":3709,"h":890,"l":47},  # Response time in ms (count, total, hi, and lo)
        {"c":11,"t":2500,"h":700,"l":20},  # server time in ms (count, total, hi, and lo)
        {"c":11,"t": 209,"h":121,"l":10},  # transfer time in ms (count, total, hi, and lo)
        {"c":11,"t": 750,"h":307,"l":15},  # rendering time in ms (count, total, hi, and lo)
        {"c":11,"t": 150,"h": 40,"l": 0},  # req. send time in ms (count, total, hi, and lo)
        {"c":11,"t":  10,"h":1,"l":0.5}],  # Apdex score (count, total, hi, and lo)
     "Internet Explorer 10":[ … ],         # next browser same interval
     "Mobile":[ … ],                       # aggregation of all mobile browsers (same interval)
     "Desktop":[ … ],                      # aggregation of all desktop browsers (same interval)
   }
   "60": ...                               # Next interval - offset in seconds from _ts
}

{% endhighlight %}
