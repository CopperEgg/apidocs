---
layout: default
title: RevealEngine - Alerts
---

Questions and Issues
--------------------

###1. Create: You can create an alert definition with one parameter: the defn_desc string. 
* The new alert definition comes up ENABLED, but does not have a valid Comparison.
* The UI prevents this when creating a new alert definition.
* Assuming this is an oversight; this doc will state that a valid comparison is required.

Creating an alert definition with one parameter, {"defn_desc":"hicpu"}:

CURL Command:
{% highlight sh %}
curl -u pxAJ7BSmPXXl3k9W:U -H "Content-Type: application/json" -XPOST -d '{"defn_desc":"hicpu"}' https://api.copperegg.com/v2/alerts/definitions.json | json_reformat
{% endhighlight %}

CURL Response:
{% highlight javascript %}
{
}
{% endhighlight %}

The following alert definition structure is returned from :index:

{% highlight javascript %}
{
  "alert_duration" : 60,              // 10 minutes
  "auto_annotate" : null,             // disabled
  "auto_clear_issues" : null,         // disabled
  "comp_desc1" : "",
  "comp_desc2" : "",
  "comp_func" : "",
  "comp_val1" : [  ],
  "comp_val2" : [  ],
  "defn_desc" : "hicpu"               // the alert defn_desc passed in
  "id" : "50250a885d9f4f6b4f000029",  // unique alert def identifier
  "match" : {  },                     // match on anything
  "notify" : {  },                    // all notifications disabled
  "notify_on_clear" : null,           // disabled
  "state" : "enabled",                // enabled by default upon create
  "type" : "ce_revealcloud"
}
{% endhighlight %}

###2. Create:  There is a disconnect between the UI and the data. 
Specifically the notify : email[] field. Create a new alert definition as described below,
and you will see that the UI shows the default email address; the data returned by index
or show has a null email field. 

To reproduce:

CURL Command:
{% highlight sh %}
curl -u pxAJ7BSmPXXl3k9W:U -H "Content-Type: application/json" -XPOST -d '{"defn_desc":"himem","comp_func":">=","comp_desc1":"Active Memory","auto_clear_issues":true,"notify_on_clear":true,"auto_annotate":false,"comp_val1":["ce_rcsummary_v1","used_pcent"],"comp_val2":[0.85],"comp_desc2":"85%","alert_duration":60,"type":"ce_revealcloud"}' https://api.copperegg.com/v2/alerts/definitions.json | json_reformat
{% endhighlight %}

CURL Response:
{% highlight javascript %}
{
}
{% endhighlight %}

The following alert definition structure is returned from :index or :status:
{% highlight javascript %}
{
  "alert_duration" : 60,
  "auto_annotate" : null,
  "auto_clear_issues" : null,
  "comp_desc1" : "Active Memory",
  "comp_desc2" : "85%",
  "comp_func" : ">=",
  "comp_val1" : [ "ce_rcsummary_v1","used_pcent"],
  "comp_val2" : [ 0.84999999999999998 ],
  "defn_desc" : "himem",
  "id" : "50253460d9106a182b00000e",
  "match" : {  },
  "notify" : {  },
  "notify_on_clear" : null,
  "state" : "enabled",
  "type" : "ce_revealcloud"
}
{% endhighlight %}

###3. Problem with Remove
See the Remove section below. I cannot get this command to work; in fact I can't find 
any API 'alert definition remove' code. 


###4. Need to document the alert definition structure.


###<<<<<<<<<<<<<<<<<<  End of Questions and Issues  >>>>>>>>>>>>>>>>>

Index
-----
List all Alert Definitions.

CURL Command:
{% highlight sh %}
curl -u myapikey:U https://api.copperegg.com/v2/alerts/definitions.json
*** remove curl -u pxAJ7BSmPXXl3k9W:U https://api.copperegg.com/v2/alerts/definitions.json
{% endhighlight %}

CURL Response:

Response is JSON with an array of alert definition structures.
{% highlight sh %}
[ 
  { 
    "alert_duration" : 60,
    "auto_annotate" : false,
    "auto_clear_issues" : false,
    "comp_desc1" : "Active Memory",
    "comp_desc2" : "85%",
    "comp_func" : ">=",
    "comp_val1" : [ "ce_rcsummary_v1","used_pcent" ],
    "comp_val2" : [ 0.84999999999999998 ],
    "defn_desc" : "himem",
    "id" : "50249b035d9f4f8422000006",
    "match" : { "tag" : [ "coppereggservice" ] },
    "notify" : { 
      "email" : [  ],
      "webhook" : [ "http://requestb.in/11zcb5x1" ]
    },
    "notify_on_clear" : true,
    "state" : "disabled",
    "type" : "ce_revealcloud"
  } 
]
{% endhighlight %}


