---
layout: default
title: Probes - Tags
---

## Overview

Each of the API commands described here relate to listing, creating, editing and deleting tags that have been associated with Probes at your site.

-----

## Index

Retrieve an array of all Probe Tag Hashes.


#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U https://api.copperegg.com/v2/revealuptime/tags.json

curl -s https://<APIKEY>:U@api.copperegg.com/v2/revealuptime/tags.json
{% endhighlight %}

#### CURL Response:

Response is a JSON-encoded array of all Probe Tag Hashes.

{% highlight sh %}
[
  { "id":"dallas_group",                         # PROBE_TAG ... is the tag itself. AKA, tag 'id'
    "probe_ids":[
      "4fefc0b82ca1fc060d000403|atl",            # PROBE_ID's
      "4fefc0b82ca1fc060d000403|nrk",
      "4fefc0b82ca1fc060d000403|MT8twxayLJjGajVVLXYnEEbMNPHmJacq|"
    ]
  },
  { "id":"atlanta_group",                        # PROBE_TAG ... is the tag itself. AKA, tag 'id'
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

In the example above, two Probe Tag Hashes are returned by the Index command; "dallas_group" and "atlanta_group".
Note that each tag structure contains an 'id', which is the tag itself, and an array of "probe_ids", one for each probe to which the tag is attached.

----

## Show

Retrieve details about each Probe with the specified tag.


#### Required Parameters:
PROBE_TAG as part of the path.

#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U https://api.copperegg.com/v2/revealuptime/tags/<PROBE_TAG>.json

curl -s https://<APIKEY>:U@api.copperegg.com/v2/revealuptime/tags/<PROBE_TAG>.json
{% endhighlight %}

#### CURL Response:

Response is a JSON-encoded array of Probe Hashes, each containing details and status of a probe associated with the specified tag:

{% highlight sh %}
{
  "id":"tag",
  "probes":[
            {
              "id":"0NoKw1SMD7Sg3jF2JTkwXtNQS",
              "probe_desc":"Test Site",
              "probe_dest":"http://www.mywebsite.com",
              "probe_data":null,
              "checkcontents":"",
              "contentmatch":null,
              "frequency":300,
              "timeout":10000,
              "retries":1,
              "type":"GET",
              "created_at":1480932562,
              "updated_at":1480932628,
              "state":"enabled",
              "tags":["tag"],
              "stations":["atl","dal","nrk","nva"],
              "headers":{},
              "idv":"0NoKw1SMD7Sg3jF2JTkwXtNQS|W5j4cNM72ih6O8kE4vC4DeptBRsFSdOt|",
              "auth_user":"",
              "auth_pass":"",
              "name_server":""
            },
            {
              "id":"0NoKw1SMD7Sg3jF2GFkwXtNQS",
              "probe_desc":"Test Site1",
              "probe_dest":"http://www.mywebsite.com",
              "probe_data":null,
              "checkcontents":"",
              "contentmatch":null,
              "frequency":300,
              "timeout":10000,
              "retries":1,
              "type":"GET",
              "created_at":1480932562,
              "updated_at":1480932628,
              "state":"enabled",
              "tags":["tag"],
              "stations":["atl","dal","nrk","nva"],
              "headers":{},
              "idv":"0NoKw1SMD7Sg3jF2GFkwXtNQS|W5j4cNM72ih6O8kE4vC4DeptBRsFSdOt|",
              "auth_user":"",
              "auth_pass":"",
              "name_server":""
            }
           ]
}
{% endhighlight %}

------

## Create

Add a new tag to one or more defined probes.

#### Required params:

id
: a text string specifying the tag. Tags may contain a-z, A-Z, 0-9, - and \_

probe_ids
: one or more probes to which the tag will be applied. if specifying more than one probe_id, use a comma-separated list.

In the following example, a tag labeled "app_group" will be applied to two existing probes.

#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U -XPOST https://api.copperegg.com/v2/revealuptime/tags.json -d 'id=<TAG>&probe_ids=<PROBE_ID>,<PROBE_ID>'

curl -XPOST -s https://<APIKEY>:U@api.copperegg.com/v2/revealuptime/tags.json -d 'id=<TAG>&probe_ids=<PROBE_ID>,<PROBE_ID>'
{% endhighlight %}

#### CURL Response:

Response is Status 200, empty JSON:
{% highlight sh %}
{}
{% endhighlight %}

-------

Delete

Delete a tag from a probe.

Required params:
* PROBE_TAG
* PROBE_ID as part of the path

#### CURL Command, and variations:
{% highlight sh %}
curl -XDELETE -su <APIKEY>:U https://api.copperegg.com/v2/revealuptime/tags/<PROBE_TAG>/<PROBE_ID>.json

curl -XDELETE -s https://<APIKEY>:U@api.copperegg.com/v2/revealuptime/tags/<PROBE_TAG>/<PROBE_ID>.json
{% endhighlight %}

#### CURL Response:

Response is Status 200, empty JSON:

{% highlight sh %}
{}
{% endhighlight %}

