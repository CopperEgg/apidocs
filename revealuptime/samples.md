---
layout: default
title: RevealUptime - Samples
---


Overview
--------
The API call for obtaining samples has a fair amount of detail, unlike many of the other CopperEgg API calls. The calling parameters and abbreviations that appear in the data structures are documented at the outset. The ideal way to get started is to scan the early sections, and then dig into the examples. Refer back to the parameters, keys and abbreviations when necessary, once you have gotten a feel for using the API.
  
  
  
###Parameters:  
* ids (required) => At least one probe id must be specified. Up to 20 probe ids can be specified in each request. Multiple ids can be formatted as either a comma separated string, or an array represented by multiple HTTP parameters named “ids\[ \]”  

* starttime =>  An integer unix timestamp (seconds since epoch) representing the beginning of your query timeframe. (NOTE: if starttime and endtime are not both provided, the last 5 minutes of samples are returned)  

* endtime => An integer unix timestamp (seconds since epoch) representing the end of your query timeframe. (NOTE: if starttime and endtime are not both provided, the last 5 minutes of samples are returned)  

* keys => A list of keys you want to include (see "key reference").  This can either be a comma separated string, or an array represented by multiple HTTP parameters named "keys\[ \]".  Default: "l_l, l_s, l_u, l_h"  

* sample_size => Override the default sample size that is determined by the
starttime/endtime range. This will only work if you specify a sample_size larger than what is automatically calculated for the time range. If you specify a smaller sample_size, the default sample_size will be used. Valid sample size values are 15 and 60.  
  
  
      
###RevealUptime Keys
{% highlight sh %}
key name           valid combinations
latency               l, l_l, s_l
latency_percent       lp, l_lp
status_code           s, l_s, s_s
uptime                u, l_u, s_u
health                h, l_h, s_h
state_string          ss, l_ss
{% endhighlight %}
Note:
* the prefacing ‘l_’ means ‘latest’; return most recent sample data.
* the prefacing ‘s_’ means 'stations'; return all individual station data.
  
  
    
###RevealUptime Abbreviations
{% highlight sh %}
term               abbreviation
timestamp             '_ts'
attributes            'a'
probe URL             'c'
probe name or label   'n'
health                'h'
probe_id              'id'
uptime                'u'
status codes          's'  
{% endhighlight %}  
    
    
    
    
Example 1
---------  
Obtain samples from one probe, specifying only the probe_id.

CURL Command:
{% highlight sh %}
curl -u APIKEY:U "https://api.copperegg.com/v2/revealuptime/samples.json?ids 4ff9f8512ca1fc338d00000e"
{% endhighlight %}

CURL Response:  

Response is JSON with an array of probe sample data:  

{% highlight javascript %}
[
  {
    "_ts" : 1344195720,
    "a" : {
      "c" : "GET http://mywebsite.com",
      "n" : "Hires probe"
    },
    "h" : {
      "0" : 100,
      "105" : 100,
      "135" : 100,
      "15" : 100,
      "165" : 100,
      "60" : 100,
      "75" : 100
    },
    "id" : "4ff9f8512ca1fc338d00000e",
    "l" : {
      "0" : [ 5,3,1, 9 ],
      "105" : [ 23,23,1,47 ],
      "135" : [ 48,50,0,98 ],
      "15" : [ 44,45,1,90 ],
      "165" : [ 2,2,1,5 ],
      "60" : [ 1,2,1,4 ],
      "75" : [ 43, 122,1,166 ]
    },
    "s" : {
      "0" : { "200" : 1 },
      "105" : { "200" : 1 },
      "135" : { "200" : 1 },
      "15" : { "200" : 3 },
      "165" : { "200" : 1 },
      "60" : { "200" : 1 },
      "75" : { "200" : 1 }
    },
    "u" : {
      "0" : 100,
      "105" : 100,
      "135" : 100,
      "15" : 100,
      "165" : 100,
      "60" : 100,
      "75" : 100
    }
  }
]
{% endhighlight %}
    
  
  
