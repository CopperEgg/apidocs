---
layout: default
title: Probes- Samples
---


## Overview

There is a single API call for retrieving Probe data samples.


### Required Parameters:

ids
: At least one PROBE_ID must be specified. Up to 20 PROBE_IDs can be specified in each request. Multiple ids can be formatted as either a comma separated string or an array represented by multiple HTTP parameters named “ids\[ \]”


### Optional Parameters:

starttime
: An integer unix timestamp (seconds since epoch) representing the beginning of your query timeframe.

endtime
: An integer unix timestamp (seconds since epoch) representing the end of your query timeframe.

keys
: A list of keys you want to include (see 'Probe Sample Keys' below).  This can either be a comma separated string or an array represented by multiple HTTP parameters named "keys\[ \]".  Default: "l_l, l_s, l_u, l_h"

sample_size
: Override the default sample size that is determined by the starttime/endtime range. This will only work if you specify a sample_size larger than that automatically calculated for the time range. If you specify a smaller sample_size, the default sample_size will be used.

**Note:** If starttime and endtime both are not provided, the last 5 minutes of samples are returned. Also, if the frequency of probe is greater than the duration specified for samples, the request will not return any samples.

### Probe Sample Keys
{% highlight sh %}
key name           valid combinations
latency               l, l_l, s_l
latency_percent       lp, l_lp
status_code           s, l_s, s_s
uptime                u, l_u, s_u
health                h, l_h, s_h
state_string          ss, l_ss
{% endhighlight %}
**Note:**
* the prefacing ‘l_’ means ‘latest’; return most recent sample data.
* the prefacing ‘s_’ means 'separated'; return data from individual components



### Probe Sample Abbreviations
{% highlight sh %}
term               abbreviation
timestamp             '_ts'
actual sample size    '_bs'
attributes            'a'
probe URL             'c'
probe name or label   'n'
health                'h'
probe_id              'id'
uptime                'u'
status codes          's'
{% endhighlight %}

----
#### Example 1
----
Obtain samples from one probe, specifying only the PROBE_ID.

#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U "https://api.copperegg.com/v2/revealuptime/samples.json?ids=<PROBE_ID>"

curl -s  "https://<APIKEY>:U@api.copperegg.com/v2/revealuptime/samples.json?ids=<PROBE_ID>"
{% endhighlight %}

#### CURL Response:

Response is a JSON-encoded array with a single Probe Sample Hash:

{% highlight sh %}
[
  {
    "a":{"n":"site1","c":"GET http://site1.com/"},
    "id":"4ff8da3a2ca1fc10a20001e7",
    "_ts":1365135660,
    "_bs":5,
    "l":{"0":[143,143,0,286],"60":[152,153,0,305],"120":[146,150,0,296],"180":[158,162,0,320]},
    "s":{"0":{"301":2},"60":{"301":3},"120":{"301":3},"180":{"301":4}},
    "h":{"0":100,"60":100,"120":100,"180":100},
    "u":{"0":100,"60":100,"120":100,"180":100}
  }
]
{% endhighlight %}


----
#### Example 2
----

Obtain samples from two probes, specifying sample_size of 60. Default keys.

#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U "https://api.copperegg.com/v2/revealuptime/samples.json?sample_size=60&ids=<PROBE_ID>,<PROBE_ID>"

curl -s "https://<APIKEY>:U@api.copperegg.com/v2/revealuptime/samples.json?sample_size=60&ids=<PROBE_ID>,<PROBE_ID>"
{% endhighlight %}


#### CURL Response:

Response is a JSON-encoded array of Probe Sample Hashes, in this case, with 60 seconds data:

{% highlight sh %}
[
  {
    "a":{"n":"site1","c":"GET http://site1.com/"},
    "id":"4ff7e3122ca1fc02a00002f7",
    "_ts":1365136440,
    "_bs":60,
    "l":{"0":[45,389,4,438],"60":[53,381,5,439],"120":[29,876,6,911]},
    "s":{"0":{"200":18},"60":{"200":21},"120":{"200":18}},
    "h":{"0":100,"60":100,"120":98},
    "u":{"0":100,"60":100,"120":100}
  },
  {
    "a":{"n":"site2","c":"GET http://site2.com/"},
    "id":"4ff8da3a2ca1fc10a20001e7",
    "_ts":1365136440,
    "_bs":60,
    "l":{"0":[160,161,0,321],"60":[160,152,0,312],"120":[155,161,0,316]},
    "s":{"0":{"301":4},"60":{"301":3},"120":{"301":4}},
    "h":{"0":100,"60":100,"120":100},
    "u":{"0":100,"60":100,"120":100}
  }
]
{% endhighlight %}


