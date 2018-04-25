---
layout: default
title: Azure Samples
---

## Overview

This is an API used to get overview of an Azure Account. It fetches stats related to subscriptions and their resources with corresponding objects and metrics.

### Required Parameters:

account_id
: Id of Azure account which can be retrieved by [Accounts API](accounts.html)


#### CURL Command, and variations:

{% highlight sh %}
curl -su <APIKEY>:U "https://api.copperegg.com/v2/azure/samples/overview.json?account_id=<AZURE_ACCOUNT_ID>"

curl -s  "https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/overview.json?account_id=<AZURE_ACCOUNT_ID>"
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
  "metrics": {
    "resource_type_1": {
      "objects": 100,
      "metrics": 707
    },
    "resource_type_2": {
      "objects": 1,
      "metrics": 1
    }
  }
}
{% endhighlight %}

---

## VM

This is an API used to get samples of one or more VM resources

### VM Sample Keys
{% highlight sh %}
Key name           Valid combinations

Cpu                c
Network            n
Disk               d
{% endhighlight %}

### Fetch Samples from resources specified in idvs

#### Required Parameters:

idvs
: It is a list of ids(unique for every vm resource)

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| VM Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### CURL Command:

{% highlight sh %}

curl -XGET -s 'https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/vm.json -H "Content-Type: application/json" -d '{"idvs":["idv1", "idv2"]}'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{
        "c":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "n":{
            "1484810160":[533795466,30448340],
            "1484810220":[null,null],
            "1484810280":[null,null],
            "1484810340":[null,null],
            "1484810400":[null,null],
            "1484810460":[518838963,27407162],
            "1484810520":[null,null],
            "1484810580":[null,null],
            "1484810640":[null,null],
            "1484810700":[null,null]
        },
        "d":{
            "1484810160":[0,0],
            "1484810220":[0,0],
            "1484810280":[0,0],
            "1484810340":[0,0],
            "1484810400":[0,0],
            "1484810460":[0,0],
            "1484810520":[0,0],
            "1484810580":[0,0],
            "1484810640":[0,0]
        }
    }
}
{% endhighlight %}

---

## VM Details

This is an API used to get detailed samples of a vm resource

### VM Sample Keys
{% highlight sh %}
Key name           Valid combinations

Cpu                c
Network            n
Disk R/W           d
Disk Operations    o
{% endhighlight %}

### Fetch Samples from resource specified by idv

#### Required Parameters:

idv
: unique id for a vm resource

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| VM Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### Optional Parameters:

starttime
: integer value corresponding start time of timeframe for which samples are being fetched

endtime
: integer value corresponding end time of timeframe for which samples are being fetched

#### CURL Command:

{% highlight sh %}
curl -s 'https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/vm_details.json?idv=<IDV1>&starttime=1484810160&endtime=1484811360'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{
        "c":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "n":{
            "1484810160":[533795466,30448340],
            "1484810220":[null,null],
            "1484810280":[null,null],
            "1484810340":[null,null],
            "1484810400":[null,null],
            "1484810460":[518838963,27407162],
            "1484810520":[null,null],
            "1484810580":[null,null],
            "1484810640":[null,null],
            "1484810700":[null,null]
        },
        "d":{
            "1484810160":[0,0],
            "1484810220":[0,0],
            "1484810280":[0,0],
            "1484810340":[0,0],
            "1484810400":[0,0],
            "1484810460":[0,0],
            "1484810520":[0,0],
            "1484810580":[0,0],
            "1484810640":[0,0]
        },
        "o":{
            "1484810160":[0,0],
            "1484810220":[0,0],
            "1484810280":[0,0],
            "1484810340":[0,0],
            "1484810400":[0,0],
            "1484810460":[0,0],
            "1484810520":[0,0],
            "1484810580":[0,0],
            "1484810640":[0,0]
        }
    }
}
{% endhighlight %}

---

## SQL

This is an API used to get samples of one or more SQL resources

### SQL Sample Keys
{% highlight sh %}
Key name           Valid combinations

Cpu                c
I/O                i
Database           p
Throughput (DTU)   t
Connection         n
Workers            w
{% endhighlight %}

### Fetch Samples from resources specified in idvs

#### Required Parameters:

idvs
: It is a list of ids(unique for every sql resource)

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| SQL Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### CURL Command:

{% highlight sh %}
curl -XGET -s https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/sql.json -H "Content-Type: application/json" -d '{"idvs":["idv1", "idv2"]}'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{
        "c":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "i":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "p":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "t":{
            "1484810160":0.441,
            "1484810460":0.428,
            "1484810760":0.464,
            "1484811060":0.448,
            "1484811360":0.429
        },
        "n":{
            "1484810160":[0.841, 0.489, 0.814],
            "1484810460":[0.628, 0.533, 0.384],
            "1484810760":[0.464, 0.461, 0.282],
            "1484811060":[0.248, 0.583, 0.584],
            "1484811360":[0.629, 0.485, 0.734]
        },
        "w":{
            "1484810160":0.541,
            "1484810460":0.528,
            "1484810760":0.564,
            "1484811060":0.548,
            "1484811360":0.529
        }

    }
}
{% endhighlight %}

---

## SQL Details

This is an API used to get detailed samples of a sql resource

### SQL Sample Keys
{% highlight sh %}
Key name           Valid combinations

Cpu                c
I/O                i
Log                l
Throughput         t
Database Size      b
Connections        n                    # successful, failed, blocked by firewall
Deadlocks          d
Storage            p
In Memory Storage  o
Workers            w
Sessions           s
DTU Limit and Used dt
{% endhighlight %}

### Fetch Samples from resource specified by idv

#### Required Parameters:

idv
: unique id for a sql resource

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| SQL Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### Optional Parameters:

starttime
: integer value corresponding start time of timeframe for which samples are being fetched

endtime
: integer value corresponding end time of timeframe for which samples are being fetched

#### CURL Command:

{% highlight sh %}
curl -s 'https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/sql_details.json?idv=<IDV1>&starttime=1484810160&endtime=1484811360'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{
        "c":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "i":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "l":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "t":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "b":{
            "1484810160":533795466,
            "1484810460":30448340,
            "1484810760":518838963,
            "1484811060":27407162,
            "1484811360":513468389
        },
        "n":{
            "1484810160":[10,0,1],
            "1484810460":[12,0,1],
            "1484810760":[15,0,1],
            "1484811060":[10,0,0]
        },
        "d":{
            "1484810160":1,
            "1484810460":0,
            "1484810760":4,
            "1484811060":0,
            "1484811360":0
        },
        "p":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "o":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "w":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "s":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        }
    }
}
{% endhighlight %}

