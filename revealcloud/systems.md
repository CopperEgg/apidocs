---
layout: default
title: RevealCloud - Systems
---


Overview
--------

Each of the API commands described here relate to the set of all systems that have been created at your site.

Each system is completely described by a System hash, which is essentially the metadata about your systems. It includes hostname, label, tags, and all other attributes on the system object. The UUID is the unique identifier you will use on future calls to retrieve samples (metrics) for that system.

Index
-----
List all defined RevealCloud systems.  
  
CURL Command:  
{% highlight sh %}
curl -u APIKEY:U https://api.copperegg.com//v2/revealcloud/systems.json 
{% endhighlight %}
  
CURL Response:   
  
Response is a JSON array of System hashes.  
  
{% highlight javascript %}
[
  {
    "a": {                        # baked attributes
      "p": 1345146730,          # last_updated (timestamp)
      "c": 1341108555,          # created_at (timestamp)
      "h": "1.0",               # health index 0..1
      "s": "1",                 # state 0=unknown, 1=ok, 2=warn, 3=critical
      "o": "m",                 # os  l=linux,m=mac,w=windows,f=freebsd
      "ov": "12.0.0",           # os version
      "rv": "v3-43-geefad79",   # revealcloud collector version
      "pv": "v3-43-geefad79",
      "n": "MacBook-Pro",       # hostname
      "t"=>[                    # tags applied to this system
        "jambalaya", 
        "alligator"
      ],        
      "us": "[",
      "bs": "1",
      "ls": ",",
      "cs": " ",
      "ms": "1",
      "fs": ","
    },
    "uuid": "ac1f5ef85c1177ef97596f334f877370",   # system unique identifier
    "hid": 0                      # is hidden? does not exist if false, 1=true
  }
]
{% endhighlight %}
  
  
Show  
----
Show in-depth information about a single system.  
  
###Required parameters  
  
* At least one system uuid. In the following example, the UUID spcified is ac1f5ef85c1177ef97596f334f877370. (see above)

CURL Command:  
{% highlight sh %}
curl -u APIKEY:U https://api.copperegg.com/v2/revealcloud/systems.json?uuids=UUID  
{% endhighlight %}

CURL Response:

Response is JSON with an single System hash, containing all details of the specified system. The result will be the same as above.

 











