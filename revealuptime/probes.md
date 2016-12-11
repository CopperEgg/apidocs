---
layout: default
title:  Probes
---

## Overview

'Probe' refers to a periodic test of an internet-connected service. Today the supported Probe types include TCP port connections, ICMP, DNS, HTTP GET/POST and HTTPS GET/POST, REST, SSL.
'Station' refers to a location from which the tests are being generated.

Each of the API commands described here relate to retrieving, creating, editing and deleting one or more of your Probes.
Each probe is completely described by a Probe Hash, and each has a unique id referred to herein as a PROBE_ID.


### The Probe Hash
An example JSON-encoded Probe Hash is shown below:

{% highlight sh %}
{
  "id":"4ff6010f2ca1fc1bd30000fd",                # the PROBE_ID
  "probe_desc":"Some website of interest",        # a user-defined text string describing the probe
  "probe_dest":"http://websiteofinterest.com",    # the url or IP address of the endpoint to test
  "probe_data":"",                                # a text string used when checking content
  "checkcontents":"",                             # indicates whether to examine the retrieved contents
  "contentmatch":"",                              # if checking contents, the string to compare with
  "frequency":15,                                 # number of seconds between each test
  "timeout":10000,                                # abort after this number of milliseconds, if test hasn't completed
  "retries":1,                                    # retry attempts, if connection attempt fails
  "type":"GET",                                   # may be GET, PUT, TCP or ICMP
  "created_at":1341522191,                        # time and date when probe was created (unix timestamp)
  "updated_at":1356980017,                        # time and date of last update (unix timestamp)
  "state":"enabled",                              # current operating state of this probe, enabled or disabled (paused)
  "tags":[                                        # array of tags associated with this probe
  ],
  "stations":[                                    # array of  locations from which to send the tests
    "dal"
  ],
  "headers":{},                                   # HTTP(s) header field
  "idv":"0NoKw1SMD7Sg3jF2JTkwXtNQS|",             # internal field
  "auth_user":"",                                 # Authentication username for REST probe
  "auth_pass":"",                                 # Authentication password for REST probe
  "name_server":""                                # Name server for resolving probe
}
{% endhighlight %}

----
## Index

Retrieve an array of all of your Probe Hashes.

#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U https://api.copperegg.com/v2/revealuptime/probes.json

curl -s https://<APIKEY>:U@api.copperegg.com/v2/revealuptime/probes.json
{% endhighlight %}


#### CURL Response:
Response is a JSON-encoded array of Probe Hashes.

{% highlight ruby %}
[
  {
    "id":"4ff6010f2ca1fc1bd30000fd",
    "probe_desc":"Some website of interest",
    "probe_dest":"http://websiteofinterest.com",
    "probe_data":"",
    "checkcontents":"",
    "contentmatch":"",
    "frequency":15,
    "timeout":10000,
    "retries":1,
    "type":"GET",
    "created_at":1341522191,
    "updated_at":1356980017,
    "state":"enabled",
    "tags":[],
    "stations":[
      "dal"
    ],
    "headers":{},
    "idv":"0NoKw1SMD7Sg3jF2JTkwXtNQS|W5j4cNM72ih6O8kE4vC4DeptBRsFSdOt|",
    "auth_user":"",
    "auth_pass":"",
    "name_server":""
  },
  {
    "id":"4ff6015ac0212a273200002d",
    "probe_desc":"Another website of interest",
    "probe_dest":"http:///otherwebsiteofinterest.com",
    "probe_data":"",
    "checkcontents":"",
    "contentmatch":"",
    "frequency":60,
    "timeout":10000,
    "retries":1,
    "type":"GET",
    "created_at":1341522266,
    "updated_at":1356980021,
    "state":"enabled",
    "tags":[],
    "stations":[
      "dal",
      "fre",
      "nrk",
      "atl"
    ],
    "headers":{},
    "idv":"0NoKw1SMD7Sg3jF2JTkwXtNQS|W5j4cNM74ih6O8kE4vC4DeptBRsFSdOt|",
    "auth_user":"",
    "auth_pass":"",
    "name_server":""
  },
]
{% endhighlight %}

----
## Show

Retrieve a single Probe Hash, given its PROBE_ID.

### Required parameters