Show
----
Show in-depth information about a single alert definition.

Required parameters: ..... alert definition id as part of the path

CURL Command:
{% highlight sh %}
curl -u myapikey:U https://api.copperegg.com/v2/alerts/definitions/50249b035d9f4f8422000006.json
*** curl -u pxAJ7BSmPXXl3k9W:U https://api.copperegg.com/v2/alerts/definitions/50249b035d9f4f8422000006.json
{% endhighlight %}

CURL Response:

Response is JSON with an single alert definition structure.

{% highlight javascript %}
{ 
  "alert_duration" : 60,
  "auto_annotate" : false,
  "auto_clear_issues" : false,
  "comp_desc1" : "Active Memory",
  "comp_desc2" : "85%",
  "comp_func" : ">=",
  "comp_val1" : [ "ce_rcsummary_v1","used_pcent" ],
  "comp_val2" : [ 0.84999999999999998 ],
  "defn_desc" : "himem",
  "id" : "50249b035d9f4f8422000006",
  "match" : { "tag" : [ "coppereggservice" ] },
  "notify" : { 
    "email" : [  ],
    "webhook" : [ "http://requestb.in/11zcb5x1" ]
    },
  "notify_on_clear" : true,
  "state" : "disabled",
  "type" : "ce_revealcloud"
}
{% endhighlight %}


Create
------
Create a new alert definition.


####Required parameters:
* defn_desc ........... a short text description of your choice
* type ................ ce_revealcloud or ce_revealcloud
* comp_func ........... { < > <= >= = != =~ !~ }
* comp_desc1 .......... see 'Specifying Comparison parameters' below
* comp_val1 ...........    ''
* comp_val2 ...........    ''
* comp_desc2 ..........    ''

####Optional parameters:
* auto_clear_issues ... true or false
* notify_on_clear ..... true or false
* auto_annotate ....... true or false
* alert_duration ...... in seconds
* state ............... enabled or disabled
* match ............... if not specified, defaults to match anything
* notify {campfire[],email[],hipchat[],pagerduty[],sms[],twitter[],webhook[]}


###Specifying Comparison parameters