---

## MySQL

This is an API used to get samples of one or more MySQL resources

### MySQL Sample Keys
{% highlight sh %}
Key name           Valid combinations

Cpu                c
I/O                i
Storage            s
Memory             m
Connection         n
Storage Percent    sp
{% endhighlight %}

### Fetch Samples from resources specified in idvs

#### Required Parameters:

idvs
: It is a list of ids(unique for every sql resource)

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| MySQL Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### CURL Command:

{% highlight sh %}
curl -XGET -s https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/mysql.json -H "Content-Type: application/json" -d '{"idvs":["idv1", "idv2"]}'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{
        "c":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "i":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "s":{
            "1484810160":[30448340,533795466],
            "1484810460":[30449340,533795466],
            "1484810760":[41448340,533795466],
            "1484811060":[41448340,533795466],
            "1484811360":[41478340,533795466]
        },
        "m":{
            "1484810160":0.441,
            "1484810460":0.538,
            "1484810760":0.263,
            "1484811060":0.544,
            "1484811360":0.623
        },
        "n":{
            "1484810160":[30448340,533795466],
            "1484810460":[30449340,533795466],
            "1484810760":[41448340,533795466],
            "1484811060":[41448340,533795466],
            "1484811360":[41478340,533795466]
        },
        "sp":{
            "1484810160":0.241,
            "1484810460":0.358,
            "1484810760":0.364,
            "1484811060":0.248,
            "1484811360":0.359
        }
    }
}
{% endhighlight %}

---

## MySQL Details

This is an API used to get detailed samples of a mysql resource

### MySQL Sample Keys
{% highlight sh %}
Key name           Valid combinations

Cpu                c
Compute Unit       l                    # limit
Compute Unit       p                    # percentage
Memory             m
I/O                i
Storage Percentage sp
Storage            sl                   # used and limit
Connections        n                    # active and failed
{% endhighlight %}

### Fetch Samples from resource specified by idv

#### Required Parameters:

idv
: unique id for a mysql resource

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| MySQL Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### Optional Parameters:

starttime
: integer value corresponding start time of timeframe for which samples are being fetched

endtime
: integer value corresponding end time of timeframe for which samples are being fetched

#### CURL Command:

{% highlight sh %}
curl -s 'https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/mysql_details.json?idv=<IDV1>&starttime=1484810160&endtime=1484811360'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{
        "c":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "l":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "p":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "m":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "i":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "sp":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "sl":{
            "1484810160":[30448340,533795466],
            "1484810460":[30449340,533795466],
            "1484810760":[41448340,533795466],
            "1484811060":[41448340,533795466],
            "1484811360":[41478340,533795466]
        },
        "n":{
            "1484810160":[533795466,30448340],
            "1484810220":[null,null],
            "1484810280":[null,null],
            "1484810340":[null,null],
            "1484810400":[null,null],
            "1484810460":[518838963,27407162]
        }
    }
}
{% endhighlight %}

---

## Postgres

This is an API used to get samples of one or more Postgres resources

### Postgres Sample Keys
{% highlight sh %}
Key name           Valid combinations

Cpu                c
I/O                i
Storage            s
Memory             m
Connection         n
Storage Percent    sp

{% endhighlight %}

### Fetch Samples from resources specified in idvs

#### Required Parameters:

idvs
: It is a list of ids(unique for every postgres resource)

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Postgres Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### CURL Command:

{% highlight sh %}
curl -XGET -s https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/postgres.json -H "Content-Type: application/json" -d '{"idvs":["idv1", "idv2"]}'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{
        "c":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "i":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "s":{
            "1484810160":[30448340,533795466],
            "1484810460":[30449340,533795466],
            "1484810760":[41448340,533795466],
            "1484811060":[41448340,533795466],
            "1484811360":[41478340,533795466]
        },
        "m":{
            "1484810160":0.441,
            "1484810460":0.538,
            "1484810760":0.263,
            "1484811060":0.544,
            "1484811360":0.623
        },
        "n":{
            "1484810160":[30448340,533795466],
            "1484810460":[30449340,533795466],
            "1484810760":[41448340,533795466],
            "1484811060":[41448340,533795466],
            "1484811360":[41478340,533795466]
        },
        "sp":{
            "1484810160":0.241,
            "1484810460":0.358,
            "1484810760":0.364,
            "1484811060":0.248,
            "1484811360":0.359
        }
    }
}
{% endhighlight %}

---

## Postgres Details

This is an API used to get detailed samples of a postgres resource

### Postgres Sample Keys
{% highlight sh %}
Key name           Valid combinations

Cpu                c
Compute Unit       l                    # limit
Compute Unit       p                    # percentage
Memory             m
I/O                i
Storage Percentage sp
Storage            sl                   # used and limit
Connections        n                    # active and failed
{% endhighlight %}

### Fetch Samples from resource specified by idv

#### Required Parameters:

idv
: unique id for a postgres resource

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Postgres Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### Optional Parameters:

starttime
: integer value corresponding start time of timeframe for which samples are being fetched

endtime
: integer value corresponding end time of timeframe for which samples are being fetched

#### CURL Command:

{% highlight sh %}
curl -s 'https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/postgres_details.json?idv=<IDV1>&starttime=1484810160&endtime=1484811360'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{
        "c":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "l":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "p":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "m":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "i":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "sp":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "sl":{
            "1484810160":[30448340,533795466],
            "1484810460":[30449340,533795466],
            "1484810760":[41448340,533795466],
            "1484811060":[41448340,533795466],
            "1484811360":[41478340,533795466]
        },
        "n":{
            "1484810160":[533795466,30448340],
            "1484810220":[null,null],
            "1484810280":[null,null],
            "1484810340":[null,null],
            "1484810400":[null,null],
            "1484810460":[518838963,27407162]
        }
    }
}
{% endhighlight %}

---

## Analysis Service

This is an API used to get samples of one or more Analysis service resources

### Analysis Service Sample Keys
{% highlight sh %}
Key name                      Valid combinations

QPU                           q
Memory                        m
Current connections           c
Query pool busy threads       qp
Command pool busy threads     cp
Processing pool               pp

{% endhighlight %}

### Fetch Samples from resources specified in idvs

#### Required Parameters:

idvs
: It is a list of ids(unique for every Analysis service resource)

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Analysis Service Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### CURL Command:

