---
layout: default
title: RevealUptime - Probes
---

Index
-----
List all defined RevealUptime probes.

CURL Command:
{% highlight sh %}
curl -u myapikey:U https://api.copperegg.com/v2/revealuptime/probes.json
{% endhighlight %}

CURL Response:

Response is JSON with an array of probe structures for defined RevealUptime probes.

{% highlight javascript %}
[
  { "alert_def_id" : "",
    "checkcontents" : "",
    "contentmatch" : "",
    "created_at" : 1341782097,
    "frequency" : "15",
    "id" : "4ff9f8512ca1fc338d00000e",
    "probe_data" : "",
    "probe_desc" : "Hires probe",
    "probe_dest" : "http://mywebsite.com",
    "retries" : 1,
    "state" : "enabled",
    "stations" : [ "atl" ],
    "tags" : [ "atlanta_group" ],
    "timeout" : 10000,
    "type" : "GET",
    "updated_at" : 1344385807
  },
  { "alert_def_id" : "",
    "checkcontents" : "",
    "contentmatch" : "",
    "created_at" : 1342482449,
    "frequency" : "15",
    "id" : "5004a81187517319f4000238",
    "probe_data" : "",
    "probe_desc" : "Lowres probe",
    "probe_dest" : "https://mywebsite.com",
    "retries" : 1,
    "state" : "enabled",
    "stations" : [ "atl"],
    "tags" : [ "atlanta_group" ],
    "timeout" : 10000,
    "type" : "GET",
    "updated_at" : 1344378245
  }
]
{% endhighlight %}


Definition of fields in the probe structure:

{% highlight sh %}
"id":"4ff9f8512ca1fc338d00000e",      // unique identifier for this probe
"alert_def_id":"",                    //
"probe_desc":"Hires probe",           // Label in 'Create a Probe' dialogue
"probe_dest":"http://mywebsite.com",  // URL in the 'Create a Probe' dialogues
"probe_data":"",                      //
"checkcontents":"",                   // used for GET with content check
"contentmatch":"",                    // used for GET with content check
"frequency":"15",                     // probe frequency, in secs. default is 60
"timeout":10000,                      // timeout in ms, default is 10000
"retries":1,                          // default 1
"type":"GET",                         // GET or POST probe
"created_at":1341782097,              // timestamp of probe creation
"updated_at":1344385807,              // timestamp last updated
"state":"enabled",                    // enabled, disabled, deleted
"tags":["atlanta_group"],             // array of associated tags
"stations":["atl"]                    // array of probe stations
{% endhighlight %}



Show
----
Show in-depth information about a single RevealUptime probe.

Required parameters: ... probe id as part of the path

CURL Command:
{% highlight sh %}
curl -u myapikey:U https://api.copperegg.com/v2/revealuptime/probes/50200c55d9106a232e000041.json
{% endhighlight %}

CURL Response:

Response is JSON with an single probe structure, containing all details of the specified probe.

{% highlight javascript %}
{
  "id":"4ff9f8512ca1fc338d00000e",
  "alert_def_id":"",
  "probe_desc":"Hires probe"",
  "probe_dest":"http://mywebsite.com",
  "probe_data":"",
  "checkcontents":"",
  "contentmatch":"",
  "frequency":"15",
  "timeout":10000,
  "retries":1,
  "type":"GET",
  "created_at":1341782097,
  "updated_at":1344385807,
  "state":"deleted",
  "tags":["atlanta_group"],
  "stations":["atl"]
}
{% endhighlight %}


Create
------
Create a new RevealUptime probe.

Required parameters:
* probe_desc    a short text identifier of your choice
* probe_dest    the URL to probe
* type          GET or POST probe