----
#### Example 3
----

Obtain samples from a single probe, specifying starttime, endtime, and sample_size of 60 seconds. Default keys.

#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U "https://api.copperegg.com/v2/revealuptime/samples.json?starttime=1344195713&endtime=1344195893&sample_size=60&ids=<PROBE_ID>"

curl -s "https://<APIKEY>:U@api.copperegg.com/v2/revealuptime/samples.json?starttime=1344195713&endtime=1344195893&sample_size=60&ids=<PROBE_ID>"
{% endhighlight %}

#### CURL Response:

Response is a JSON-encoded array with a single Probe Sample Hash:

{% highlight sh %}
[
  {
    "a":{"n":"site1","c":"GET http://site1.com/"},
    "id":"4ff8da3a2ca1fc10a20001e7",
    "_ts":1344195713,
    "_bs":5,
    "l":{"0":[143,143,0,286],"60":[152,153,0,305],"120":[146,150,0,296],"180":[158,162,0,320]},
    "s":{"0":{"301":2},"60":{"301":3},"120":{"301":3},"180":{"301":4}},
    "h":{"0":100,"60":100,"120":100,"180":100},
    "u":{"0":100,"60":100,"120":100,"180":100}
  }
]
{% endhighlight %}


----
#### Example 4
----

Obtain samples from one probe, specifying sample_size of 60, and the keys l, lp, l_s, u, l_h and l_ss.

#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U "https://api.copperegg.com/v2/revealuptime/samples.json?sample_size=60&ids=<PROBE_ID>&keys=l,lp,l_s,u,l_h,l_ss"

curl -s "https://<APIKEY>:U@api.copperegg.com/v2/revealuptime/samples.json?sample_size=60&ids=<PROBE_ID>&keys=l,lp,l_s,u,l_h,l_ss"
{% endhighlight %}

#### CURL Response:

Response is a JSON-encoded array with a single Probe Sample Hash:

{% highlight sh %}
[
  {
    "a":{"n":"Hires probe","c":"GET http://mywebsite.com"},
    "id":"4ff9f8512ca1fc338d00000e",
    "_ts":1344451560,
    "_bs":60,
    "l":{"0":[ 30,36,0,66 ],"60":[ 40,47,0,87 ],"120":[ 32,53,1,86 ],"180":[ 34,35,1,70 ]},
    "lp":{"0":[ 0.4545, 1.0,1.0 ],"60":[ 0.4598,1.0,1.0 ],"120":[ 0.3721,0.9884,1.0 ],"180":[ 0.4857,0.9857,1.0 ]},
    "l_s":{ "200":28 },
    "l_h":100,
    "u":{"0":100,"60":100, "120":100, "180":100},
    "l_ss":{ "s":28 }
  }
]
{% endhighlight %}

Note: Latency percent arrays contain only three values: connect, time for the first byte, and transfer.


----
#### Example 5
----

Obtain all station data for one probe, specifying sample_size of 60, and the keys s_l, s_s, s_u, and s_h.


#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U "https://api.copperegg.com/v2/revealuptime/samples.json?sample_size=60&ids=<PROBE_ID>&keys=s_l,s_s,s_u,s_h"

curl -s "https://<APIKEY>:U@api.copperegg.com/v2/revealuptime/samples.json?sample_size=60&ids=<PROBE_ID>&keys=s_l,s_s,s_u,s_h"
{% endhighlight %}

#### CURL Response:

Response is a JSON-encoded array with a single Probe Sample Hash:

{% highlight sh %}
[
  {
    "a":{"n":"site1 home", "c":"GET http://site1.net"},
    "id":"4ff9f8512ca1fc338d00000e",
    "_ts":1344453360,
    "_bs":60,
    "s_l":{
      "atl":{"0":[21,47,1,69],"60":[21,23,0,44],"120":[21,24,1,46],"180":[62,23,1,86]},
      "dal":{"0":[39,3,1,43],"60":[4,3,1,8],"120":[3,3,0,6],"180":[11,3,1,15]}
    },
    "s_s":{
      "atl":{"0":{"200":3},"60":{"200":4},"120":{"200":3},"180":{"200":3}},
      "dal":{"0":{"200":3},"60":{"200":4},"120":{"200":3},"180":{"200":4}}
    },
    "s_h":{
      "atl":{"0":100,"60":100,"120":100,"180":100},
      "dal":{"0":100,"60":100,"120":100,"180":100}
    },
    "s_u":{
      "atl":{"0":100,"60":100,"120":100,"180":100},
      "dal":{"0":100,"60":100,"120":100,"180":100}
    }
  }
]
{% endhighlight %}