Example 2  
---------
Obtain samples from two probes, ( with PROBEID's of 4ff9f8512ca1fc338d00000e and 5004a81187517319f4000238) specifying sample_size of 60. Default keys.  

CURL Command:
{% highlight sh %}
curl -u APIKEY:U "https://api.copperegg.com/v2/revealuptime/samples.json?sample_size=60&ids=4ff9f8512ca1fc338d00000e,5004a81187517319f4000238"
{% endhighlight %}

CURL Response:

Response is JSON with a 2-element array of probe sample data, in this case, with 60 second data:

{% highlight javascript %}
[
  {
    "a":{
      "n":"Hires probe    ",
      "c":"GET http://mywebsite.com      "
    },
    "id":"4ff9f8512ca1fc338d00000e",
    "_ts":1344449340,
    "l":{
      "0":[ 59,40,6,105 ],
      "60":[ 34,61,1,96 ],
      "120":[ 41,53,0,94 ],
      "180":[ 40,44,0,84 ]
    },
    "s":{
      "0":{ "200":35 },
      "60":{ "200":33 },
      "120":{ "200":24 },
      "180":{ "200":33 }
    },
    "h":{
      "0":100,
      "60":100,
      "120":100,
      "180":100
    },
    "u":{
      "0":100,
      "60":100,
      "120":100,
      "180":100
    }
  },
  {
    "a":{
      "n":"Lores probe",
      "c":"GET http://mywebsite.com"
    },
    "id":"5004a81187517319f4000238",
    "_ts":1344449340,
    "l":{
      "0":[ 59,40,6,105 ],
      "60":[ 34,61,1,96 ],
      "120":[ 41,53,0,94 ],
      "180":[ 40,44,0,84 ]
    },
    "s":{
      "0":{ "200":35 },
      "60":{ "200":33 },
      "120":{ "200":24 },
      "180":{ "200":33 }
    },
    "h":{
      "0":100,
      "60":100,
      "120":100,
      "180":100
    },
    "u":{
      "0":100,
      "60":100,
      "120":100,
      "180":100
    }
  }
]
{% endhighlight %}
    
  
  
Example 3
---------
Obtain samples from a single probe (with PROBEID 4ff9f8512ca1fc338d00000e), specifying starttime, endtime and sample_size of 60 seconds. Default keys.

CURL Command:
{% highlight sh %}
curl -u APIKEY:U "https://api.copperegg.com/v2/revealuptime/samples.json?starttime=1344195713&endtime=1344195893&sample_size=60&ids=4ff9f8512ca1fc338d00000e"
{% endhighlight %}

CURL Response:

Response is JSON with an array of probe sample data:

{% highlight javascript %}
[
  {
    "a":{
      "n":"Hires probe",
      "c":"GET http://mywebsite.com"
    },
    "id":"4ff9f8512ca1fc338d00000e",
    "_ts":1344195600,
    "l":{
      "0":[ 40,43,0,83 ],
      "60":[ 24,54,1,79 ],
      "120":[ 34,35,1,70 ],
      "180":[ 22,49,1,72 ],
      "240":[ 25,26,0,51 ],
      "300":[ 44,114,1,159 ]
    },
    "s":{
      "0":{ "200":5 },
      "60":{ "200":2 },
      "120":{ "200":4 },
      "180":{ "200":3 },
      "240":{ "200":2 },
      "300":{ "200":1 }
    },
    "h":{
      "0":100,
      "60":100,
      "120":100,
      "180":100,
      "240":100,
      "300":100
    },
    "u":{
      "0":100,
      "60":100,
      "120":100,
      "180":100,
      "240":100,
      "300":100
    }
  }
]
{% endhighlight %}

  
  
  
Example 4
---------
Obtain samples from one probe (with PROBEID 4ff9f8512ca1fc338d00000e), specifying sample_size of 60. Default keys.

CURL Command:
{% highlight sh %}
curl -u APIKEY:U "https://api.copperegg.com/v2/revealuptime/samples.json?sample_size=60&ids=4ff9f8512ca1fc338d00000e"
{% endhighlight %}

CURL Response:

Response is JSON with an array of probe sample data:

{% highlight javascript %}
[
  {
    "a":{
      "n":"Hires probe",
      "c":"GET http://mywebsite.com"
    },
    "id":"4ff9f8512ca1fc338d00000e",
    "_ts":1344449340,
    "l":{
      "0":[ 59,40,6,105 ],
      "60":[ 34,61,1,96 ],
      "120":[ 41,53,0,94 ],
      "180":[ 40,44,0,84 ]
    },
    "s":{
      "0":{ "200":35 },
      "60":{ "200":33 },
      "120":{ "200":24 },
      "180":{ "200":33 }
    },
    "h":{
      "0":100,
      "60":100,
      "120":100,
      "180":100
    },
    "u":{
      "0":100,
      "60":100,
      "120":100,
      "180":100
    }
  }
]
{% endhighlight %}
  
  
  
Example 5
---------
Obtain samples from one probe, (with PROBEID 4ff9f8512ca1fc338d00000e), specifying sample_size of 60, and the keys l, lp, l_s, u, l_h and l_ss.

CURL Command:
{% highlight sh %}
curl -u APIKEY:U "https://api.copperegg.com/v2/revealuptime/samples.json?sample_size=60&ids=4ff9f8512ca1fc338d00000e&keys=l,lp,l_s,u,l_h,l_ss"
{% endhighlight %}

CURL Response:

Response is JSON with an array of probe sample data:

{% highlight javascript %}
[
  {
    "a":{
      "n":"Hires probe",
      "c":"GET http://mywebsite.com"
    },
    "id":"4ff9f8512ca1fc338d00000e",
    "_ts":1344451560,
    "l":{
      "0":[ 30,36,0,66 ],
      "60":[ 40,47,0,87 ],
      "120":[ 32,53,1,86 ],
      "180":[ 34,35,1,70 ]
    },
    "lp":{
      "0":[ 0.4545, 1.0,1.0 ],
      "60":[ 0.4598,1.0,1.0 ],
      "120":[ 0.3721,0.9884,1.0 ],
      "180":[ 0.4857,0.9857,1.0 ]
    },
    "l_s":{ "200":28 },
    "l_h":100,
    "u":{
      "0":100,
      "60":100,
      "120":100,
      "180":100
    },
    "l_ss":{ "s":28 }
  }
]
{% endhighlight %}

Note: Latency percent arrays contain only three values, connect, time to first byte, and transfer.
  
  
  
Example 6
---------
Obtain all station data from one probe (with PROBEID 4ff9f8512ca1fc338d00000e), specifying sample_size of 60, and the keys s_l, s_s, s_u and s_h.


CURL Command:
{% highlight sh %}
curl -u APIKEY:U "https://api.copperegg.com/v2/revealuptime/samples.json?sample_size=60&ids=4ff9f8512ca1fc338d00000e&keys=s_l,s_s,s_u,s_h"
{% endhighlight %}

CURL Response:

Response is JSON with an array of probe sample data:

{% highlight javascript %}
[
  {
    "a":{
      "n":"CuEgg home",
      "c":"GET http://copperegg.com"
    },
    "id":"4ff9f8512ca1fc338d00000e",
    "_ts":1344453360,
    "s_l":{
      "atl":{
        "0":[21,47,1,69],
        "60":[21,23,0,44],
        "120":[21,24,1,46],
        "180":[62,23,1,86]
      },
      "dal":{
        "0":[39,3,1,43],
        "60":[4,3,1,8],
        "120":[3,3,0,6],
        "180":[11,3,1,15]
      }
    },
    "s_s":{
      "atl":{
        "0":{"200":3},
        "60":{"200":4},
        "120":{"200":3},
        "180":{"200":3}
      },
      "dal":{
        "0":{"200":3},
        "60":{"200":4},
        "120":{"200":3},
        "180":{"200":4}
      }
    },
    "s_h":{
      "atl":{
        "0":100,
        "60":100,
        "120":100,
        "180":100
      },
      "dal":{
        "0":100,
        "60":100,
        "120":100,
        "180":100
      }
    },
    "s_u":{
      "atl":{
        "0":100,
        "60":100,
        "120":100,
        "180":100
      },
      "dal":{
        "0":100,
        "60":100,
        "120":100,
        "180":100
      }
    }
  }
]
{% endhighlight %}