PROBE_ID as part of the path.


#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U https://api.copperegg.com/v2/revealuptime/probes/<PROBE_ID>.json

curl -s https://<APIKEY>:U@api.copperegg.com/v2/revealuptime/probes/<PROBE_ID>.json
{% endhighlight %}


#### CURL Response:

Response is a single JSON-encoded Probe Hash.

{% highlight ruby %}
{
  "id":"4ff6015ac0212a273200002d",
  "probe_desc":"Another website of interest",
  "probe_dest":"http:///otherwebsiteofinterest.com",
  "probe_data":"",
  "checkcontents":"",
  "contentmatch":"",
  "frequency":60,
  "timeout":10000,
  "retries":1,
  "type":"GET",
  "created_at":1341522266,
  "updated_at":1356980021,
  "state":"enabled",
  "tags":[],
  "stations":[
    "dal",
    "fre",
    "nrk",
    "atl"
  ],
  "headers":{},
  "idv":"0NoKw1SMD7Sg3jF2JTkwXtNQS|W5j4cNM72ih6O8kE4vC4DeptBRsFSdOt|",
  "auth_user":"",
  "auth_pass":"",
  "name_server":""
}
{% endhighlight %}

------
## Create

Create a new probe.


#### Required parameters:

probe_desc
: Your short text description of the probe (string); e.g., "probe_desc":"MyWebsite".
Any characters allowed.

type
: A string that may be GET, POST, PUT, DELETE, SSH, ICMP, DNS, TCP or SSL.

probe_dest
: The URL or IP address to probe, formatted as a string; e.g., "probe_dest":"http://mywebsite.com"


#### Optional parameters:

check_contents
: A string parameter used to enable / disable GET content-checking, and to specify the type of content check made.
check_contents may have one of three values:

 * null: no content check is made
 * "match": true if the string in 'contentmatch' is found
 * "notmatch": true if the string in 'contentmatch' is NOT found

contentmatch
: The string used for comparison if 'check_contents' is not null.

frequency
: Frequency of probing; if not specified, the default of 60 seconds will be used; may be set to 15, 60 or 300.
NOTE: 'frequency' is a misnomer ... you are actually specifying the time between tests in seconds.

timeout
: request time-out, in milliseconds; if not specified, will default to 10000 ms, or 10 seconds.

retries
: Number of times to retry the operation; if not specified, defaults to 1.

tags
: Tags to apply to this probe; null: no tags will be applied.

stations
: Specify which stations will probe the destination URL; if not specified, all stations will probe.

username
: Specify username for basic authentication of REST probes (GET, POST, PUT, DELETE).

password
: Specify password for basic authentication of REST probes. (Used in GET, POST, PUT, DELETE probes)

name_server
: Specify name server to resolve probe destination specified. (Used in DNS probes)

### Create Example 1: create a new probe using only the required parameters, to demonstrate defaults.


#### CURL Command, and variations:

{% highlight sh %}
curl -su <APIKEY>:U -XPOST https://api.copperegg.com/v2/revealuptime/probes.json -d 'probe_desc=MyWebsite&probe_dest=http://mywebsite.com&type=GET'

curl -s -XPOST https://<APIKEY>:U@api.copperegg.com/v2/revealuptime/probes.json -d 'probe_desc=MyWebsite&probe_dest=http://mywebsite.com&type=GET'

curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/revealuptime/probes.json -d '{"probe_desc":"MyNewWebsite","probe_dest":"http://mywebsite.com","type":"GET"}'
{% endhighlight %}


#### CURL Response:
Response is the newly-created JSON-encoded Probe Hash:

{% highlight ruby %}
{
  "id":"sn3tiu84teve2nZzXhq2rq8ud",
  "probe_desc":"MyNewWebsite",
  "probe_dest":"http://mywebsite.com",
  "probe_data":null,
  "checkcontents":"",
  "contentmatch":null,
  "frequency":60,
  "timeout":10000,
  "retries":1,
  "type":"GET",
  "created_at":1364926232,
  "updated_at":1364926232,
  "state":"enabled",
  "tags":[

  ],
  "stations":[
    "dal",
    "tok",
    "nrk",
    "fre",
    "atl",
    "lon"
  ],
  "headers":{},
  "idv":"0NoKw1SMD7Sg3jF2JTkwXtNQS|W5j4cNM72ih6O8kE4vC4DeptBRsFSdOt|",
  "auth_user":"",
  "auth_pass":"",
  "name_server":""
}
{% endhighlight %}