{% highlight sh %}
curl -XGET -s https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/analysis_service.json -H "Content-Type: application/json" -d '{"idvs":["idv1", "idv2"]}'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{
        "q":{
            "1524642180":0.0,
            "1524642240":0.0,
            "1524642300":0.25,
            "1524642360":0.0,
            "1524642420":0.25,
            "1524642480":0.25,
            "1524642540":0.5,
            "1524643860":0.0
        },
        "m":{
            "1524642180":612462592,
            "1524642240":606857216,
            "1524642300":607080448,
            "1524642360":607819776,
            "1524642420":610163712,
            "1524642480":611998720,
            "1524643860":609601536
        },
        "c":{"1524642180":[0.0,0.0],
            "1524642240":[0.0,0.0],
            "1524642300":[0.0,0.0],
            "1524642360":[0.0,0.0],
            "1524642420":[0.0,0.0],
            "1524642480":[0.0,0.0],
            "1524643860":[0.0,0.0]
        },
        "qp":{
            "1524642180":[0.0,1.0],
            "1524642240":[0.0,1.0],
            "1524642300":[0.0,1.0],
            "1524642360":[0.0,1.0],
            "1524642420":[0.0,1.0],
            "1524643860":[0.0,1.0]
         }
        "cp":{
            "1524642180":[0.0,1.0],
            "1524642240":[0.0,1.0],
            "1524642300":[0.0,1.0],
            "1524642360":[0.0,1.0],
            "1524642420":[0.0,1.0],
            "1524643860":[0.0,1.0]
         }
        "pp":{
            "1524642180":[0.0,1.0],
            "1524642240":[0.0,1.0],
            "1524642300":[0.0,1.0],
            "1524642360":[0.0,1.0],
            "1524642420":[0.0,1.0],
            "1524643860":[0.0,1.0]
         }
    }
}

{% endhighlight %}

---

## Analysis Service Details

This is an API used to get detailed samples of a Analysis resource

### Analysis Service Sample Keys
{% highlight sh %}
Key name                        Valid combinations

QPU                             q
Memory                          m
Connections                     c
Successful connections          cs
User sessions                   u
Query pool                      qp
Command pool                    cp
Processing Pool                 pp
Current clean price             ccp
Current clean memory            cm
Quota                           qt
Quota blocked                   qtb
Rows                            r
Long parsing                    l
Short parsing                   s
Memory Thrashing Metric         mt
Mashup engine qpu metric        meq
Mashup engine memory metric     mem

{% endhighlight %}

### Fetch Samples from resource specified by idv

#### Required Parameters:

idv
: unique id for a analysis service resource

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Analysis Service Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### Optional Parameters:

starttime
: integer value corresponding start time of timeframe for which samples are being fetched

endtime
: integer value corresponding end time of timeframe for which samples are being fetched

#### CURL Command:

