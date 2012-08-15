---
layout: default
title: Alerts - Issues
---

Overview
--------

Each of the API commands described here relate to the set of all issues that have occurred on your site. Today there are two kinds of issues, those created by system alerts, (RevealCloud) and those created by website alerts (RevealUptime). 

Both kinds of issues are presented and operated on in the same way by this API. Each issue is completely described by an Issue hash. The key-value pairs within the Issue hash are described in detail in the final sections of this document.


Index
-----

CURL Command:
{% highlight sh %}
curl -u APIKEY:U https://api.copperegg.com/v2/alerts/issues.json
{% endhighlight %}

CURL Response:

Response is a JSON array of all non-deleted issues. In this example, there are two issues; the first is an issue caused by a website alert, the second caused by a system alert.

{% highlight javascript %}
[
  {
    "id":"50183b776cc66909b7758065",
    "state":"cleared",
    "short_msg":"my_website: Lores_Health (Health Index 90% < 95%)",
    "attr_description":"Additional Information",
    "attrs":{
      "label":"my_website", 
      "description":"Lores_Health",
      "destination":"http://mywebsite.com",
      "frequency","60",
      "type","GET"
    },
    "type":"ce_revealuptime",
    "created_at":1343765367,
    "updated_at":1343765380,
    "cleared_date":1343765380,
    "notified_date":1343765368,
    "ignore_until":1343765372,
    "annotation_id":"",
    "obj_idv":"5004a81187517319f4000238|cjwTwDzL2q9QE8x16fGrSGoVRUPm0Jrk|"
  },
  { 
    "id":"501b40596cc66909b7760cd0",
    "state":"cleared",
    "short_msg":"DBServer: Lost nfsd (Process list does not contain nfsd)",
    "attr_description":"Additional Information",
    "attrs":
      "ce_processes":"{
        \"p\":[
    [\"launchd\",null,1,\"0\",\"S\",0.000003,0.000003,0.000007,0,2568998912,2162688,0],
          [\"netbiosd\",null,104,\"222\",\"S\",0,0,0,0,2597040128,3117056,0],
          [\"UserEventAgent\",null,11,\"0\",\"S\",0,0,0,0,2587148288,4882432,0],
          [\"ntpd\",null,98,\"0\",\"S\",0.000002,0.000006,0.000008,0,2560475136,1245184,0],
                                    ... ,
          [\"SystemStarter\",null,99,\"0\",\"S\",0,0,0,0,2559008768,745472,0]
        ],
        \"u\":[
          [-2,0.000001,0.000003,0.000004,0,2572431360,5767168,0],
          [0,0.003760,0.012779,0.016539,0,138357985280,1688731648,0],
          [501,0.023961,0.005368,0.029330,0,221265072128,3804700672,0],
          [65,0.000010,0.000011,0.000021,0,2578763776,4583424,0],
          [88,0.001999,0.000763,0.002762,0,3631882240,155607040,0]
        ]
      }",
      "hostname":"mysql_1",
      "label":"DBServer"
    },
    "type":"ce_revealcloud",
    "created_at":1343963225,
    "updated_at":1343963357,
    "cleared_date":1343963357,
    "notified_date":1343963228,
    "ignore_until":1343963230,
    "annotation_id":"",
    "obj_idv":"ac1f5ef85c1177ef97596f334f877370|"
  }
]
{% endhighlight %}


Show
----
Show in-depth information about a single issue.

Required Parameters: the id of the issue of interest.

CURL Command:
{% highlight sh %}
curl -u APIKEY:U https://api.copperegg.com/v2/alerts/issues/ISSUEID.json
{% endhighlight %}

CURL Response:

Response is a JSON hash containing details of the specified issue; in this case, id 188:
{% highlight javascript %}
{
  "id":188,
  "state":"notified",
  "short_msg":"mysql_1: Memory Use - High (Active Memory 0.958 >= 0.95)",
  "attr_description":"Additional Information",
  "attrs":{
    "aws_profile":"default-paravirtual",
    "hostname":"mysql-1",
    "aws_availability_zone":"us-east-1b",
    "linux_distro":"Ubuntu 12.04 LTS \\n \\l\n",
    "aws_public_hostname":"ec2-000-001-00-11.compute-1.amazonaws.com",
    "aws_reservation_id":"my_res_id",
    "aws_inst_type":"c1.xlarge",
    "aws_hostname":"ip-127.0.0.1.ec2.internal",
    "aws_public_ipv4":"127.0.0.1",
    "aws_ami_id":"ami-0674d66f",
    "aws_sec_group":"API Server",
    "aws_local_hostname":"ip-127-0-0-1.ec2.internal",
    "aws_inst_id":"my_inst_id",
    "aws_mac_addr":"11:22:33:44:55:66",
    "aws_local_ipv4":"127.0.0.1",
    "aws_kernel_id":"aki-825ea7eb"
  },
  "type":"ce_revealcloud",
  "created_at":1344521344,
  "updated_at":0,
  "cleared_at":0,
  "notified_at":1344521506,
  "ignore_until":1344521349,
  "annotation_id":"",
  "obj_idv":"d16b38d742a8ada6ccc7b8b33d5eb7dd|"
}

{% endhighlight %}



Update 
----
Update a single issue.

Required Parameters: 
* the id of the issue of interest
* a string specifying a change of state. Permissible strings are :
  * "state=active" 
  * "state=notified"
  * "state=acknowledged"
  * "state=cleared"
  * "state=snoozed"

CURL Command:
{% highlight sh %}
curl -XPUT https://APIKEY:U@api.copperegg.com/v2/alerts/issues/ISSUEID.json -d "state=cleared"
{% endhighlight %}

CURL Response:

Response is Status 200, empty JSON:

{% highlight javascript %}
{
}
{% endhighlight %}



Destroy
----
Delete a single issue.

Required Parameters: 
* the id of the issue of interest
* the string "state=deleted"

CURL Command:
{% highlight sh %}
curl -XPUT https://APIKEY:U@api.copperegg.com/v2/alerts/issues/ISSUEID.json -d "state=deleted"
{% endhighlight %}

CURL Response:

The specified issue will be deleted.
Response is Status 200, empty JSON:

{% highlight javascript %}
{
}
{% endhighlight %}



The Issue hash
--------------

The JSON-formatted Issue hash has the following structure:
{
  "id":"unique identifier string",
  "state":"string describing the state of the issue",
  "short_msg":"string describing the alert trigger",
  "attr_description":"Additional Information",
  "attrs":{
    "key1":"relevant value1", 
    "key2":"relevant value2",
    "keyN":"relevant value N"
  },
  "type":"string indicating alert source",
  "created_at":timestamp,
  "updated_at":timestamp,
  "cleared_date":timestamp, or 0
  "notified_date":timestamp, or 0
  "ignore_until": ignore this
  "annotation_id":"id", or "", 
  "obj_idv":"ignore this"
},


###Definition of key:value pairs in a System Issue hash:

* "id":188
    Unique id for this issue structure.

* "state":"cleared"   
    Current state of this issue. Possible values are "active", "notified", "acknowledged", "snoozed" and "cleared".

* "short_msg":"DBServer: CPU-total (CPU Total Usage 0.945 > 0.9)" 
    This string is a human-readable description of the system alert that triggered the creation of this issue.

* "attr_description":"Additional Information"           
    A string describing the contents of the following 'attrs' field, which may be useful for parsing its contents.

* "attrs":{ "hostname":"DBtier-s1",  "label":"DBServer" }           
    A hash containing information pertinent to this issue. This Additional Information may vary depending on many factors, including the system (virtual, physical), services provider and OS. 
  
* "type":"ce_revealcloud"   
    Type of issue, "ce_revealcloud" indicating a System issue. 

* "created_at":1344631403       
    Time and Date of alert & issue creation. UTC -> unix timestamp

* "updated_at":1344632039       
    Time and Date of most recent update. UTC -> unix timestamp

* "cleared_date":0            
    Time and Date when the issue was cleared, or 0. UTC -> unix timestamp

* "notified_date":1344631404    
    Time and Date when notified, or 0. UTC -> unix timestamp

* "ignore_until":1344631408
    CopperEgg Internal use. 

* "annotation_id":""
    The id of an annotation created by the same alert as this issue, or null.

* "obj_idv":"ac1f5ef85c1177ef97596f334f877370|"
    CopperEgg Internal use.     


###Definition of key:value pairs in a Website Issue hash:
The keys are the same as for the System Issue. The difference between the two hashes can be found in the values of the following key:value pairs:


* "short_msg":"MyWebsite: Slow Response Time (Response Time 110 ms >= 40.0 ms)"
    This string is a human-readable description of the website alert that triggered the creation of this issue.
          
* "attrs":{
    "label":"my_website", 
    "description":"Lores_Health",
    "destination":"http://mywebsite.com",
    "frequency","60",
    "type","GET"
  }
  A hash containing information pertinent to this issue. The Additional Information provided for website issues is of course different than that for system issues.
 
* "type":"ce_revealuptime"   
    Type of issue, "ce_revealuptime" indicating a website (AKA probe) issue.  



