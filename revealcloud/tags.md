---
layout: default
title: Systems - Tags
---

## Index

Retrieve all Systems tags.

#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U https://api.copperegg.com/v2/revealcloud/tags.json

curl -s https://<APIKEY>:U@api.copperegg.com/v2/revealcloud/tags.json
{% endhighlight %}

#### CURL Response:

Response is a JSON-formatted array of System Tag Hashes, one hash per System tag.

{% highlight sh %}
[
 { "id" : "MyMac",
   "uuids" : [ "ac1f5ef85c1177ef97596f334f877370" ]
 },
 { "id" : "newtag6",
   "uuids" : [ "fa1b86b5fabde626f85eb04fb67711b0" ]
 },
 { "id" : "puppetclient",
   "uuids" : [ "adfd8f357459b57c8deb461ee269b1ce" ]
 },
 { "id" : "tag100",
   "uuids" : [ "b18d39d9b343ac07315a7fd5612866e7" ]
 },
 { "id" : "tag5",
   "uuids" : [ "f7e5b061cae389bb45b63cccd1a1abd6" ]
 },
 { "id" : "tag6",
   "uuids" : [ "fa1b86b5fabde626f85eb04fb67711b0" ]
 },
 { "id" : "winserver",
   "uuids" : [ "124f4ae912ae9f5e718d2a5ab4fbaed5" ]
 }
]
{% endhighlight %}

Note that each System Tag Hash contains a single TAG_ID (tag "id"), which is the tag itself, and an array of "uuids", one for each monitored system with the tag of reference attached.


----
## Show


Retrieve in-depth information about the Systems tagged with the specified SYSTEM_TAG.

#### Required Parameters:
SYSTEM_TAG as part of the path.


### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U https://api.copperegg.com/v2/revealcloud/tags/<SYSTEM_TAG>.json

curl -s https://<APIKEY>:U@api.copperegg.com/v2/revealcloud/tags/<SYSTEM_TAG>.json
{% endhighlight %}


#### CURL Response:

Response is JSON-encoded array of hashes containing details of all systems associated with the SYSTEM_TAG.

{% highlight sh %}
[
 {"state":3,"hidden":true,"last_updated":1355434010,"created_at":1355434010,"tags":["winserver"],"attrs":{},"meta":{},"id":null,"uuid":null,"health":0},
 {"state":3,"hidden":true,"last_updated":1345825675,"created_at":1345825675,"tags":["winserver"],"attrs":{},"meta":{},"id":null,"uuid":null,"health":0},
 {"state":3,"hidden":true,"last_updated":1345825675,"created_at":1345825675,"tags":["winserver"],"attrs":{},"meta":{},"id":null,"uuid":null,"health":0},
 {"state":3,"hidden":true,"last_updated":1363620812,"created_at":1345825667,"tags":["winserver"],"attrs":{"rc_os":"windows","rc_version":"3.0.36.0","version_checked_at":"2013-03-18 10:33:32 -0500","CSDVersion":"Service Pack 1","uts_release":"6.1.7601.65536","uuid_origin":"","uts_machine":"x86_64","uts_sysname":"Windows","uts_version":"Microsoft Windows NT 6.1.7601 Service Pack 1","uuid_type":"search","Operating_System":"Microsoft Windows 7 Professional ","uts_nodename":"WIN-1M8N94S69C8","rc_args":"\"C:\\Program Files (x86)\\CopperEgg\\RevealCloud\\revealWindows.exe\"","hostname":"WIN-1M8N94S69C8","rc_health_timestamp":"1363620774","rc_health_index":"1.0","rc_health_state":"1","rc_health_info":"[1, 1, 1, 1, 1, 1, 1]","ce_bench_cpuindex":"284.234","ce_bench_cpucount":"2","ce_bench_cpustream":"0.000","rc_level":"2"},"meta":{"rc_health_index":"0.82","rc_health_state":"2","rc_health_info":"[1, 1, 1, 1, 1, 1, 1, 3, 1, 1, 3]","rc_version":"v3.3-92-g0814c8d","rc_os":"windows","rc_health_timestamp":"1481207525","version_checked_at":"2016-12-08 08:31:41 -0600"},"id":null,"uuid":null,"health":0},
 {"state":3,"hidden":true,"last_updated":1355420334,"created_at":1355420334,"tags":["winserver"],"attrs":{},"meta":{},"id":null,"uuid":null,"health":0}
]
{% endhighlight %}

Note: the results above indicate that the tag 'winserver' is associated with 5 systems, all hidden.

------
## Create

Add a new System Tag to one or more monitored Systems.


#### Required params:

* SYSTEM_TAG as part of the path

* one or more uuids to which the tag will be applied

* if specifying more than one uuid, use a comma-separated list


### Example:
In the following example, SYSTEM_TAG "systemtest" will be applied to an existing system.


#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U -XPOST https://api.copperegg.com/v2/revealcloud/tags.json -d 'id=systemtest&uuids=<UUID>'

curl -s -XPOST https://<APIKEY>:U@api.copperegg.com/v2/revealcloud/tags.json -d 'id=systemtest&uuids=<UUID>'

curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/revealcloud/tags.json -d '{"uuids":<UUID>,"id":"systemtest"}'
{% endhighlight %}

#### CURL Response:

Response is Status 200, empty JSON:

{% highlight sh %}
{}
{% endhighlight %}


-------
## Delete

Remove a tag from one system.


#### Required params:
* SYSTEM_TAG as part of the path

* UUID of the system from which the tag will be removed, as part of the path


#### CURL Command, and variations:
{% highlight sh %}
curl -XDELETE -su <APIKEY>:U https://api.copperegg.com/v2/revealcloud/tags/SYSTEM_TAG/UUID.json

curl -XDELETE -s https://<APIKEY>:U@api.copperegg.com/v2/revealcloud/tags/SYSTEM_TAG/UUID.json
{% endhighlight %}

#### CURL Response:

Response is Status 200, empty JSON:

{% highlight sh %}
{}
{% endhighlight %}
