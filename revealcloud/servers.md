---
layout: default
title: Systems
---

## Overview

Each of the API commands described here relate to retrieving, hiding and deleting one or more Systems being monitored at your site.
Each system is completely described by a System Hash, and each has a unique id referred to herein as a UUID.


### The System Hash

An example JSON-encoded System Hash is shown below:

{% highlight sh %}
[
  {
    "a":{                       # baked attributes
      "p":1364939147,           # last_updated (unix timestamp, UTC)
      "c":1341108555,           # created_at (unix timestamp, UTC)
      "h":1.0,                  # health index 0..1
      "s":1,                    # state 0=unknown, 1=ok, 2=warn, 3=critical
      "n":"IP_192-168-0-10",    # hostname
      "l":"Database-1",         # label, if defined
      "t":["prod"],             # tags applied to this system
      "o":"m",                  # os  l=linux,m=mac,w=windows,f=freebsd
      "ov":"12.3.0",            # os version
      "rv":"v3.1-12-g9e3cc44",  # revealcloud collector version
      "cl":"3",                 # collector level (internal use)
      "us":1,                   # uptime status
      "bs":1,                   # blocked status
      "ls":1,                   # load status
      "cs":1,                   # cpu status
      "ms":1,                   # memory status
      "fs":1                    # filesystems status
    },
    "uuid":"ac1f5ef85c1177ef97596f334f877370",   # system unique identifier; UUID
    "hid":0                                      # is hidden? 0 = false, 1 = true
  }
]
{% endhighlight %}

-----

## Index

Retrieve an array of System Hashes for all monitored systems at a site.

#### Optional parameters:

show_hidden
: set to show_hidden=1 to include hidden systems
*NOTE:*  show_hidden defaults to 0, meaning hidden systems are not returned.

#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U https://api.copperegg.com/v2/revealcloud/systems.json

curl -s https://<APIKEY>:U@api.copperegg.com/v2/revealcloud/systems.json

curl -s https://<APIKEY>:U@api.copperegg.com/v2/revealcloud/systems.json?show_hidden=1
{% endhighlight %}

#### CURL Response:

Response is a JSON-encoded array of System Hashes.
For example:
{% highlight sh %}
[
  {
    "a":{                       # baked attributes
      "p":1364939147,           # last_updated (timestamp)
      "c":1341108555,           # created_at (timestamp)
      "h":1.0,                  # health index 0..1
      "s":1,                    # state 0=unknown, 1=ok, 2=warn, 3=critical
      "n":"MacBookPro",         # hostname
      "t":[                     # tags applied to this system
        "MyMac"
      ],
      "o":"m",                  # os  l=linux,m=mac,w=windows,f=freebsd
      "ov":"12.3.0",            # os version
      "rv":"v3.1-12-g9e3cc44",  # revealcloud collector version
      "cl":"3",
      "us":1,
      "bs":1,
      "ls":1,
      "cs":1,
      "ms":1,
      "fs":1
    },
    "uuid":"ac1f5ef85c1177ef97596f334f877370",   # system unique identifier
    "hid":0                     # is hidden? 0 = false, 1 = true
  },
  {
    "a":{
      "p":1364235385,
      "c":1362145671,
      "h":1.0,
      "s":1,
      "n":"domU-12-31-38-04-B6-B7",
      "l":"centos6_3",          # label
      "t":[
        "corporate-website"
      ],
      "o":"l",
      "ov":"2.6.32-279.22.1.el6.i686",
      "rv":"v3.1-13-g9b4d0de",
      "cl":"3",
      "us":1,
      "bs":1,
      "ls":1,
      "cs":1,
      "ms":1,
      "fs":1
    },
    "uuid":"29a28c82d8119fec2024d63ddf913512",
    "hid":0
  }
]
{% endhighlight %}


-------

## Hide

Hide the specified system.

#### Required params:
UUID as part of the path


### Hide Example:


#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U -XPOST  https://api.copperegg.com/v2/revealcloud/uuids/<UUID>/hide.json

curl -s -XPOST https://<APIKEY>:U@api.copperegg.com/v2/revealcloud/uuids/<UUID>/hide.json
{% endhighlight %}

#### CURL Response:

Response is Status 200, "hidden"

{% highlight sh %}
hidden
{% endhighlight %}

-------

## Delete

Delete the specified System Hash.
NOTE: in the UI, a system DELETE is referred to as 'Remove'

#### Required params:
UUID as part of the path


### Delete Example: delete a System Hash.


#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U -XDELETE  https://api.copperegg.com/v2/revealcloud/uuids/<UUID>.json

curl -s -XDELETE  https://<APIKEY>:U@api.copperegg.com/v2/revealcloud/uuids/<UUID>.json
{% endhighlight %}

#### CURL Response:

Response is Status 200, "removed"

{% highlight sh %}
removed
{% endhighlight %}