{% highlight sh %}
curl -s 'https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/analysis_service_details.json?idv=<IDV1>&starttime=1484810160&endtime=1484811360'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV>":{
        "q":{
            "1524641040":0.25,
            "1524641100":0.0,
            "1524641160":0.5,
            "1524641220":0.75,
            "1524641280":0.25,
            "1524641340":0.0,
            "1524641400":0.0,
            "1524641460":0.0,
            "1524644460":0.25
        },
        "m":{
            "1524641040":[607687680,881798144,3219926016,2575039488,2570845184,2575039488,9453568,0],
            "1524641100":[609498112,892695552,3219926016,2575039488,2570845184,2575039488,9453568,0],
            "1524641160":[611751936,906274816,3219926016,2575039488,2570845184,2575039488,9453568,0],
            "1524641220":[608238592,884934656,3219926016,2575039488,2570845184,2575039488,9453568,0],
            "1524644280":[609553408,884589568,3219926016,2575039488,2570845184,2575039488,9453568,0],
            "1524644340":[611022848,893135872,3219926016,2575039488,2570845184,2575039488,9453568,0],
            "1524644400":[610465792,890216448,3219926016,2575039488,2570845184,2575039488,9453568,0],
            "1524644460":[611144704,894028800,3219926016,2575039488,2570845184,2575039488,9453568,0]
        },
        "c":{
            "1524641040":[0.0,0.0,0.0],
            "1524641100":[0.0,0.0,0.0],
            "1524641160":[0.0,0.0,0.0],
            "1524641220":[0.0,0.0,0.0],
            "1524641280":[0.0,0.0,0.0],
            "1524644340":[0.0,0.0,0.0],
            "1524644400":[0.0,0.0,0.0],
            "1524644460":[0.0,0.0,0.0]
        },
        "cs":{
            "1524641040":0.0,
            "1524641100":0.0,
            "1524641160":0.0,
            "1524641220":0.0,
            "1524641280":0.0,
            "1524643680":0.0,
            "1524643740":0.0,
            "1524644400":0.0,
            "1524644460":0.0
        },
        "u":{
            "1524641040":0.0,
            "1524641100":0.0,
            "1524641160":0.0,
            "1524641220":0.0,
            "1524641280":0.0,
            "1524641340":0.0,
            "1524641400":0.0,
            "1524644400":0.0,
            "1524644460":0.25
        },
        "qp":{
            "1524641040":[0.0,1.0,0.0],
            "1524641100":[0.0,1.0,0.0],
            "1524641160":[0.0,1.0,0.0],
            "1524641220":[0.0,1.0,0.0],
            "1524641280":[0.0,1.0,0.0],
            "1524641340":[0.0,1.0,0.0],
            "1524644280":[0.0,1.0,0.0],
            "1524644340":[0.0,1.0,0.0],
            "1524644400":[0.0,1.0,0.0],
            "1524644460":[0.0,1.0,0.0]
        },
        "cp":{
            "1524641040":[0.0,0.0,1.0],
            "1524641100":[0.0,0.0,1.0],
            "1524641160":[0.0,0.0,1.0],
            "1524641220":[0.0,0.0,1.0],
            "1524644220":[0.0,0.0,1.0],
            "1524644280":[0.0,0.0,1.0],
            "1524644340":[0.0,0.0,1.0],
            "1524644400":[0.0,0.0,1.0],
            "1524644460":[0.0,0.0,1.0]
        },
        "pp":{
            "1524641040":[0.0,0.0,0.0,0.0,1.0,1.0],
            "1524641100":[0.0,0.0,0.0,0.0,1.0,1.0],
            "1524641160":[0.0,0.0,0.0,0.0,1.0,1.0],
            "1524641220":[0.0,0.0,0.0,0.0,1.0,1.0],
            "1524641280":[0.0,0.0,0.0,0.0,1.0,1.0],
            "1524641700":[0.0,0.0,0.0,0.0,1.0,1.0],
            "1524641760":[0.0,0.0,0.0,0.0,1.0,1.0],
            "1524641820":[0.0,0.0,0.0,0.0,1.0,1.0],
            "1524641880":[0.0,0.0,0.0,0.0,1.0,1.0],
            "1524641940":[0.0,0.0,0.0,0.0,1.0,1.0],
            "1524642000":[0.0,0.0,0.0,0.0,1.0,1.0],
            "1524642060":[0.0,0.0,0.0,0.0,1.0,1.0],
            "1524644460":[0.0,0.0,0.0,0.0,1.0,1.0]
        },
        "ccp":{
            "1524641040":0.0,
            "1524641100":0.0,
            "1524641160":0.0,
            "1524641220":0.0,
            "1524641280":0.0,
            "1524641340":0.0,
            "1524641400":0.0,
            "1524641460":0.0,
            "1524644280":0.0,
            "1524644340":0.0,
            "1524644400":0.0,
            "1524644460":0.0
        },
        "cm":{
            "1524641040":[0,41877504],
            "1524641100":[0,41878528],
            "1524641160":[0,41878528],
            "1524641220":[0,41879552],
            "1524641280":[0,41879552],
            "1524641340":[0,41880576],
            "1524641400":[0,41881600],
            "1524644340":[0,41912320],
            "1524644400":[0,41914624],
            "1524644460":[0,41915392]
        },
        "qt":{
            "1524641040":0.0,
            "1524641100":0.0,
            "1524641160":0.0,
            "1524641220":0.0,
            "1524641280":0.0,
            "1524641340":0.0,
            "1524644340":0.0,
            "1524644400":0.0,
            "1524644460":0.0
        },
        "qtb":{
            "1524641040":0.0,
            "1524641100":0.0,
            "1524641160":0.0,
            "1524641220":0.0,
            "1524641280":0.0,
            "1524644280":0.0,
            "1524644340":0.0,
            "1524644400":0.0,
            "1524644460":0.0
        },
        "r":{
            "1524641040":[0.0,0.0,0.0],
            "1524641100":[0.0,0.0,0.0],
            "1524641160":[0.0,0.0,0.0],
            "1524641220":[0.0,0.0,0.0],
            "1524641280":[0.0,0.0,0.0],
            "1524641340":[0.0,0.0,0.0],
            "1524644340":[0.0,0.0,0.0],
            "1524644400":[0.0,0.0,0.0],
            "1524644460":[0.0,0.0,0.0]
        },
        "l":{
            "1524641040":[0.0,4.0,0.0],
            "1524641100":[0.0,4.0,0.0],
            "1524641160":[0.0,4.0,0.0],
            "1524641220":[0.0,4.0,0.0],
            "1524644220":[0.0,4.0,0.0],
            "1524644280":[0.0,4.0,0.0],
            "1524644340":[0.0,4.0,0.0],
            "1524644400":[0.0,4.0,0.0],
            "1524644460":[0.0,4.0,0.0]
        },
        "s":{
            "1524641040":[0.0,4.0,0.0],
            "1524641100":[0.0,4.0,0.0],
            "1524641160":[0.0,4.0,0.0],
            "1524641220":[0.0,4.0,0.0],
            "1524641280":[0.0,4.0,0.0],
            "1524641340":[0.0,4.0,0.0],
            "1524644340":[0.0,4.0,0.0],
            "1524644400":[0.0,4.0,0.0],
            "1524644460":[0.0,4.0,0.0]
        },
        "mt":{
            "1524641040":0.0,
            "1524641100":0.0,
            "1524641160":0.0,
            "1524641220":0.0,
            "1524641280":0.0,
            "1524644160":0.0,
            "1524644220":0.0,
            "1524644280":0.0,
            "1524644340":0.0,
            "1524644400":0.0,
            "1524644460":0.0
        },
        "meq":{
            "1524641040":0.0,
            "1524641100":0.0,
            "1524641160":0.0,
            "1524641220":0.0,
            "1524641280":0.0,
            "1524644160":0.0,
            "1524644220":0.0,
            "1524644280":0.0,
            "1524644340":0.0,
            "1524644400":0.0,
            "1524644460":0.0
        },
        "mem":{
            "1524641040":0,
            "1524641100":0,
            "1524641160":0,
            "1524641220":0,
            "1524641280":0,
            "1524644160":0,
            "1524644220":0,
            "1524644280":0,
            "1524644340":0,
            "1524644400":0,
            "1524644460":0
        }
    }
}
{% endhighlight %}

---

## Load balancer

This is an API used to get samples of one or more load balancer resources

### Load balancer Sample Keys
{% highlight sh %}
Key name            Valid combinations

VIP Endpoint        v
Dip Endpoint        d
Bytes               b
Packets             p
SYN Packets         s
SNAT connections    c

{% endhighlight %}

### Fetch Samples from resources specified in idvs

#### Required Parameters:

idvs
: It is a list of ids(unique for every load balancer resource)

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Load balancer Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### CURL Command:

{% highlight sh %}
curl -XGET -s https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/load_balancer.json -H "Content-Type: application/json" -d '{"idvs":["idv1", "idv2"]}'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{
        "v":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "d":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "b":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "p":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "s":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "c":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        }
    }
}
{% endhighlight %}

---

## Load balancer Details

This is an API used to get detailed samples of a load balancer resource

### Load balancer Sample Keys
{% highlight sh %}
Key name            Valid combinations

VIP Endpoint        v
Dip Endpoint        d
Bytes               b
Packets             p
SYN Packets         s
SNAT connections    c

{% endhighlight %}

### Fetch Samples from resource specified by idv

#### Required Parameters:

idv
: unique id for a load balancer resource

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Load balancer Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### Optional Parameters:

starttime
: integer value corresponding start time of timeframe for which samples are being fetched

endtime
: integer value corresponding end time of timeframe for which samples are being fetched

#### CURL Command:

{% highlight sh %}
curl -s 'https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/load_balancer_details.json?idv=<IDV1>&starttime=1484810160&endtime=1484811360'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{
        "v":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "d":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "b":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "p":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "s":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "c":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        }
    }
}
{% endhighlight %}

---

## Application gateway

This is an API used to get samples of one or more application gateway resources

### Application gateway Sample Keys
{% highlight sh %}
Key name            Valid combinations

Throughput          t

{% endhighlight %}

### Fetch Samples from resources specified in idvs

#### Required Parameters:

idvs
: It is a list of ids(unique for every application gateway resource)

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Application Gateway Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### CURL Command:

{% highlight sh %}
curl -XGET -s https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/application_gateway.json -H "Content-Type: application/json" -d '{"idvs":["idv1", "idv2"]}'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{
        "t":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        }
    }
}
{% endhighlight %}

---

## Application gateway Details

This is an API used to get detailed samples of a application gateway resource

### Application gateway Sample Keys
{% highlight sh %}
Key name            Valid combinations

Throughput          t

{% endhighlight %}

### Fetch Samples from resource specified by idv

#### Required Parameters:

idv
: unique id for a application gateway resource

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Application gateway Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### Optional Parameters:

starttime
: integer value corresponding start time of timeframe for which samples are being fetched

endtime
: integer value corresponding end time of timeframe for which samples are being fetched

#### CURL Command:

{% highlight sh %}
curl -s 'https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/application_gateway_details.json?idv=<IDV1>&starttime=1484810160&endtime=1484811360'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{
        "t":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        }
    }
}
{% endhighlight %}

---

## Virtual Network Gateway

This is an API used to get samples of one or more virtual network gateway resources

### Virtual Network Gateway Sample Keys
{% highlight sh %}
Key name                    Valid combinations

Bandwidth                   b
Tunnel Bytes                tb
Tunnel Packets              tp
Packet Drop                 d

{% endhighlight %}

### Fetch Samples from resources specified in idvs

#### Required Parameters:

idvs
: It is a list of ids(unique for every virtual network gateway resource)

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Virtual Network Gateway Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### CURL Command:

{% highlight sh %}
curl -XGET -s https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/virtual_network_gateway.json -H "Content-Type: application/json" -d '{"idvs":["idv1", "idv2"]}'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{
        "b":{
            "1484810160":0,
            "1484810460":1,
            "1484810760":1,
            "1484811060":0,
            "1484811360":1
        },
        "tb":{
            "1484810160":[0,0],
            "1484810460":[160,320],
            "1484810760":[0,0],
            "1484811060":[0,0],
            "1484811360":[160,320]
        },
        "tp":{
            "1484810160":[5,10],
            "1484810460":[0,0],
            "1484810760":[5,10],
            "1484811060":[0,0],
            "1484811360":[5,10]
        },
        "d":{
            "1484810160":[0,0],
            "1484810460":[0,0],
            "1484810760":[0,0],
            "1484811060":[0,0],
            "1484811360":[0,0]
        }
    }
}
{% endhighlight %}

---

## Virtual Network Gateway Details

This is an API used to get detailed samples of a virtual network gateway resource

### Virtual Network Gateway Sample Keys
{% highlight sh %}
Key name                    Valid combinations

Bandwidth                   b
Tunnel Bytes                tb
Tunnel Packets              tp
Packet Drop                 d

{% endhighlight %}

### Fetch Samples from resource specified by idv

#### Required Parameters:

idv
: unique id for a virtual network gateway resource

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Virtual Network Gateway Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### Optional Parameters:

starttime
: integer value corresponding start time of timeframe for which samples are being fetched

endtime
: integer value corresponding end time of timeframe for which samples are being fetched

#### CURL Command:

{% highlight sh %}
curl -s 'https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/virtual_network_gateway_details.json?idv=<IDV1>&starttime=1484810160&endtime=1484811360'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{
        "b":{
            "1484810160":0,
            "1484810460":1,
            "1484810760":1,
            "1484811060":0,
            "1484811360":1
        },
        "tb":{
            "1484810160":[0,0],
            "1484810460":[160,320],
            "1484810760":[0,0],
            "1484811060":[0,0],
            "1484811360":[160,320]
        },
        "tp":{
            "1484810160":[5,10],
            "1484810460":[0,0],
            "1484810760":[5,10],
            "1484811060":[0,0],
            "1484811360":[5,10]
        },
        "d":{
            "1484810160":[0,0],
            "1484810460":[0,0],
            "1484810760":[0,0],
            "1484811060":[0,0],
            "1484811360":[0,0]
        }
    }
}
{% endhighlight %}

---

## Express Route Circuit

This is an API used to get samples of one or more express route circuit resources

### Express Route Circuit Sample Keys
{% highlight sh %}
Key name            Valid combinations

Bits in             i
Bits out            o

{% endhighlight %}

### Fetch Samples from resources specified in idvs

#### Required Parameters:

idvs
: It is a list of ids(unique for every express route circuit resource)

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Express Route Circuit Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### CURL Command:

{% highlight sh %}
curl -XGET -s https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/express_route_circuit.json -H "Content-Type: application/json" -d '{"idvs":["idv1", "idv2"]}'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{
        "i":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "o":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        }
    }
}
{% endhighlight %}

---

## Express Route Circuit Details

This is an API used to get detailed samples of a express route circuit resource

### Express Route Circuit Sample Keys
{% highlight sh %}
Key name            Valid combinations

Bits in             i
Bits out            o

{% endhighlight %}

### Fetch Samples from resource specified by idv

#### Required Parameters:

idv
: unique id for a express route circuit resource

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Express Route Circuit Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### Optional Parameters:

starttime
: integer value corresponding start time of timeframe for which samples are being fetched

endtime
: integer value corresponding end time of timeframe for which samples are being fetched

#### CURL Command:

{% highlight sh %}
curl -s 'https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/express_route_circuit_details.json?idv=<IDV1>&starttime=1484810160&endtime=1484811360'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{
        "i":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "o":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        }
    }
}
{% endhighlight %}

---

## Traffic Manager Profile

This is an API used to get samples of one or more traffic manager profile resources

### Traffic Manager Profile Sample Keys
{% highlight sh %}
Key name               Valid combinations

Qps By Endpoint        q
Endpoint status        s

{% endhighlight %}

### Fetch Samples from resources specified in idvs

#### Required Parameters:

idvs
: It is a list of ids(unique for every traffic manager profile resource)

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Traffic Manager Profile Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### CURL Command:

{% highlight sh %}
curl -XGET -s https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/traffic_manager_profile.json -H "Content-Type: application/json" -d '{"idvs":["idv1", "idv2"]}'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{
        "q":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "s":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        }
    }
}
{% endhighlight %}

---

## Traffic Manager Profile Details

This is an API used to get detailed samples of a traffic manager profile resource

### Traffic Manager Profile Sample Keys
{% highlight sh %}
Key name               Valid combinations

Qps By Endpoint        q
Endpoint status        s

{% endhighlight %}

### Fetch Samples from resource specified by idv

#### Required Parameters:

idv
: unique id for a traffic manager profile resource

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Traffic Manager Profile Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### Optional Parameters:

starttime
: integer value corresponding start time of timeframe for which samples are being fetched

