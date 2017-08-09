---
layout: default
title: Azure All Entities
---

## Overview

Each of the API commands described here relate to retrieving Azure Entities(Resources) being monitored at your site.
Each Azure Resource is completely described by a Hash.

### The Azure Resource Hash

An example JSON-encoded Azure Resource Hash is shown below:

{% highlight ruby %}
{
    "id":1,                                         # Azure resource ID (Assigned by Uptime Cloud Monitor)
    "azure_account_id":3,                           # Azure account ID (Assigned by Uptime Cloud Monitor)
    "azure_subscription_id":10,                     # Azure subscription ID (Assigned by Uptime Cloud Monitor)
    "azure_resource_group_id":"34",                 # Azure resource group ID (Assigned by Uptime Cloud Monitor)
    "name":"dummy_name",                            # Name of the Azure Resource
    "type":"dummy_type",                            # Type  of the Azure Resource
    "sku_attrs":{...},                              # Sku Attributes of the Azure Resource
    "unique_id":"/subscriptions/sub_id/resourceGroups/rg_id/dummy_resource_path",
        # A unique identifier for the resource
    "location":"dummy_location",                    # Location of the resource
    "reading_enabled":true,                         # If monitoring is enabled for the resource group
    "last_seen_at":null                             # Timestamp when resource was last seen/monitored

}
{% endhighlight %}

------

## Index

Retrieve a list of all of your Azure Resources for your site.

#### Required Parameters:

Azure_Account_ID
:  ID of Azure Account for which resources are being fetched

#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U https://api.copperegg.com/v2/azure/allentities.json

curl -s https://<APIKEY>:U@api.copperegg.com/v2/azure/allentities.json
{% endhighlight %}


#### CURL Response:
Response is a JSON-encoded list of Azure resources Hashes and stats(contains total no of resources for your site).

{% highlight ruby %}
{
    "resources":[
        {
            "id":1,
            "azure_account_id":3,
            "azure_subscription_id":10,
            "azure_resource_group_id":"34",
            "name":"dummy_name",
            "type":"dummy_type",
            "sku_attrs":{...},
            "unique_id":"/subscriptions/sub_id/resourceGroups/rg_id/dummy_resource_path",
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
