---
layout: default
title: RevealUptime - Tags
---

Index
-----
List all defined RevealUptime tags.

CURL Command:
{% highlight sh %}
curl -u APIKEY:U https://api.copperegg.com/v2/revealuptime/tags.json
{% endhighlight %}

CURL Response:

Response is JSON with an array of all defined RevealUptime tags.

{% highlight javascript %}
[
  { "id":"dallas_group",
    "probe_ids":[
      "4fefc0b82ca1fc060d000403|atl",
      "4fefc0b82ca1fc060d000403|nrk",
      "4fefc0b82ca1fc060d000403|MT8twxayLJjGajVVLXYnEEbMNPHmJacq|"
    ]
  },
  { "id":"atlanta_group",
    "probe_ids":[
      "ac1f5ef85c1177ef97596f334f877370|en0|",
      "ac1f5ef85c1177ef97596f334f877370|",
      "ac1f5ef85c1177ef97596f334f877370|en1|",
      "ac1f5ef85c1177ef97596f334f877370|en2|",
      "ac1f5ef85c1177ef97596f334f877370|fw0|",
      "ac1f5ef85c1177ef97596f334f877370|/|",
      "ac1f5ef85c1177ef97596f334f877370|/Volumes/facter-1.6.10|",
      "ac1f5ef85c1177ef97596f334f877370|vmnet1|",
      "ac1f5ef85c1177ef97596f334f877370|disk0|",
      "ac1f5ef85c1177ef97596f334f877370|disk1|"
    ]
  }
]
{% endhighlight %}

In the example above, two tags are returned by the Index command; "dallas_group" and "atlanta_group". Note that each tag structure contains a singe "id", which is the Label for the tag, and an array of "probe_ids", which are unique for each probe defined in your system.


Show
----
Show in-depth information about a single RevealUptime tag.

Required Parameters: the tag of interest; in the example below, the tag is "atlanta_group".

CURL Command:
{% highlight sh %}
curl -u APIKEY:U https://api.copperegg.com/v2/revealuptime/tags/atlanta_group.json
{% endhighlight %}

CURL Response:

Response is JSON with an array of structures containing details of all probes associated with the specified tag:

{% highlight javascript %}
[
  {
    "attrs" : {
      "description" : "Hires probe",
      "destination" : "http://mywebsite.com",
      "frequency" : "15",
      "label" : "my_website_hires",
      "type" : "GET"
    },
    "created_at" : 1341782097,
    "health" : 0,
    "id" : null,
    "last_updated" : 1341782097,
    "published_rc_version" : "",
    "state" : 3,
    "tags" : [ "atlanta_group" ],
    "uuid" : null
  },
  {
    "attrs" : {
      "description" : "Lowres probe",
      "destination" : "https://mywebsite.com",
      "frequency" : "60",
      "label" : "my_website_lowres",
      "type" : "GET"
    },
    "created_at" : 1342482449,
    "health" : 0,
    "id" : null,
    "last_updated" : 1342482449,
    "published_rc_version" : "",
    "state" : 3,
    "tags" : [ "atlanta_group" ],
    "uuid" : null
  }
]
{% endhighlight %}

*** the details of these structures will be reviewed below.

Create
------
Add a new tag to one or more defined probed.

Required params:  

* a tag ( tags may contain a-z, A-Z, 0-9, - and _)  

* one or more probe_ids to which the tag will be applied  

* if specifying more than one probe_id, use a comma-separated list  

In the following example, a tag labelled "app_group" will be applied to two existing probes, with probe_ids of 4ff9f8512ca1fc338d00000e and 5004a884b0175d20c00000be.

CURL Command:
{% highlight sh %}
curl -u APIKEY:U -XPOST https://api.copperegg.com/v2/revealuptime/tags.json -d 'id=app_group&probe_ids=4ff9f8512ca1fc338d00000e,5004a884b0175d20c00000be'
{% endhighlight %}

CURL Response:

Response is Status 200, empty JSON:
{% highlight javascript %}
{

}
{% endhighlight %}


Destroy
-------
Remove a tag from a probe.

Required params:
* a tag
* a probe_id from which the tag will be removed

In the following example, a tag labelled "app_group" will be removed from the probe with probe_id 4ff9f8512ca1fc338d00000e.

CURL Command:
{% highlight sh %}
curl -s -XDELETE -u APIKEY:U https://api.copperegg.com/v2/revealuptime/tags/app_group/4ff9f8512ca1fc338d00000e.json
{% endhighlight %}

CURL Response:

Response is Status 200, empty JSON:

{% highlight javascript %}
{

}
{% endhighlight %}

