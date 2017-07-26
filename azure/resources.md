---
layout: default
title: Azure Resources
---

## Overview

Each of the API commands described here relate to retrieving and updating one or more Azure Resources being monitored at your site.
Each Azure Resource is completely described by a Hash.

### The Azure Resource Hash

An example JSON-encoded Azure Resource Hash is shown below:

{% highlight ruby %}
{
    "id":1,                                         # Azure Resource ID(Assigned by Uptime Cloud Monitor)
    "azure_subscription_unique_id":"/subscriptions/dummy_subscription_id",
        # Azure subscription unique id of the subscription of the resource
    "azure_resource_group_unique_id":"/subscriptions/dummy_subscription_id/resourceGroups/dummy_resource_group_id",
        # Azure Resource Group unique id of the resource group of the resource
    "name":"dummy_name",                            # Name of the Azure Resource
    "type":"dummy_type",                            # Type  of the Azure Resource
    "sku_attrs":{...},                              # Sku Attributes of the Azure Resource
    "unique_id":"/subscriptions/dummy_subscription_id/resourceGroups/dummy_resource_group_id/dummy_resource_path",
        # A unique identifier for the resource
    "location":"dummy_location",                    # Location of the resource
    "reading_enabled":true,                         # If monitoring is enabled for the resource
    "last_seen_at":null                             # Timestamp when resource was last seen/monitored

}
{% endhighlight %}

------

## Index

Retrieve a list of all of your Azure Resources for an Azure Resource Group.

#### Required Parameters:

Azure_Account_ID
:  ID of Azure Account for which resources are being fetched

#### Optional Parameters:

Azure_Subscription_ID
:  ID of Azure Subscription for which resources are being fetched

Azure_Resource_Group_ID
:  ID of Azure Resource Group for which resources are being fetched

overview
:  Only existence of key is required. If key is provided, resources will be fetched for all accounts for the user

type
:  Fetch resources of specific type

#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U https://api.copperegg.com/v2/azure/accounts/<Azure_Account_ID>/resources.json

curl -s https://<APIKEY>:U@api.copperegg.com/v2/azure/accounts/<Azure_Account_ID>/resources.json
{% endhighlight %}

##### CURL command with optional parameters:
{% highlight sh %}
curl -su <APIKEY>:U https://api.copperegg.com/v2/azure/accounts/<Azure_Account_ID>/resources.json?overview=true&type=dummy_type

curl -su <APIKEY>:U https://api.copperegg.com/v2/azure/accounts/<Azure_Account_ID>/subscriptions/<Azure_Subscription_ID>/resource_groups/<Azure_Resource_Group_ID>/resources.json -d '{ overview: "true", type: "dummy_type" }'
{% endhighlight %}


#### CURL Response:
Response is a JSON-encoded list of Azure Resource Hashes and stats(contains total no of resources for the resource group/account).

{% highlight ruby %}
{
    "resources":[
        {
            "id":1,
            "azure_subscription_unique_id":"/subscriptions/dummy_subscription_id",
            "azure_resource_group_unique_id":"/subscriptions/dummy_subscription_id/resourceGroups/dummy_resource_group_id",
            "name":"dummy_name",
            "type":"dummy_type",
            "sku_attrs":{...},
            "unique_id":"/subscriptions/dummy_subscription_id/resourceGroups/dummy_resource_group_id/dummy_resource_path",
            "location":"dummy_location",
            "reading_enabled":true,
            "last_seen_at":null
        }
    ],
    "stats":{
        "total":1
    }
}
{% endhighlight %}

------

## Count

Fetches count of total azure resources for your account or resource group.

##### Curl Command
{% highlight sh %}
curl -s https://<APIKEY>:U@api.copperegg.com/v2/azure/accounts/<Azure_Account_ID>/subscriptions/<Azure_Subscription_ID>/resource_groups/<Azure_Resource_Group_ID>/resources/count.json

curl -s https://<APIKEY>:U@api.copperegg.com/v2/azure/accounts/<Azure_Account_ID>/resources/count.json
{% endhighlight %}

##### Curl Response
{% highlight ruby %}
1
{% endhighlight %}

------

## Update

Updates an existing Azure Resource.
: * Only reading_enabled attribute is allowed to be modified for an azure resource.

#### Required Parameters:

Azure_Account_ID
:  ID of Azure Account for which resource is to be updated

Azure_Resource_ID
:  ID of Azure Resource to be updated

reading_enbled
: If monitoring is enabled for the resource

#### Optional Parameters:

Azure_Subscription_ID
:  ID of Azure Subscription for which resource is to be updated

Azure_Resource_Group_ID
:  ID of Azure Resource Group for which resource is to be updated

##### Curl Command
{% highlight sh %}
curl -s -XPUT -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/azure/accounts/<Azure_Account_ID>/subscriptions/<Azure_Subscription_ID>/resource_groups/<Azure_Resource_Group_ID>/resources/<Azure_Resource_ID>.json -d '{ "reading_enabled":"false" }'

curl -s -XPUT -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/azure/accounts/<Azure_Account_ID>/resources/<Azure_Resource_ID>.json -d '{ "reading_enabled":"false" }'
{% endhighlight %}

##### Curl Response
{% highlight ruby %}
{
    "id":1,
    "azure_subscription_unique_id":"/subscriptions/dummy_subscription_id",
    "azure_resource_group_unique_id":"/subscriptions/dummy_subscription_id/resourceGroups/dummy_resource_group_id",
    "name":"dummy_name",
    "type":"dummy_type",
    "sku_attrs":{...},
    "unique_id":"/subscriptions/dummy_subscription_id/resourceGroups/dummy_resource_group_id/dummy_resource_path",
    "location":"dummy_location",
    "reading_enabled":false,
    "last_seen_at":null
}
{% endhighlight %}

------
