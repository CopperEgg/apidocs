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

{% highlight ruby %}
{
  "subscriptions": {
    "count": 1,
    "dummy_subscription_name_1": {
      "dummy_resource_type_1": 1,
      "dummy_resource_type_2": 1
    }
  },
  "metrics": {
    "resource_type_1": {
      "objects": 1,
      "metrics": 1
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

*idv is a combination of Azure Account Id \| Subscription ID \| Resource Group ID \| VM Resource ID\|

eg. 1\|af33c92c-7b53-4c65-9fec-8b606790afa7\|resource-group-1\|test-vm\|

#### CURL Command:

{% highlight sh %}

curl -XGET -s 'https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/vm.json -H "Content-Type: application/json" -d '{"idvs":["idv1", "idv2"]}'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
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

*idv is a combination of Azure Account Id \| Subscription ID \| Resource Group ID \| VM Resource ID\|

eg. 1\|af33c92c-7b53-4c65-9fec-8b606790afa7\|resource-group-1\|test-vm\|

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

{% highlight ruby %}
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
{% endhighlight %}

### Fetch Samples from resources specified in idvs

#### Required Parameters:

idvs
: It is a list of ids(unique for every sql resource)

*idv is a combination of Azure Account Id \| Subscription ID \| Resource Group ID \| SQL Resource ID\|

eg. 1\|af33c92c-7b53-4c65-9fec-8b606790afa7\|resource-group-1\|test-mssql-1\|

#### CURL Command:

{% highlight sh %}
curl -XGET -s https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/sql.json -H "Content-Type: application/json" -d '{"idvs":["idv1", "idv2"]}'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
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

*idv is a combination of Azure Account Id \| Subscription ID \| Resource Group ID \| SQL Resource ID\|

eg. 1\|af33c92c-7b53-4c65-9fec-8b606790afa7\|resource-group-1\|test-mssql-1\|

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

{% highlight ruby %}
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
{% endhighlight %}

### Fetch Samples from resources specified in idvs

#### Required Parameters:

idvs
: It is a list of ids(unique for every sql resource)

*idv is a combination of Azure Account Id \| Subscription ID \| Resource Group ID \| SQL Resource ID\|

eg. 1\|af33c92c-7b53-4c65-9fec-8b606790afa7\|resource-group-1\|test-mysql\|

#### CURL Command:

{% highlight sh %}
curl -XGET -s https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/mysql.json -H "Content-Type: application/json" -d '{"idvs":["idv1", "idv2"]}'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
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

*idv is a combination of Azure Account Id \| Subscription ID \| Resource Group ID \| MySQL Resource ID\|

eg. 1\|af33c92c-7b53-4c65-9fec-8b606790afa7\|resource-group-1\|test-mysql\|

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

{% highlight ruby %}
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
{% endhighlight %}

### Fetch Samples from resources specified in idvs

#### Required Parameters:

idvs
: It is a list of ids(unique for every postgres resource)

*idv is a combination of Azure Account Id \| Subscription ID \| Resource Group ID \| Postgres Resource ID\|

eg. 1\|af33c92c-7b53-4c65-9fec-8b606790afa7\|resource-group-1\|test-postgres\|

#### CURL Command:

{% highlight sh %}
curl -XGET -s https://<APIKEY>:U@api.copperegg.com/v2/azure/samples/postgres.json -H "Content-Type: application/json" -d '{"idvs":["idv1", "idv2"]}'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
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

*idv is a combination of Azure Account Id \| Subscription ID \| Resource Group ID \| Postgres Resource ID\|

eg. 1\|af33c92c-7b53-4c65-9fec-8b606790afa7\|resource-group-1\|test-postgres\|

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

{% highlight ruby %}
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
