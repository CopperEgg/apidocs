---
layout: default
title: Stale Servers
---

## Overview

These are the API calls for counting and deleting stale servers. A server can be called stale if it was last updated before a certain time limit.

# API to count stale servers :

This will get count of total servers vs. stale servers for a given time period.

{% highlight sh %}
curl -su <APIKEY>:U -H "Content-type: application/json" -XGET "https://api.copperegg.com/v2/servers/count_stale.json?days=x&months=y&years=z"

x = number of days as a positive non-zero integer
y = number of months as a positive non-zero integer
z = number of years as a positive non-zero integer
{% endhighlight %}

For eg, a sample request to list stale servers older than 10 days would be :

{% highlight sh %}
curl -su <APIKEY>:U -H "Content-type: application/json" -XGET "https://api.copperegg.com/v2/servers/count_stale.json?days=10&months=0&years=0"
{% endhighlight %}

Above request can also be reduced to skip months and years parameters because they are zero
{% highlight sh %}

curl -su <APIKEY>:U -H "Content-type: application/json" -XGET "https://api.copperegg.com/v2/servers/count_stale.json?days=10"
{% endhighlight %}

#### CURL OUTPUT FORMAT
{% highlight sh %}

Total servers : <NUMBER_OF_SERVERS> , Stale servers : <NUMBER_OF_SERVERS_STALE_SINCE_GIVEN_PERIOD>
{% endhighlight %}

-----

## Another similar API to delete stale servers :

{% highlight sh %}
curl -su <APIKEY>:U -XDELETE "https://api.copperegg.com/v2/servers/destroy_stale.json?days=x&months=y&years=z"

x = no. of days as a positive non-zero integer
y = no. of months as a positive non-zero integer
z = no. of years as a positive non-zero integer
{% endhighlight %}

For eg, a sample request to delete stale servers older than 6 months would be :

{% highlight sh %}
curl -su <APIKEY>:U -XDELETE "https://api.copperegg.com/v2/servers/destroy_stale.json?days=0&months=6&years=0"
{% endhighlight %}

Above request can also be reduced to skip days and years parameters because they are zero

{% highlight sh %}
curl -su <APIKEY>:U -XDELETE "https://api.copperegg.com/v2/servers/destroy_stale.json?months=6"
{% endhighlight %}


#### CURL OUTPUT FORMAT
{% highlight sh %}

Removed <NUMBER_OF_SERVERS_STALE_SINCE_GIVEN_PERIOD> stale servers out of <NUMBER_OF_SERVERS>
{% endhighlight %}