endtime
: integer value corresponding end time of timeframe for which samples are being fetched

#### CURL Command:

{% highlight sh %}
curl -s 'https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/traffic_manager_profile_details.json?idv=<IDV1>&starttime=1484810160&endtime=1484811360'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{
        "q":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "s":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        }
    }
}
{% endhighlight %}

---

## Server Farm

This is an API used to get samples of one or more server farm resources

### Server Farm Sample Keys
{% highlight sh %}
Key name            Valid combinations

CPU                 c
Memory              m
Disk                d
Http                h
Bytes               b

{% endhighlight %}

### Fetch Samples from resources specified in idvs

#### Required Parameters:

idvs
: It is a list of ids(unique for every server farm resource)

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Server Farm Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### CURL Command:

{% highlight sh %}
curl -XGET -s https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/server_farm.json -H "Content-Type: application/json" -d '{"idvs":["idv1", "idv2"]}'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{
        "c":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "m":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "b":{
            "1484810160":[0,0],
            "1484810460":[0,0],
            "1484810760":[0,0],
            "1484811060":[0,0],
            "1484811360":[0,0]
        },
        "d":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":1,
            "1484811060":0,
            "1484811360":0
        },
        "h":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        }
    }
}
{% endhighlight %}

---

## Server Farm Details

This is an API used to get detailed samples of a server farm resource

### Server Farm Sample Keys
{% highlight sh %}
Key name            Valid combinations

CPU                 c
Memory              m
Disk                d
Http                h
Bytes               b

{% endhighlight %}

### Fetch Samples from resource specified by idv

#### Required Parameters:

idv
: unique id for a server farm resource

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Server Farm Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### Optional Parameters:

starttime
: integer value corresponding start time of timeframe for which samples are being fetched

endtime
: integer value corresponding end time of timeframe for which samples are being fetched

#### CURL Command:

{% highlight sh %}
curl -s 'https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/server_farm_details.json?idv=<IDV1>&starttime=1484810160&endtime=1484811360'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{
        "c":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "m":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "b":{
            "1484810160":[0,0],
            "1484810460":[0,0],
            "1484810760":[0,0],
            "1484811060":[0,0],
            "1484811360":[0,0]
        },
        "d":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":1,
            "1484811060":0,
            "1484811360":0
        },
        "h":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        }
    }
}
{% endhighlight %}

---

## Site

This is an API used to get samples of one or more site resources

### Site Sample Keys
{% highlight sh %}
Key name                 Valid combinations

CPU                      c
Requests                 r
Bytes                    b
Http2xx                  h2
Http4xx                  h4
Average response time    a

{% endhighlight %}

### Fetch Samples from resources specified in idvs

#### Required Parameters:

idvs
: It is a list of ids(unique for every site resource)

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| SiteResource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### CURL Command:

{% highlight sh %}
curl -XGET -s https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/site.json -H "Content-Type: application/json" -d '{"idvs":["idv1", "idv2"]}'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{
        "a":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "b":{
            "1484810160":[0, 0],
            "1484810460":[0, 0],
            "1484810760":[0, 0],
            "1484811060":[0, 0],
            "1484811360":[0, 0]
        },
        "c":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "h2":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "h4":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "r":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        }
    }
}
{% endhighlight %}

---

## Site Details

This is an API used to get detailed samples of a site resource

### Site Sample Keys
{% highlight sh %}
Key name                 Valid combinations

CPU                      c
Requests                 r
Bytes                    b
Http1xx                  h1
Http2xx                  h2
Http3xx                  h3
Http4xx                  h4
Http5xx                  h5
Memory                   m
Average response time    a

{% endhighlight %}

### Fetch Samples from resource specified by idv

#### Required Parameters:

idv
: unique id for a site resource

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Site Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### Optional Parameters:

starttime
: integer value corresponding start time of timeframe for which samples are being fetched

endtime
: integer value corresponding end time of timeframe for which samples are being fetched

#### CURL Command:

{% highlight sh %}
curl -s 'https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/site_details.json?idv=<IDV1>&starttime=1484810160&endtime=1484811360'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{
        "a":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "b":{
            "1484810160":[0,0],
            "1484810460":[0,0],
            "1484810760":[0,0],
            "1484811060":[0,0],
            "1484811360":[0,0]
        },
        "c":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "h1":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "h2":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "h3":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "h4":{
            "1484810160":[0,0,0,0],
            "1484810460":[0,0,0,0],
            "1484810760":[0,0,0,0],
            "1484811060":[0,0,0,0],
            "1484811360":[0,0,0,0]
        },
        "h5":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "m":{
            "1484810160":[0,0],
            "1484810460":[0,0],
            "1484810760":[0,0],
            "1484811060":[0,0],
            "1484811360":[0,0]
        },
        "r":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        }
    }
}
{% endhighlight %}

---

## Function site

This is an API used to get samples of one or more function site resources

### Function site Sample Keys
{% highlight sh %}
Key name                    Valid combinations

Bytes                       b
Http5xx                     h
Memory                      m
Function execution units    fu
Function execution count    fc

{% endhighlight %}

### Fetch Samples from resources specified in idvs

#### Required Parameters:

idvs
: It is a list of ids(unique for every function site resource)

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Function site Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### CURL Command:

{% highlight sh %}
curl -XGET -s https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/function_site.json -H "Content-Type: application/json" -d '{"idvs":["idv1", "idv2"]}'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{
        "b":{
            "1484810160":[0,0],
            "1484810460":[0,0],
            "1484810760":[0,0],
            "1484811060":[0,0],
            "1484811360":[0,0]
        },
        "h":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "m":{
            "1484810160":[0,0],
            "1484810460":[0,0],
            "1484810760":[0,0],
            "1484811060":[0,0],
            "1484811360":[0,0]
        },
        "fu":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "fc":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        }
    }
}
{% endhighlight %}

---

## Function site Details

This is an API used to get detailed samples of a function site resource

### Function site Sample Keys
{% highlight sh %}
Key name                    Valid combinations

Bytes                       b
Http5xx                     h
Memory                      m
Function execution units    fu
Function execution count    fc
Connections                 c

{% endhighlight %}

### Fetch Samples from resource specified by idv

#### Required Parameters:

idv
: unique id for a function site resource

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Function site Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### Optional Parameters:

starttime
: integer value corresponding start time of timeframe for which samples are being fetched

endtime
: integer value corresponding end time of timeframe for which samples are being fetched

#### CURL Command:

{% highlight sh %}
curl -s 'https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/function_site_details.json?idv=<IDV1>&starttime=1484810160&endtime=1484811360'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{
        "b":{
            "1484810160":[0,0],
            "1484810460":[0,0],
            "1484810760":[0,0],
            "1484811060":[0,0],
            "1484811360":[0,0]
        },
        "h":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "m":{
            "1484810160":[0,0],
            "1484810460":[0,0],
            "1484810760":[0,0],
            "1484811060":[0,0],
            "1484811360":[0,0]
        },
        "c":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "fu":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "fc":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        }
    }
}
{% endhighlight %}

---

## Slot

This is an API used to get samples of one or more slot resources

### Slot Sample Keys
{% highlight sh %}
Key name                 Valid combinations

CPU                      c
Requests                 r
Bytes                    b
Http2xx                  h2
Http4xx                  h4
Average response time    a

{% endhighlight %}

### Fetch Samples from resources specified in idvs

#### Required Parameters:

idvs
: It is a list of ids(unique for every slot resource)

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Slot Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### CURL Command:

{% highlight sh %}
curl -XGET -s https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/slot.json -H "Content-Type: application/json" -d '{"idvs":["idv1", "idv2"]}'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{
        "a":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "b":{
            "1484810160":[0, 0],
            "1484810460":[0, 0],
            "1484810760":[0, 0],
            "1484811060":[0, 0],
            "1484811360":[0, 0]
        },
        "c":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "h2":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "h4":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "r":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        }
    }
}
{% endhighlight %}

---

## Slot Details

This is an API used to get detailed samples of a slot resource

### Slot Sample Keys
{% highlight sh %}
Key name                   Valid combinations

CPU                        c
Requests                   r
Bytes                      b
Http1xx                    h1
Http2xx                    h2
Http3xx                    h3
Http4xx                    h4
Http5xx                    h5
Memory                     m
Average response time      a

{% endhighlight %}

### Fetch Samples from resource specified by idv

#### Required Parameters:

idv
: unique id for a slot resource

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Slot Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### Optional Parameters:

starttime
: integer value corresponding start time of timeframe for which samples are being fetched

endtime
: integer value corresponding end time of timeframe for which samples are being fetched

#### CURL Command:

{% highlight sh %}
curl -s 'https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/slot_details.json?idv=<IDV1>&starttime=1484810160&endtime=1484811360'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{
        "a":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "b":{
            "1484810160":[0,0],
            "1484810460":[0,0],
            "1484810760":[0,0],
            "1484811060":[0,0],
            "1484811360":[0,0]
        },
        "c":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "h1":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "h2":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "h3":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "h4":{
            "1484810160":[0,0,0,0],
            "1484810460":[0,0,0,0],
            "1484810760":[0,0,0,0],
            "1484811060":[0,0,0,0],
            "1484811360":[0,0,0,0]
        },
        "h5":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "m":{
            "1484810160":[0,0],
            "1484810460":[0,0],
            "1484810760":[0,0],
            "1484811060":[0,0],
            "1484811360":[0,0]
        },
        "r":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        }
    }
}
{% endhighlight %}

---

## Function slot

This is an API used to get samples of one or more function slot resources

### Function slot Sample Keys
{% highlight sh %}
Key name                    Valid combinations

Bytes                       b
Http5xx                     h
Memory                      m
Function execution units    fu
Function execution count    fc

{% endhighlight %}

### Fetch Samples from resources specified in idvs

#### Required Parameters:

idvs
: It is a list of ids(unique for every function slot resource)

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Function slot Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### CURL Command:

{% highlight sh %}
curl -XGET -s https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/function_slot.json -H "Content-Type: application/json" -d '{"idvs":["idv1", "idv2"]}'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{
        "b":{
            "1484810160":[0,0],
            "1484810460":[0,0],
            "1484810760":[0,0],
            "1484811060":[0,0],
            "1484811360":[0,0]
        },
        "h":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "m":{
            "1484810160":[0,0],
            "1484810460":[0,0],
            "1484810760":[0,0],
            "1484811060":[0,0],
            "1484811360":[0,0]
        },
        "fu":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "fc":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        }
    }
}
{% endhighlight %}

---

## Function slot Details

This is an API used to get detailed samples of a function slot resource

### Function slot Sample Keys
{% highlight sh %}
Key name                    Valid combinations

Bytes                       b
Http5xx                     h
Memory                      m
Function execution units    fu
Function execution count    fc
Connections                 c

{% endhighlight %}

### Fetch Samples from resource specified by idv

#### Required Parameters:

idv
: unique id for a function slot resource

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Function slot Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### Optional Parameters:

starttime
: integer value corresponding start time of timeframe for which samples are being fetched

endtime
: integer value corresponding end time of timeframe for which samples are being fetched

#### CURL Command:

{% highlight sh %}
curl -s 'https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/function_slot_details.json?idv=<IDV1>&starttime=1484810160&endtime=1484811360'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{
        "b":{
            "1484810160":[0,0],
            "1484810460":[0,0],
            "1484810760":[0,0],
            "1484811060":[0,0],
            "1484811360":[0,0]
        },
        "h":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "m":{
            "1484810160":[0,0],
            "1484810460":[0,0],
            "1484810760":[0,0],
            "1484811060":[0,0],
            "1484811360":[0,0]
        },
        "c":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "fu":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        },
        "fc":{
            "1484810160":0,
            "1484810460":0,
            "1484810760":0,
            "1484811060":0,
            "1484811360":0
        }
    }
}
{% endhighlight %}

---
<!---
## Network interface

This is an API used to get samples of one or more network interface resources

### Network interface Sample Keys
{% highlight sh %}
Key name                    Valid combinations

Bytes                       b
Packets                     p

{% endhighlight %}

### Fetch Samples from resources specified in idvs

#### Required Parameters:

idvs
: It is a list of ids(unique for every network interface resource)

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Network interface Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### CURL Command:

{% highlight sh %}
curl -XGET -s https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/network_interface.json -H "Content-Type: application/json" -d '{"idvs":["idv1", "idv2"]}'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{

    }
}
{% endhighlight %}

---

## Network interface Details

This is an API used to get detailed samples of a network interface resource

### Network interface Sample Keys
{% highlight sh %}
Key name                    Valid combinations

Bytes                       b
Packets                     p

{% endhighlight %}

### Fetch Samples from resource specified by idv

#### Required Parameters:

idv
: unique id for a network interface resource

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Network interface Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### Optional Parameters:

starttime
: integer value corresponding start time of timeframe for which samples are being fetched

endtime
: integer value corresponding end time of timeframe for which samples are being fetched

#### CURL Command:

