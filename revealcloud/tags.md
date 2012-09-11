---
layout: default
title: RevealCloud - Tags
---


Index
-----
List all defined RevealCloud tags.

CURL Command:
{% highlight sh %}
curl -u APIKEY:U https://api.copperegg.com/v2/revealcloud/tags.json
{% endhighlight %}

CURL Response:

Response is JSON with an array of hashes, one hash per RevealCloud tag.

{% highlight sh %}
[  
  {
    "id":"amazon",
    "uuids":["e0cdba3789d38f412aadec6480c286b7","49d012aea603be267441bd22da4bf803"]
  },
  {
    "id":"App1",
    "uuids":["e0cdba3789d38f412aadec6480c286b7"]
  },
  {
    "id":"App2",
    "uuids":["49d012aea603be267441bd22da4bf803"]
  },
  {
    "id":"local",
    "uuids":["ac1f5ef85c1177ef97596f334f877370"]
  },
  {
    "id":"mac",
    "uuids":["ac1f5ef85c1177ef97596f334f877370"]
  }
]
{% endhighlight %}   
   
In the example above: five tags are returned by the Index command; "App1", "App2", "mac", "local" and "amazon". Note that each tag hash contains a single tag "id", which is the Label for the tag, and an array of "uuids", one for each monitored system with the tag of reference.
   
   
   
Show
----
Show in-depth information about a single RevealCloud tag.

Required Parameters: the tag of interest, as part of the path.

CURL Command:
{% highlight sh %}
curl -u APIKEY:U https://api.copperegg.com/v2/revealcloud/tags/TAG.json
{% endhighlight %}   
    
CURL Response:   
   
Response is JSON with an array of hashes containing details of all systems associated with the specified tag. 

In the example below, the tag "amazon" was provided:

{% highlight sh %}
[
  {
    "last_updated":1347331194,                                    # time when this tag was last updated
    "created_at":1347330508,                                      # time when this tag was created
    "attrs":{
      "aws_local_hostname":"ip-10-86-210-174.ec2.internal",       # host name retrieved from the cloud service provider
      "aws_inst_id":"i-9a6e01e0",                                 # instance_id retrieved from the cloud service provider
      "rc_health_info":"[2, 1, 1, 1, 1, 1, 1]",                   # internal use
      "aws_mac_addr":"12:31:38:19:D4:60",                         # mac address retrieved from the cloud service provider
      "rc_os":"linux-2.6",                                        # OS reported by the cloud service provider
      "aws_kernel_id":"aki-88aa75e1",                             # OS kernel_id reported by the cloud service provider
      "aws_local_ipv4":"10.86.210.174",                           # IP address local to the cloud service provider
      "uuid_type":"uuid_hypervisor",                              # how revealcloud created the uuid
      "rc_version":"v3-43-geefad79",                              # revealcloud collector version
      "aws_profile":"default-paravirtual",                        # returned by cloud service provider
      "uts_sysname":"Linux",                                      # uts name seen by the revealcloud collector
      "uts_release":"3.2.28-45.62.amzn1.x86_64",                  # uts release seen by the revealcloud collector
      "rc_health_timestamp":"1347331194",                         # time of most recent revealcloud health check
      "uuid_origin":"00000000-0000-0000-0000-ec2327827936\n",     # uuid reported by cloud service provider (internal use)
      "hostname":"ip-10-86-210-174",                              # hostname provided by cloud service provider
      "version_checked_at":"2012-09-10 21:39:43 -0500",           # time of last collector version check
      "aws_availability_zone":"us-east-1b",                       # cloud service provider availability zone
      "uts_version":"#1 SMP Wed Aug 22 03:09:00 UTC 2012",                                    # OS uts version 
      "rc_args":"-a api.copperegg.com -k yakCgQewmwKtywGH -P /usr/local/revealcloud/run ",    # command line arguments when collectore was started
      "rc_health_index":"0.93",                                                               # current helath index
      "uts_nodename":"ip-10-86-210-174",                                  # uts node name
      "linux_distro":"Amazon Linux AMI release 2012.03\n",                # linux distobution read by the collector
      "aws_public_hostname":"ec2-54-242-3-44.compute-1.amazonaws.com",    # public hostname, provided by cloud service provider
      "aws_reservation_id":"r-93a62ef4",                                  # cloud service provider-specific reservation
      "aws_inst_type":"m1.small",                                 # cloud service provider-specific instance type
      "aws_hostname":"ip-10-86-210-174.ec2.internal",             # cloud service provider internal hostname
      "rc_health_state":"1",                                      # current health state, per the rc collector
      "aws_public_ipv4":"54.242.3.44",                            # public IP address, provided by cloud service provider
      "aws_ami_id":"ami-01902168",                                # image id, cloud service provider-specific
      "uts_machine":"x86_64",                                     # uts machine architecture
      "aws_sec_group":"AppSecurityGroup-111111111111"             # cloud-service provider security group name
    },
    "state":2,                                # current state of this system hash
    "tags":["App1","amazon"],                 # tags associated with this system
    "id":null,                                # internal use
    "uuid":null,                              # internal use  
    "published_rc_version":"v3-43-geefad79",  # RevealCloud version
    "health":0                                # internal use
  },
  {
    "last_updated":1347331114,
    "created_at":1347330514,
    "attrs":{
      "link":"12:31:38:19:d4:60",
      "inet":"10.86.210.174",
      "inet6":"fe80::1031:38ff:fe19:d460"
    },
    "state":2,
    "tags":["App1","amazon"],
    "id":null,
    "uuid":null,
    "published_rc_version":"",
    "health":0
  },
  {
    "last_updated":1347330520,
    "created_at":1347330520,
    "attrs":{},
    "state":3,
    "tags":["App1","amazon"],
    "id":null,
    "uuid":null,
    "published_rc_version":"",
    "health":0
  },
  {
    "last_updated":1347330514,
    "created_at":1347330514,
    "attrs":{},
    "state":3,
    "tags":["App1","amazon"],
    "id":null,
    "uuid":null,
    "published_rc_version":"",
    "health":0
  },
  {
    "last_updated":1347331193,
    "created_at":1347330768,
    "attrs":{
      "aws_local_hostname":"ip-10-144-9-94.ec2.internal",
      "aws_inst_id":"i-9e6e01e4",
      "rc_health_info":"[2, 1, 1, 1, 1, 1, 1]",
      "aws_mac_addr":"22:00:0A:90:09:5E",
      "rc_os":"linux-2.6",
      "aws_kernel_id":"aki-88aa75e1",
      "aws_local_ipv4":"10.144.9.94",
      "uuid_type":"uuid_hypervisor",
      "rc_version":"v3-43-geefad79",
      "aws_profile":"default-paravirtual",
      "uts_sysname":"Linux",
      "uts_release":"3.2.28-45.62.amzn1.x86_64",
      "rc_health_timestamp":"1347331194",
      "uuid_origin":"00000000-0000-0000-0000-ec2327827940\n",
      "hostname":"ip-10-144-9-94",
      "version_checked_at":"2012-09-10 21:39:48 -0500",
      "aws_availability_zone":"us-east-1a",
      "uts_version":"#1 SMP Wed Aug 22 03:09:00 UTC 2012",
      "rc_args":"-a api.copperegg.com -k yakCgQewmwKtywGH -P /usr/local/revealcloud/run ",
      "rc_health_index":"0.93",
      "uts_nodename":"ip-10-144-9-94",
      "linux_distro":"Amazon Linux AMI release 2012.03\n",
      "aws_public_hostname":"ec2-184-73-64-30.compute-1.amazonaws.com",
      "aws_reservation_id":"r-91a62ef6",
      "aws_inst_type":"m1.small",
      "aws_hostname":"ip-10-144-9-94.ec2.internal",
      "rc_health_state":"1",
      "aws_public_ipv4":"184.73.64.30",
      "aws_ami_id":"ami-01902168",
      "uts_machine":"x86_64",
      "aws_sec_group":"AppSecurityGroup-111111111111"
    },
    "state":2,
    "tags":["App2","amazon"],
    "id":null,
    "uuid":null,
    "published_rc_version":"v3-43-geefad79",
    "health":0
  },
  {
    "last_updated":1347330773,
    "created_at":1347330773,
    "attrs":{
      "link":"22:00:0a:90:09:5e",
      "inet":"10.144.9.94",
      "inet6":"fe80::2000:aff:fe90:95e"
    },
    "state":3,
    "tags":["App2","amazon"],
    "id":null,
    "uuid":null,
    "published_rc_version":"",
    "health":0
  },
  {
    "last_updated":1347330778,
    "created_at":1347330778,
    "attrs":{},
    "state":3,
    "tags":["App2","amazon"],
    "id":null,
    "uuid":null,
    "published_rc_version":"",
    "health":0
  },
  {
    "last_updated":1347330773,
    "created_at":1347330773,
    "attrs":{},
    "state":3,
    "tags":["App2","amazon"],
    "id":null,
    "uuid":null,
    "published_rc_version":"",
    "health":0
  }
]
{% endhighlight %}   
   