### Create Example 2: create a new probe which will be monitored every 15 seconds from London and Tokyo.


#### CURL Command, and variations:

{% highlight sh %}
curl -su <APIKEY>:U -XPOST https://api.copperegg.com/v2/revealuptime/probes.json -d 'probe_desc=MyWebsite&probe_dest=http://mywebsite.com&type=GET&frequency=15&stations=lon,tok'

curl -s -XPOST https://<APIKEY>:U@api.copperegg.com/v2/revealuptime/probes.json -d 'probe_desc=MyWebsite&probe_dest=http://mywebsite.com&type=GET&frequency=15&stations=lon,tok'

curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/revealuptime/probes.json -d '{"probe_desc":"MyNewWebsite","probe_dest":"http://mywebsite.com","type":"GET","frequency":15,"stations":["lon","tok"]}'
{% endhighlight %}


#### CURL Response:

Response is the newly-created JSON-encoded Probe Hash:

{% highlight ruby %}
{
  "id":"dYI0NFrcNC2Szy2pnTzx01wtu",
  "probe_desc":"MyWebsite",
  "probe_dest":"http://mywebsite.com",
  "probe_data":null,
  "checkcontents":"",
  "contentmatch":null,
  "frequency":15,
  "timeout":10000,
  "retries":1,
  "type":"GET",
  "created_at":1364932752,
  "updated_at":1364932752,
  "state":"enabled",
  "tags":[

  ],
  "stations":[
    "lon",
    "tok"
  ],
  "headers":{},
  "idv":"0NoKw1SMD7Sg3jF2JTkwXtNQS|W5j4cNM72ih6O8kE4vC4DeptBRsFSdOt|",
  "auth_user":"",
  "auth_pass":"",
  "name_server":""
}
{% endhighlight %}

------
## Update

Update an existing Probe.

#### Required parameters

Same as described for Create


#### Optional parameters

Same as described for Create



#### Update Example: change the frequency of the probe created above to every 300 seconds.

#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U -XPUT https://api.copperegg.com/v2/revealuptime/probes/<PROBE_ID>.json  -d 'frequency=300'

curl -s -XPUT https://<APIKEY>:U@api.copperegg.com/v2/revealuptime/probes/<PROBE_ID>.json  -d 'frequency=300'

curl -s -XPUT -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/revealuptime/probes/<PROBE_ID>.json  -d '{"frequency":300}'
{% endhighlight %}

#### CURL Response:

Response is the newly-updated JSON-encoded Probe Hash:

{% highlight ruby %}
{
  "id":"fpWTlmwIfVdlhJFGAsCMTZ3az",
  "probe_desc":"MyNewWebsite",
  "probe_dest":"http://mywebsite.com",
  "probe_data":null,
  "checkcontents":"",
  "contentmatch":null,
  "frequency":300,
  "timeout":10000,
  "retries":1,
  "type":"GET",
  "created_at":1364933182,
  "updated_at":1364933183,
  "state":"enabled",
  "tags":[

  ],
  "stations":[
    "lon",
    "tok"
  ],
  "headers":{},
  "idv":"0NoKw1SMD7Sg3jF2JTkwXtNQS|W5j4cNM72ih6O8kE4vC4DeptBRsFSdOt|",
  "auth_user":"",
  "auth_pass":"",
  "name_server":""
}
{% endhighlight %}

-------
## Delete

Delete the specified Probe Hash.

#### Required params:
PROBE_ID as part of the path


### Delete Example: delete the probe created above.

#### CURL Command, and variations:

{% highlight sh %}
curl -su <APIKEY>:U -XDELETE https://api.copperegg.com/v2/revealuptime/probes/<PROBE_ID>.json

curl -s -XDELETE https://<APIKEY>:U@api.copperegg.com/v2/revealuptime/probes/<PROBE_ID>.json
{% endhighlight %}

#### CURL Response:

Response is Status 200, empty JSON:

{% highlight ruby %}
{}
{% endhighlight %}