####RevealCloud
{% highlight javascript %}
  Process List
    "comp_func":"select from->",              //{ "=~" "!~" }
    "comp_val1":["ce_usage","payload"],
    "comp_desc1":"Process list",
    "comp_val2":["yourprocess"],              //replace 'yourprocess' with a string
    "comp_desc2":"yourprocess",               //replace 'yourprocess' with a string

  CPU Total Usage
    "comp_func": "select from ->",            //{ < > <= >= = != }
    "comp_val1":["ce_rcsummary_v1","active"],
    "comp_desc1":"CPU Total Usage",
    "comp_val2":[0.8],                        // 0.1 to 1.0
    "comp_desc2":"80%",                       // 1% to 100%

  CPU Steal Usage
    "comp_func": "select from ->",            //{ < > <= >= = != }
    "comp_val1":["ce_rcsummary_v1","steal"],
    "comp_desc1":"CPU Steal Usage",
    "comp_val2":[0.3],                        // 0.1 to 1.0
    "comp_desc2":"30%",                   //comp_val2 expressed as %, converted to str

  CPU IOWait Usage
    "comp_func": "select from ->",            //{ < > <= >= = != }
    "comp_val1":["ce_rcsummary_v1","iowait"],
    "comp_desc1":"CPU IOWait Usage",
    "comp_val2":[0.25],                        // 0.1 to 1.0
    "comp_desc2":"25%",                   //comp_val2 expressed as %, converted to str

  Active Memory Usage   
    "comp_func": "select from ->",            //{ < > <= >= = != }
    "comp_val1":["ce_rcsummary_v1","used_pcent"],
    "comp_desc1":"Active Memory",
    "comp_val2":[0.95],                       // 0.1 to 1.0
    "comp_desc2":"95%"                    //comp_val2 expressed as %, converted to str

  Filesystem Usage
    "comp_func": "select from ->",            //{ < > <= >= = != }
    "comp_val1":["ce_filesystem_v1","used_pcent"],
    "comp_desc1":"Filesystem Usage",
    "comp_val2":[0.8],                        // 0.1 to 1.0
    "comp_desc2":"80%",                   //comp_val2 expressed as %, converted to str

  Load
    "comp_func": "select from ->",            //{ < > <= >= = != }
    "comp_val1":["ce_rcsummary_v1","load_shortterm"],
    "comp_desc1":"Load",
    "comp_val2":[5],                    //allowed: greater than 0 
    "comp_desc2":"5",                   //comp_val2 converted to str

  Network Bytes Sent
    "comp_func": "select from ->",      //{ < > <= >= = != }
    "comp_val1":["ce_rcsummary_v1","if_bytes_tx_gauge"],
    "comp_desc1":"Network Bytes Sent",
    "comp_val2":[2621440],              //allowed: greater than 0
    "comp_desc2":"2.5 MB/s",            //comp_val2 expressed as MB/s, converted to str

  Network Bytes Received
    "comp_func": "select from ->",      //{ < > <= >= = != }
    "comp_val1":["ce_rcsummary_v1","if_bytes_rx_gauge"],
    "comp_desc1":"Network Bytes Received",
    "comp_val2":[209715.2],             //allowed: greater than 0
    "comp_desc2":"0.2 MB/s",            //comp_val2 expressed as MB/s, converted to str

  Health
    "comp_func": "select from ->",      //{ < > <= >= = != }
    "comp_val1":["ce_health","health_index"],
    "comp_desc1":"Health Index",
    "comp_val2":[0.45],                 // 0.1 to 1.0
    "comp_desc2":"45%",                 //comp_val2 expressed as %, converted to str

  System Not Seen
    "comp_func":"",
    "comp_val1":["ce_health","health_state_last_updated"],
    "comp_desc1":"System Not Seen",
    "comp_val2":[""],
    "comp_desc2":"",
{% endhighlight %}

####RevealUptime
{% highlight javascript %}
  Response Time
    "comp_func": "select from ->",            //{ < > <= >= = != }
    "comp_val1":["ce_probe_summary_v1","time"],
    "comp_desc1":"Response Time",
    "comp_val2":["3000"],             //allowed: greater than 0, string containing RT
    "comp_desc2":"3000ms",            //comp_val2 string with ms appended

  Response Status Code
    "comp_func":"select from->",              //{ < > <= >= = != =~ !~ }
    "comp_val1":["ce_probe_summary_v1","status_code"],
    "comp_desc1":"Status Code",
    "comp_val2":["^[45]"],            // str containing a code, or a regex exp
    "comp_desc2":"^[45]",             // str containing a code, or a regex exp

  Uptime
    "comp_val1":["ce_probe_summary_v1","status"],
    "comp_desc1":"Uptime",
    "comp_val2":[0.8],                // 0.1 to 1.0
    "comp_desc2":"80%"                //comp_val2 expressed as %, converted to str

  Health
    "comp_func": "select from ->",            //{ < > <= >= = != }
    "comp_val1":["ce_probe_summary_v1","health"],
    "comp_desc1":"Health Index",
    "comp_val2":[0.2],                // 0.1 to 1.0
    "comp_desc2":"20%"                //comp_val2 expressed as %, converted to str
{% endhighlight %}




###Create Example 1: create a new alert definition, to demonstrate defaults.

CURL Command:
{% highlight sh %}
curl -u pxAJ7BSmPXXl3k9W:U -H "Content-Type: application/json" -XPOST -d '{"defn_desc":"himem","comp_func":">=","comp_desc1":"Active Memory","comp_val1":["ce_rcsummary_v1","used_pcent"],"comp_val2":[0.85],"comp_desc2":"85%","alert_duration":60,"type":"ce_revealcloud"}' https://api.copperegg.com/v2/alerts/definitions.json | json_reformat
{% endhighlight %}

CURL Response:
{% highlight javascript %}
{
}
{% endhighlight %}

