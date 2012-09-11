---
layout: default
title: RevealUptime - Probes
---

Overview
--------

Each of the API commands described here relate to the set of all probes that have been created at your site.    
  
Each probe is completely described by a Probe hash. The key-value pairs within this hash are described in detail in the Create section.  



Index
-----
List all defined RevealUptime probes.

CURL Command:  
{% highlight sh %}
curl -u APIKEY:U https://api.copperegg.com/v2/revealuptime/probes.json
{% endhighlight %}

CURL Response:  

Response is a JSON array of Probe hashes.

{% highlight javascript %}
[
  {
    "id" : "4ff9f8512ca1fc338d00000e",
    "alert_def_id" : "",
    "probe_desc" : "Hires probe",
    "probe_dest" : "http://mywebsite.com",
    "probe_data" : "",
    "checkcontents" : "",
    "contentmatch" : "",
    "frequency" : "15",
    "timeout" : 10000,
    "retries" : 1,
    "type" : "GET",
    "created_at" : 1341782097,
    "updated_at" : 1344385807
    "state" : "enabled",
    "tags" : [ "atlanta_group" ],
    "stations" : [ "atl" ]
  },
  { 
    "id" : "5004a81187517319f4000238",
    "alert_def_id" : "",
    "probe_desc" : "Lowres probe",
    "probe_dest" : "https://mywebsite.com",
    "probe_data" : "",
    "checkcontents" : "",
    "contentmatch" : "",
    "frequency" : "15",
    "timeout" : 10000,
    "retries" : 1,
    "type" : "GET",
    "created_at" : 1342482449,
    "updated_at" : 1344378245
    "state" : "enabled",
    "tags" : [ "atlanta_group" ],
    "stations" : [ "atl"],
  }
]
{% endhighlight %}


Show
----
Show in-depth information about a single RevealUptime probe.  

###Required parameters   
  
* You must include the PROBEID URL as part of the path.  
  
  
CURL Command:  
{% highlight sh %}
curl -u APIKEY:U https://api.copperegg.com/v2/revealuptime/probes/PROBEID.json
{% endhighlight %}

CURL Response:

Response is JSON with an single probe hash, containing all details of the specified probe.

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

####Required parameters:  
You must include a string describing the probe, the type of the probe, (GET or POST) and the URL to probe.
   
* probe_desc  
    Your short text description of the probe (string); e.g., "probe_desc":"MyWebsite".  

* type  
    A string that may be "GET" or "POST" (website alert); e.g., "type":"GET". 

* probe_dest   
    The URL to probe, formatted as a string; e.g., "probe_dest":"http://mywebsite.com"   


####Optional parameters:  

* check_contents  
    A string parameter used to enable / disable GET content-checking, and to specify the type of content check made. check_contents may have one of three values:      
  * null: no content check is made  
  * "match": true if the string in 'contentmatch' is found  
  * "notmatch": true if the string in 'contentmatch' is NOT found  

* contentmatch  
    The string used for comparison if 'check_contents' is not null.  

* frequency     
    Frequency of probing; if not specified, the default of 60 seconds will be used; may be set to 15 or 60 (number). NOTE: 'frequency' is a misnomer ... you are actually specifying the probe interval, or period in seconds. A 15 sec period means a probe frequency of 4 times/minute; 60 sec period means 1 probe/minute.  

* timeout       
    GET or POST request time-out, in milliseconds; if not specified, will default to 10000 ms, or 10 seconds.  

* retries
    Number of times to retry the operation; if not specified, defaults to 1.

* tags 
    Tags to apply to this probe; null: no tags will be applied.  

* stations
    Specify which stations will probe the destination URL; if not specified, all stations will probe.  
  

####Create Example 1: create a new probe using only the required parameters, to demonstrate defaults.  
  

CURL Command:  
{% highlight sh %}
curl -u APIKEY:U -XPOST https://api.copperegg.com/v2/revealuptime/probes.json -d 'probe_desc=MyWebsite&probe_dest=http://mywebsite.com&type=GET'
{% endhighlight %}
  

CURL Response:

Response is a JSON Probe hash:  

{% highlight javascript %}
{
  "id":"50203ddf35d58d034500000f",
  "alert_def_id":"",
  "probe_desc":"MyWebsite",
  "probe_dest":"http:/mywebsite.com",
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
  
  
####Create Example 2: create a new probe monitored every 15 seconds from London and Tokyo.  
  

CURL Command:
{% highlight sh %}
curl -u APIKEY:U -XPOST https://api.copperegg.com/v2/revealuptime/probes.json -d 'probe_desc=MyWebsite&probe_dest=http://mywebsite.com&type=GET&frequency=15&stations=lon,tok'
{% endhighlight %}
  

CURL Response:  
  
Response is a JSON a Probe hash:  

{% highlight javascript %}
{
  "id":"50203ddf35d58d034500000f",
  "alert_def_id":"",
  "probe_desc":"MyWebsite",
  "probe_dest":"http:/mywebsite.com",
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

####Required parameters    
    
* same as described for :create  
  
  
####Optional parameters   
  
* same as described for :create  



####Update Example: change checking frequency of the probe created above to every 60 seconds.  (where PROBEID = 50203ddf35d58d034500000f)

CURL Command:
{% highlight sh %}
curl -u APIKEY:U -XPUT https://api.copperegg.com/v2/revealuptime/probes/PROBEID.json  -d 'probe_desc=MyWebsite&probe_dest=http://mywebsite.com&type=GET&frequency=60'
{% endhighlight %}

CURL Response:

Response is JSON with the updated probe structure:

{% highlight javascript %}
{
  "id":"50203ddf35d58d034500000f",
  "alert_def_id":"",
  "probe_desc":"MyWebsite",
  "probe_dest":"http:/mywebsite.com",
  "probe_data":"",
  "checkcontents":"",
  "contentmatch":"",
  "frequency":60,
  "timeout":10000,
  "retries":1,
  "type":"GET",
  "created_at":1344290271,
  "updated_at":1344293871,
  "state":"enabled",
  "tags":[],
  "stations":["lon","tok"]
}
{% endhighlight %}


Remove
-------
Remove the specified probe.

Required params:  ... probe_id as part of the path

####Remove Example: remove the probe created above. (where PROBEID = 50203ddf35d58d034500000f)

CURL Command:
{% highlight sh %}
curl  -u APIKEY:U -XDELETE  https://api.copperegg.com/v2/revealuptime/probes/PROBEID.json
{% endhighlight %}

CURL Response:

Response is Status 200, empty JSON:

{% highlight javascript %}
removed
{% endhighlight %}

