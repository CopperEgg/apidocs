---
layout: default
title: Alerts - Issues
---

##Overview

Each of the API commands described here relate to retrieving, editing, and deleting the Issues that have occurred on your site.  
Today there are three kinds of issues, those created by system alerts, (RevealCloud), those created by website alerts (RevealUptime), and those created by custom metrics (RevealMetrics). 

Each issue is completely described by an Issue hash.

----
###The Issue Hash
The JSON-encoded Issue Hash is shown in the following system alert example:

{% highlight sh %}
{
  "id":3607050,                                     # Unique Issue_ID 
  "state":"cleared",                                # current state
  "short_msg":"MacBookPro: HighCPU (CPU Total Usage 0.035 > 0.01)",   # text msg describing the alert trigger
  "attr_description":"Additional Information",      # text description of the following attributes
  "attrs":{                                         # attributes specific to this Issue
    "inet6":"fe80::ca2a:14ff:fe2c:25c0",
    "hostname":"ScottsMacBookPro.local",
    "inet":"10.0.1.113,10.0.1.114"
  },
  "type":"ce_revealcloud",                          # one of the three Issue types mentioned above
  "created_at":1364849548,                          # timestamp of initial alert trigger
  "updated_at":1364853492,                          # timestamp of last update
  "cleared_at":1364853492,                          # timestamp of clear event
  "notified_at":1364849549,                         # timestamp of notification event
  "ignore_until":0,                                 # read-only field, internal use
  "annotation_id":"",                               # read-only field, internal use
  "obj_idv":"ac1f5ef85c1177ef97596f334f877370|"     # read-only field, object identifier
}
{% endhighlight %}

----
##Index
----
Retrieve all existing Issues at your site (in batches of 200 max).

####CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U https://api.copperegg.com/v2/alerts/issues.json?per_page=integer&page_number=integer

curl -s https://<APIKEY>:U@api.copperegg.com/v2/alerts/issues.json?per_page=integer&page_number=integer
{% endhighlight %}

where <br>
per_page    = No. of issues to be fetched in a page (in one call). Maximum is 200. <br>
page_number = The number of results you would like to get in one call. Maximum and default value is 200. <br>

####CURL Response:
Response is an array of JSON-encoded Issue Hashes. In this example, there are two issues; the first is a website alert, the second a system alert.

{% highlight ruby %}
[
 {
  "id":"50183b776cc66909b7758065",
  "state":"cleared",
  "short_msg":"my_website: Lores_Health (Health Index 90% < 95%)",
  "attr_description":"Additional Information",
  "attrs":{                               # attributes found in a website / port alert
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
  "attrs":                                # attributes found in process alert
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
  
----  
##Show
----
Show in-depth information about a single Issue.  
  
####Required Parameters:  
Issue_ID as part of the path
  
####CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U https://api.copperegg.com/v2/alerts/issues/ISSUE_ID.json

curl -s https://<APIKEY>:U@api.copperegg.com/v2/alerts/issues/ISSUE_ID.json
{% endhighlight %}  
  
####CURL Response:  
  
Response is a single JSON-encoded Issue Hash. 
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
  
----
##Update 
----
Update a single Issue.

####Required Parameters:  
Issue_ID as part of the path  
  
A string specifying a change of state. Permissible strings are :
* "state=active" 
* "state=notified"
* "state=acknowledged"
* "state=cleared"
* "state=snoozed"  
  
####CURL Command, and variations:  
{% highlight sh %}
curl -s -XPUT https://<APIKEY>:U@api.copperegg.com/v2/alerts/issues/ISSUE_ID.json -d "state=cleared"

curl -su <APIKEY>:U https://api.copperegg.com/v2/alerts/issues/ISSUE_ID.json -XPUT -d "state=cleared"
{% endhighlight %}  
  
####CURL Response:  
  
Response is Status 200, and the newly updated Issue Hash

{% highlight javascript %}
{
 "id":3607894,
 "state":"cleared",
 "short_msg":"MacBookPro: HighCPU (CPU Total Usage 0.018 > 0.01)",
 "attr_description":"Additional Information",
 "attrs":{
  "inet":"10.0.1.113,10.0.1.114",
  "inet6":"fe80::ca2a:14ff:fe2c:25c0",
  "hostname":"MacBookPro"},
  "type":"ce_revealcloud",
  "created_at":1364854093,
  "updated_at":1364877323,
  "cleared_at":1364877323,
  "notified_at":1364854093,
  "ignore_until":0,
  "annotation_id":"",
  "obj_idv":"ac1f5ef85c1177ef97596f334f877370|"
} 
{% endhighlight %}  
  
----
##Delete
----
Delete a single Issue

####Required Parameters:  
Issue_ID as part of the path  
  
The string "state=deleted"  

####CURL Command, and variations:
{% highlight sh %}
curl -s -XPUT https://<APIKEY>:U@api.copperegg.com/v2/alerts/issues/<ISSUE_ID>.json -d "state=deleted"

curl -su <APIKEY>:U https://api.copperegg.com/v2/alerts/issues/<ISSUE_ID>.json -XPUT -d "state=deleted"
{% endhighlight %}  
  
####CURL Response:

The specified issue will be deleted.
Response is Status 200, empty JSON:

{% highlight javascript %}
{
}
{% endhighlight %}