Optional parameters:
* check_contents
*               null: no content check is made
*               'match': true if the string in 'contentmatch' is found
*               'notmatch': true if the string in 'contentmatch' is NOT found
* contentmatch  the string used if 'check_contents' is not null
* frequency     frequency of probing; null: 60 seconds; can be 15 or 60
* timeout       GET or POST request timout, in milliseconds
*               null: will default to 10000 ms (10 seconds)
* retries       times to retry the opertion; null: defaults to 1
* tags          tags to apply to this probe; null: no tags will be applied
* stations      stations to probe the specified URL; null: all stations


Create Example 1: create a new probe using only the required parameters, to demonstrate defaults.

CURL Command:
{% highlight sh %}
curl -u myapikey:U -XPOST https://api.copperegg.com/v2/revealuptime/probes.json -d 'probe_desc=newsite&probe_dest=http://mynewsite.com&type=GET'
{% endhighlight %}

CURL Response:

Response is JSON with a probe structure:

{% highlight javascript %}
{
  "id":"50203ddf35d58d034500000f",
  "alert_def_id":"",
  "probe_desc":"newsite",
  "probe_dest":"http:/mynewsite.com",
  "probe_data":"",
  "checkcontents":"",
  "contentmatch":"",
  "frequency":60,
  "timeout":10000,
  "retries":1,
  "type":"GET",
  "created_at":1344290271,
  "updated_at":1344290271,
  "state":"enabled",
  "tags":[],
  "stations":["dal","tok","nrk","fre","atl","lon"]
}
{% endhighlight %}


Create Example 2: create a new probe monitored every 15 seconds from London and Tokyo.

CURL Command:
{% highlight sh %}
curl -u myapikey:U -XPOST https://api.copperegg.com/v2/revealuptime/probes.json -d 'probe_desc=newsite&probe_dest=http://mynewsite.com&type=GET&frequency=15&stations=lon,tok'
{% endhighlight %}

CURL Response:

Response is JSON with a new probe structure:

{% highlight javascript %}
{
  "id":"50203ddf35d58d034500000f",
  "alert_def_id":"",
  "probe_desc":"newsite",
  "probe_dest":"http:/mynewsite.com",
  "probe_data":"",
  "checkcontents":"",
  "contentmatch":"",
  "frequency":15,
  "timeout":10000,
  "retries":1,
  "type":"GET",
  "created_at":1344290271,
  "updated_at":1344290271,
  "state":"enabled",
  "tags":[],
  "stations":["lon","tok"]
}
{% endhighlight %}


Update
------
Update an existing RevealUptime probe.

Required parameters:
* probe_desc  ... a short text identifier of your choice
* probe_dest  ... the URL to probe
* type  ......... GET or POST probe
* probe_id  ..... as part of the path

Optional parameters:  ... same as described for :create


Example: change checking frequency of the probe created above to every 60 seconds.

CURL Command:
{% highlight sh %}
curl -u myapikey:U -XPUT https://api.copperegg.com/v2/revealuptime/probes/50203ddf35d58d034500000f.json  -d 'probe_desc=newsite&probe_dest=http://mynewsite.com&type=GET&frequency=60'
{% endhighlight %}

CURL Response:

Response is JSON with the updated probe structure:

{% highlight javascript %}
{
  "id":"50203ddf35d58d034500000f",
  "alert_def_id":"",
  "probe_desc":"newsite",
  "probe_dest":"http:/mynewsite.com",
  "probe_data":"",
  "checkcontents":"",
  "contentmatch":"",
  "frequency":60,
  "timeout":10000,
  "retries":1,
  "type":"GET",
  "created_at":1344290271,
  "updated_at":1344290271,
  "state":"enabled",
  "tags":[],
  "stations":["lon","tok"]
}
{% endhighlight %}


Destroy
-------
Remove the specified probe.

Required params:  ... probe_id as part of the path

Example: remove the probe created above.

CURL Command:
{% highlight sh %}
curl  -u myapikey:U -XDELETE  https://api.copperegg.com/v2/revealuptime/probes/50203ddf35d58d034500000f.json
{% endhighlight %}

CURL Response:

Response is Status 200, empty JSON:

{% highlight javascript %}
{

}
{% endhighlight %}



