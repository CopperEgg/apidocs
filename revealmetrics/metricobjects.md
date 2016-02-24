---
layout: default
title: Custom Metric Objects and Staleness
---
## Overview

These are the API calls for counting and deleting stale custom metric objects.

### About Metric Objects:
If you define a custom metric group monitoring a particular metric, you can send data to our Uptime
Cloud Monitor from as many systems as you want. For eg. If we want to monitor MySQL metrics for 10
servers, we will use the same "Metric Group" and correspondingly 10 metric objects will be created
, one for each server. Data samples will then be sent periodically to each of the 10 custom metric
objects from the corresponding MySQL servers.

Even if these servers are no longer actively monitored, their data samples are still stored inside
their corresponding custom metric objects in Uptime Cloud Monitor. You will not be billed for these
data samples if the custom metric object is not active (i.e.) for each month, billing happens only
for the custom metrics object that are 'alive' and have incoming data samples during that month.

You might consider deleting 'stale' custom metric objects that no longer have incoming data samples
so that they are not more visible on your UI (Custom -> Custom Objects). A “Stale” custom metric
object for a time period is defined as that object for which no data/samples were received in that
period. So, if we call an object as 6 month stale, that means no samples were received from your
metric since last 6 months. Such cleanup of stale custom metric objects also improves the
performance of your site.


## API to count stale custom metric objects :

A simple API will get you count of your total custom metric objects vs. stale custom metric objects
 for a particular time period which is sent by you.

{% highlight sh %}
curl -su <APIKEY>:U -H "Content-type: application/json" -XGET "http://api.copperegg.com/v2/revealmetrics/count_stale_objects.json?days=x&months=y&years=z"

x = no. of days as a positive non-zero integer
y = no. of months as a positive non-zero integer
z = no. of years as a positive non-zero integer
{% endhighlight %}

For eg, a sample request to delete custom metric objects older than 10 days would be :

{% highlight sh %}
curl -su <APIKEY>:U -H "Content-type: application/json" -XGET "http://api.copperegg.com/v2/revealmetrics/count_stale_objects.json?days=10&months=0&years=0"
{% endhighlight %}

Above request can also be reduced to skip months and years parameters because they are zero
{% highlight sh %}

curl -su <APIKEY>:U -H "Content-type: application/json" -XGET "http://api.copperegg.com/v2/revealmetrics/count_stale_objects.json?days=10"
{% endhighlight %}

## Another similar API to delete stale custom objects :

{% highlight sh %}
curl -su <APIKEY>:U -H "Content-type: application/json" -XPOST "http://api.copperegg.com/v2/revealmetrics/destroy_stale_objects.json" -d '{"days": x, "months": y, "years": z}'

x = no. of days as a positive non-zero integer
y = no. of months as a positive non-zero integer
z = no. of years as a positive non-zero integer
{% endhighlight %}

For eg, a sample request to delete custom metric objects older than 6 months would be :

{% highlight sh %}
curl -su <APIKEY>:U -H "Content-type: application/json" -XPOST "http://api.copperegg.com/v2/revealmetrics/destroy_stale_objects.json" -d '{"days": 0, "months": 6, "years": 0}'
{% endhighlight %}

Above request can also be reduced to skip days and years parameters because they are zero

{% highlight sh %}
curl -su <APIKEY>:U -H "Content-type: application/json" -XPOST "http://api.copperegg.com/v2/revealmetrics/destroy_stale_objects.json" -d '{"months": 6}'
{% endhighlight %}
