---
layout: default
title: Azure Accounts
---

## Overview

Each of the API commands described here relate to retrieving, adding and deleting one or more Azure Accounts being monitored at your site.
Each Azure Account is completely described by a Hash.

### The Azure Account Hash

An example JSON-encoded Azure Account Hash is shown below:

{% highlight sh %}
{
    "id":1,                                      # Azure Account ID (Assigned by Uptime Cloud Monitor)
    "tenant_id":"dummy_tenant_id",               # Azure account tenant id
    "client_id":"dummy_client_id",               # Azure account client id
    "client_secret":"dummy_client_secret",       # Azure account client secret
    "label":"Azure",                             # Label of Azure Account to show on Uptime Cloud Monitor UI
    "tags":[],                                   # Tags associated with this Azure account
    "reading_enabled":true                       # If account monitoring is enabled
}
{% endhighlight %}

------

## Index

Retrieve a list of all of your Azure Accounts.

#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U https://api.copperegg.com/v2/azure/accounts.json

curl -s https://<APIKEY>:U@api.copperegg.com/v2/azure/accounts.json
{% endhighlight %}


#### CURL Response:
Response is a JSON-encoded list of AWS Account Hashes and stats (contains total no of accounts).

{% highlight sh %}
{
    "accounts":[
                   {
                       "id":1,
                       "tenant_id":"dummy_tenant_id",
                       "client_id":"dummy_client_id",
                       "client_secret":"dummy_client_secret",
                       "label":"Azure",
                       "tags":[],
                       "reading_enabled":true
                   }
               ],
    "stats":{
                "total":1
            }
}
{% endhighlight %}

------

## Create

Add a new AWS Account.

#### Required parameters:

client_id
: Client Id string for Azure Account

tenant_id
: Tenant Id string for Azure Account

client_secret
: Client Secret string for Azure Account

label
: Label is a Describer String to be shown on UI

#### Optional parameters:

tags
: Tags to apply to this Azure Account, If not specified no tags will be applied.

##### Curl Command
{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/azure/accounts.json -d '{ "tenant_id":"<Tenant ID>","client_id":"<Client ID>","client_secret":"<Client Secret>","label":"<LABEL>","tags":["<tag1>", "<tag2>"] }'
{% endhighlight %}

##### Curl Response
{% highlight sh %}
{
    "id":1,
    "tenant_id":<Tenant ID>,
    "client_id":<Client ID>,
    "client_secret":<Client Secret>,
    "label":"Azure",
    "tags":["<tag1>","<tag2>"],
    "reading_enabled":true
}
{% endhighlight %}

------

## Update
Update specified Azure Account Hash

#### Required parameters:

Azure_Account_ID
:  ID of Azure Account which is to be updated

*All params are same as create, required only params those need to modify.

#### Curl Command

{% highlight sh %}
curl -s -XPUT -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/azure/accounts/<Azure_Account_id>.json -d '{ "tenant_id":"<Tenant ID>","client_id":"<Client ID>","client_secret":"<Client Secret>","label":"<LABEL>","tags":["<tag1>", "<tag3>"] }'
{% endhighlight %}

#### Curl Response
{% highlight sh %}
{
    "id":1,
    "tenant_id":<Tenant ID>,
    "client_id":<Client ID>,
    "client_secret":<Client Secret>,
    "label":"Azure",
    "tags":["<tag1>","<tag3>"],
    "reading_enabled":true
}
{% endhighlight %}

------

## Delete
Delete the specified Azure Account Hash

#### Required parameters:

Azure_Account_ID
: ID of Azure Account which is to be deleted

#### Curl Command

{% highlight sh %}
curl -s -XDELETE -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/azure/accounts/<Azure_Account_id>.json
{% endhighlight %}

#### Curl Response

{% highlight sh %}
{}
{% endhighlight %}