Note: the results above indicate that the tag 'amazon' is associated with two systems.   
   
   
Create
------
Add a new tag to one or more defined systems.

Required params:  
   
* a tag ( tags may contain a-z, A-Z, 0-9, - and _)  
   
* one or more uuids to which the tag will be applied  
   
* if specifying more than one uuid, use a comma-separated list  
   
In the following example, a tag labelled "systemtest" will be applied to two existing systems, with uuids of e0cdba3789d38f412aadec6480c286b7 and ac1f5ef85c1177ef97596f334f877370.
   
CURL Command:
{% highlight sh %}
curl -u APIKEY:U -XPOST https://api.copperegg.com/v2/revealcloud/tags.json -d 'id=systemtest&uuids=e0cdba3789d38f412aadec6480c286b7,ac1f5ef85c1177ef97596f334f877370'
{% endhighlight %}   
    
   
   
Remove
-------
Remove a tag from one system.

Required params:
* a tag
* the uuid of the system from which the tag will be removed; uuid is part of the path

CURL Command:
{% highlight sh %}
curl -XDELETE -u APIKEY:U https://api.copperegg.com/v2/revealcloud/tags/TAG/UUID.json
{% endhighlight %}   
   
CURL Response:

Response is Status 200, empty JSON:   
   
{% highlight sh %}
{

}
{% endhighlight %}   
   
   
In the following example, the tag labelled "amazon" will be removed from one of the two systems, (see the Show example). Specifically, the system with uuid = e0cdba3789d38f412aadec6480c286b7.
   
   
CURL Command:
{% highlight sh %}
curl -XDELETE -u APIKEY:U https://api.copperegg.com/v2/revealcloud/tags/amazon/e0cdba3789d38f412aadec6480c286b7.json
{% endhighlight %}   
   
