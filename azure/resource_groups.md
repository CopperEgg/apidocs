---
layout: default
title: Azure Resource Groups
---

## Overview

Each of the API commands described here relate to retrieving and updating one or more Azure Resource Groups being monitored at your site.
Each Azure Resource Group is completely described by a Hash.

### The Azure Resource Group Hash

An example JSON-encoded Azure Resource Group Hash is shown below:

{% highlight ruby %}
{
    "id":1,                                         # Azure Resource ID(Assigned by Uptime Cloud Monitor)
    "azure_subscription_unique_id":"/subscriptions/dummy_subscription_id",                       # Azure subscription unique id of the subscription of the resource
    "name":"dummy_name",                            # Name of the Azure Resource Group
    "unique_id":"/subscriptions/dummy_subscription_id/resourceGroups/dummy_resource_group_id",   # A unique identifier for the resource group
    "location":"dummy_location",                    # Location of the resource group
    "reading_enabled":true,                         # If monitoring is enabled for the resource group
    "attrs":{...}                                   # Attributes related to this azure resource group
}
{% endhighlight %}

------

## Index

Retrieve a list of all of your Azure Resource Groups for an Azure Subscription with their resources.

#### Required Parameters:

Azure_Account_ID
:  ID of Azure Account for which resource groups are being fetched

Azure_Subscription_ID
:  ID of Azure Subscription for which resource groups are being fetched

#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U https://api.copperegg.com/v2/azure/accounts/<Azure_Account_ID>/subscriptions/<Azure_Subscription_ID>/resource_groups.json

curl -s https://<APIKEY>:U@api.copperegg.com/v2/azure/accounts/<Azure_Account_ID>/subscriptions/<Azure_Subscription_ID>/resource_groups.json
{% endhighlight %}


#### CURL Response:
Response is a JSON-encoded list of Azure Resource Group Hashes and stats(contains total no of resource groups for the subscription).

{% highlight ruby %}
{
    "resource_groups":[
        {
            "id":1,
            "azure_subscription_unique_id":"/subscriptions/dummy_subscription_id",
            "name":"dummy_name",
            "unique_id":"/subscriptions/dummy_subscription_id/resourceGroups/dummy_resource_group_id",
            "location":"dummy_location",
            "reading_enabled":true,
            "attrs":{...},
            "resources":[
                {...}
            ]
        }
    ],
    "stats":{
        "total":1
    }
}
{% endhighlight %}

------

## Update

Updates an existing Azure Resource Group.
: * Only reading_enabled attribute is allowed to be modified for an azure resource group.

#### Required Parameters:

Azure_Account_ID
:  ID of Azure Account for which resource group is to be updated

Azure_Subscription_ID
:  ID of Azure Subscription for which resource group is to be updated

Azure_Resource_Group_ID
:  ID of Azure Resource Group to be updated

reading_enbled
: If monitoring is enabled for the resource group

##### Curl Command
{% highlight sh %}
curl -s -XPUT -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/azure/accounts/<Azure_Account_ID>/subscriptions/<Azure_Subscription_ID>/resource_groups/<Azure_Resource_Group_ID>.json -d '{ "reading_enabled":"false" }'
{% endhighlight %}

##### Curl Response
{% highlight ruby %}
{
    "id":1,
    "azure_subscription_unique_id":"/subscriptions/dummy_subscription_id",
    "name":"dummy_name",
    "unique_id":"/subscriptions/dummy_subscription_id/resourceGroups/dummy_resource_group_id",
    "location":"dummy_location",
    "reading_enabled":false,
    "attrs":{...}
}
{% endhighlight %}

------
