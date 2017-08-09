---
layout: default
title: Azure Subscriptions
---

## Overview

Each of the API commands described here relate to retrieving and updating one or more Azure Subscriptions being monitored at your site.
Each Azure Subscription is completely described by a Hash.

### The Azure Subscription Hash

An example JSON-encoded Azure Subscription Hash is shown below:

{% highlight ruby %}
{
    "id":1,                                         # Azure Subscription ID (Assigned by Uptime Cloud Monitor)
    "azure_account_id":1,                           # Azure account id of the subscription
    "unique_id":"/subscriptions/dummy_unique_id",   # A unique identifier for a subscription
    "name":"dummy_name",                            # Name of the Azure Subscription
    "reading_enabled":true,                         # If monitoring is enabled for the subscription
    "state":"dummy_state",                          # State of the Azure Subscription
    "attrs":{...}                                   # Attributes related to this azure subscription
}
{% endhighlight %}

------

## Index

Retrieve a list of all of your Azure Subscriptions for an Azure Account.

#### Required Parameters:

Azure_Account_ID
:  ID of Azure Account for which subscriptions are being fetched

#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U https://api.copperegg.com/v2/azure/accounts/<Azure_Account_ID>/subscriptions.json

curl -s https://<APIKEY>:U@api.copperegg.com/v2/azure/accounts/<Azure_Account_ID>/subscriptions.json
{% endhighlight %}


#### CURL Response:
Response is a JSON-encoded list of Azure Subscription Hashes and stats (contains total no of subscriptions for the account).

{% highlight ruby %}
{
    "subscriptions":[
        {
            "id":1,
            "azure_account_id":1,
            "unique_id":"dummy_unique_id",
            "name":"dummy_name",
            "reading_enabled":true,
            "state":"dummy_state",
            "attrs":{...}
        }
    ],
    "stats":{
        "total":1
    }
}
{% endhighlight %}

------

## Update

Updates an existing Azure Subscription.
: * Only reading_enabled attribute is allowed to be modified for an azure subscription.

#### Required Parameters:

Azure_Account_ID
:  ID of Azure Account for which subscription is to be updated

Azure_Subscription_ID
:  ID of Azure Subscription to be updated

reading_enbled
: If monitoring is enabled for the subscription

##### Curl Command
{% highlight sh %}
curl -s -XPUT -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/azure/accounts/<Azure_Account_ID>/subscriptions/<Azure_Subscription_ID>.json -d '{ "reading_enabled":"false" }'
{% endhighlight %}

##### Curl Response
{% highlight ruby %}
{
    "id":1,
    "azure_account_id":1,
    "unique_id":"dummy_unique_id",
    "name":"dummy_name",
    "reading_enabled":false,
    "state":"dummy_state",
    "attrs":{...}
}
{% endhighlight %}

------