{% highlight sh %}
curl -s 'https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/network_interface_details.json?idv=<IDV1>&starttime=1484810160&endtime=1484811360'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{

    }
}
{% endhighlight %}

---

## Public Ip Address

This is an API used to get samples of one or more public ip address resources

### Public Ip Address Sample Keys
{% highlight sh %}
Key name                    Valid combinations

VIP Availability            v
Byte count                  bc
Packet count                pc
Syn packet count            sc

{% endhighlight %}

### Fetch Samples from resources specified in idvs

#### Required Parameters:

idvs
: It is a list of ids(unique for every public ip address resource)

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Public Ip Address Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### CURL Command:

{% highlight sh %}
curl -XGET -s https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/public_ip_address.json -H "Content-Type: application/json" -d '{"idvs":["idv1", "idv2"]}'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{

    }
}
{% endhighlight %}

---

## Public Ip Address Details

This is an API used to get detailed samples of a public ip address resource

### Public Ip Address Sample Keys
{% highlight sh %}
Key name                    Valid combinations

Packets                     p
TCP Packets                 tp
UDP Packets                 up
Bytes                       b
TCP bytes                   tb
UDP bytes                   ub
DDOS trigger packets        t
If under attack             a
VIP availability            v
bytes count                 c

{% endhighlight %}

### Fetch Samples from resource specified by idv

#### Required Parameters:

idv
: unique id for a public ip address resource

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Public Ip Address Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### Optional Parameters:

starttime
: integer value corresponding start time of timeframe for which samples are being fetched

endtime
: integer value corresponding end time of timeframe for which samples are being fetched

#### CURL Command:

{% highlight sh %}
curl -s 'https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/public_ip_address_details.json?idv=<IDV1>&starttime=1484810160&endtime=1484811360'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{

    }
}
{% endhighlight %}

---

## Virtual network

This is an API used to get samples of one or more virtual network resources

### Virtual network Sample Keys
{% highlight sh %}
Key name                    Valid combinations

Packets in                  b
Packets out                 h

{% endhighlight %}

### Fetch Samples from resources specified in idvs

#### Required Parameters:

idvs
: It is a list of ids(unique for every virtual network resource)

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Virtual network Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### CURL Command:

{% highlight sh %}
curl -XGET -s https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/virtual_network.json -H "Content-Type: application/json" -d '{"idvs":["idv1", "idv2"]}'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{

    }
}
{% endhighlight %}

---

## Virtual network Details

This is an API used to get detailed samples of a virtual network resource

### Virtual network Sample Keys
{% highlight sh %}
Key name                    Valid combinations

Packets in                  b
Packets out                 h

{% endhighlight %}

### Fetch Samples from resource specified by idv

#### Required Parameters:

idv
: unique id for a virtual network resource

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Virtual network Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### Optional Parameters:

starttime
: integer value corresponding start time of timeframe for which samples are being fetched

endtime
: integer value corresponding end time of timeframe for which samples are being fetched

#### CURL Command:

{% highlight sh %}
curl -s 'https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/virtual_network_details.json?idv=<IDV1>&starttime=1484810160&endtime=1484811360'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{

    }
}
{% endhighlight %}

---

## Multi role pool

This is an API used to get samples of one or more multi role pool resources

### Multi role pool Sample Keys
{% highlight sh %}
Key name                    Valid combinations

Request                     r
Http2xx                     h2
Http4xx                     h4
Average response time       a
CPU                         c
Memory                      m

{% endhighlight %}

### Fetch Samples from resources specified in idvs

#### Required Parameters:

idvs
: It is a list of ids(unique for every multi role pool resource)

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Multi role pool Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### CURL Command:

{% highlight sh %}
curl -XGET -s https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/multi_role_pool.json -H "Content-Type: application/json" -d '{"idvs":["idv1", "idv2"]}'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{

    }
}
{% endhighlight %}

---

## Multi role pool Details

This is an API used to get detailed samples of a multi role pool resource

### Multi role pool Sample Keys
{% highlight sh %}
Key name                    Valid combinations

Requests                          r
Bytes                             b
Http1xx                           h1
Http2xx                           h2
Http3xx                           h3
Http4xx                           h4
Http5xx                           h5
Average response time             a
CPU                               c
Memory                            m
Disk                              d
Http queue                        q
Front ends                        f
Service plan instance workers     s

{% endhighlight %}

### Fetch Samples from resource specified by idv

#### Required Parameters:

idv
: unique id for a multi role pool resource

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Multi role pool Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### Optional Parameters:

starttime
: integer value corresponding start time of timeframe for which samples are being fetched

endtime
: integer value corresponding end time of timeframe for which samples are being fetched

#### CURL Command:

{% highlight sh %}
curl -s 'https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/multi_role_pool_details.json?idv=<IDV1>&starttime=1484810160&endtime=1484811360'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{

    }
}
{% endhighlight %}

---

## Worker pool

This is an API used to get samples of one or more worker pool resources

### Worker pool Sample Keys
{% highlight sh %}
Key name                    Valid combinations

Worker total                wt
Worker average              wa
Worker used                 wu
CPU                         c
Memory                      m

{% endhighlight %}

### Fetch Samples from resources specified in idvs

#### Required Parameters:

idvs
: It is a list of ids(unique for every worker pool resource)

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Worker pool Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### CURL Command:

{% highlight sh %}
curl -XGET -s https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/worker_pool.json -H "Content-Type: application/json" -d '{"idvs":["idv1", "idv2"]}'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{

    }
}
{% endhighlight %}

---

## Worker pool Details

This is an API used to get detailed samples of a worker pool resource

### Worker pool Sample Keys
{% highlight sh %}
Key name                    Valid combinations

Worker total                wt
Worker average              wa
Worker used                 wu
CPU                         c
Memory                      m

{% endhighlight %}

### Fetch Samples from resource specified by idv

#### Required Parameters:

idv
: unique id for a worker pool resource

*idv is a combination of azure\| Azure Account Id \| Subscription ID \| Resource Group ID \| Worker pool Resource ID\|

These IDs are unique IDs assigned by Uptime Cloud Monitor. Eg. azure \| 1 \| 13 \| 221 \| 942 \|

#### Optional Parameters:

starttime
: integer value corresponding start time of timeframe for which samples are being fetched

endtime
: integer value corresponding end time of timeframe for which samples are being fetched

#### CURL Command:

{% highlight sh %}
curl -s 'https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/worker_pool_details.json?idv=<IDV1>&starttime=1484810160&endtime=1484811360'
{% endhighlight %}

#### CURL Response:

{% highlight sh %}
{
    "<IDV1>":{

    }
}
{% endhighlight %}

---
-->