The following is returned from an :index command:
{% highlight javascript %}
{ 
  "alert_duration" : 60,
  "auto_annotate" : null,
  "auto_clear_issues" : null,
  "comp_desc1" : "Active Memory",
  "comp_desc2" : "85%",
  "comp_func" : ">=",
  "comp_val1" : [ "ce_rcsummary_v1","used_pcent" ],
  "comp_val2" : [ 0.84999999999999998 ],
  "defn_desc" : "himem",
  "id" : "50254fec8d0dc71230000011",
  "match" : {  },
  "notify" : {  },
  "notify_on_clear" : null,
  "state" : "enabled",
  "type" : "ce_revealcloud"
}
{% endhighlight %}



###Create Example 2: create a new alert definition, with all parameters.

CURL Command:
{% highlight sh %}
curl -u pxAJ7BSmPXXl3k9W:U -H "Content-Type: application/json" -XPOST -d '{"defn_desc":"himem","comp_func":">=","comp_desc1":"Active Memory","auto_clear_issues":true,"notify_on_clear":true,"auto_annotate":false,"comp_val1":["ce_rcsummary_v1","used_pcent"],"comp_val2":[0.85],"comp_desc2":"85%","alert_duration":60,"type":"ce_revealcloud","match":{"tag":["my_webtier"]},"notify":{"email":[],"webhook":["http://requestb.in/11zcb5x1"]}}' https://api.copperegg.com/v2/alerts/definitions.json | json_reformat
{% endhighlight %}

CURL Response:

Response is JSON with a new alert definition structure:

{% highlight javascript %}
{
  "alert_duration" : 60,
  "auto_annotate" : false,
  "auto_clear_issues" : true,
  "comp_desc1" : "Active Memory",
  "comp_desc2" : "85%",
  "comp_func" : ">=",
  "comp_val1" : [ "ce_rcsummary_v1","used_pcent" ],
  "comp_val2" : [ 0.84999999999999998 ],
  "defn_desc" : "himem",
  "id" : "502551a18d0dc70fff00003d",
  "match" : { "tag" : [ "my_webtier" ] },
  "notify" : { 
    "email" : [  ],
    "webhook" : [ "http://requestb.in/11zcb5x1" ]
    },
  "notify_on_clear" : true,
  "state" : "enabled",
  "type" : "ce_revealcloud"
}
{% endhighlight %}


Update
------
Update an existing alert definition.

Required parameter ..... alert definition id as part of the path

Optional parameters .... same as described for :create
  

Example: Change alert duration, and some flags using Update.

CURL Command:
{% highlight sh %}
curl -u pxAJ7BSmPXXl3k9W:U -H "Content-Type: application/json" -XPUT -d '{"auto_clear_issues":false,"auto_annotate":true,"notify_on_clear":false,"alert_duration":120}' https://api.copperegg.com/v2/alerts/definitions/502557848d0dc719ac000003.json | json_reformat
{% endhighlight %}

CURL Response:
{% highlight javascript %}
{
}
{% endhighlight %}

Use the :show command to retrieve the updated alert definition.

CURL Command:
{% highlight sh %}
curl -u pxAJ7BSmPXXl3k9W:U https://api.copperegg.com/v2/alerts/definitions/502557848d0dc719ac000003.json
{% endhighlight %}

CURL Response:
{% highlight javascript %}
{ "alert_duration" : 120,
  "auto_annotate" : true,
  "auto_clear_issues" : false,
  "comp_desc1" : "Active Memory",
  "comp_desc2" : "85%",
  "comp_func" : ">=",
  "comp_val1" : [ "ce_rcsummary_v1","used_pcent" ],
  "comp_val2" : [ 0.84999999999999998 ],
  "defn_desc" : "himem",
  "id" : "502557848d0dc719ac000003",
  "match" : { 
    "tag" : [ "my_webtier" ] },
    "notify" : { "email" : [  ],
    "webhook" : [ "http://requestb.in/11zcb5x1" ]
  },
  "notify_on_clear" : false,
  "state" : "enabled",
  "type" : "ce_revealcloud"
}
{% endhighlight %}


Remove
-------
Remove the specified alert definition.

Required parameter ..... alert definition id as part of the path

CURL Command:
{% highlight sh %}
curl  -u myapikey:U -XDELETE  https://api.copperegg.com/v2/revealuptime/probes/50203ddf35d58d034500000f.json
*** remove curl -u pxAJ7BSmPXXl3k9W:U -XDELETE https://api.copperegg.com/v2/alerts/definitions/502557848d0dc719ac000003.json
{% endhighlight %}

CURL Response:

Response is Status 200, empty JSON:

{% highlight javascript %}
{

}
{% endhighlight %}
