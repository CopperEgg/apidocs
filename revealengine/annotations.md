---
layout: default
title: Annotations
---

## Index


#### CURL Command, and variations::
{% highlight sh %}
curl -su <APIKEY>:U https://api.copperegg.com/v2/annotations.json?per_page=integer&page_number=integer&starttime=long_integer&endtime=long_integer

curl -sk https://<APIKEY>:U@api.copperegg.com/v2/annotations.json?per_page=integer&page_number=integer&starttime=long_integer&endtime=long_integer
{% endhighlight %}

where <br>
per_page = No. of annotations to be fetched in a page (in one call). Maximum is 100. <br>
page_number = Number of the batch to be fetched. By default, it is 1.<br>
starttime = The time in seconds from 1st Jan 1970 till the lower limit of required date.<br>
endtime = The time in seconds from 1st Jan 1970 till the upper limit of required date.

If starttime and endtime are not specified, it fetches the all the annotations for the site and returns result on basis of pagination done according to page_number and per_page option.
If any of the above parameters are not sent with curl request, the request will return the first 100 annotations of the site.

The API key is a unique key that identifies each customer.
You can obtain it by clicking the Settings tab while logged on to Uptime Cloud Monitor UI.
It is presented at the bottom of the screen under “User API Access”.


#### CURL Response:

Response is a JSON-encoded array of Annotation Hashes.

{% highlight sh %}
{
  "annotations": [
                    {
                      "id": 2,
                      "note": "Annotations are sweet!",
                      "starttime": 1341515302,
                      "endtime": 1341517702,
                      "label": null,
                      "tags": ["www"],
                      "duration": 4200,
                      "created_by": "devguy@example.com",
                      "created_at": 1341518331,
                      "updated_at": 1341518331
                    },
                    {
                      "id": 5,
                      "note": "Deploy to master",
                      "starttime": 1342119638,
                      "endtime": 1342119838,
                      "label": null,
                      "tags": ["deploy","www"],
                      "duration": 200,
                      "created_by": "build@example.com",
                      "created_at": 1342123890,
                      "updated_at": 1342123890
                    }
                  ]
  "stats": {
              "total" : 2      # total annotations without pagination (according to current filter)
           }
}
{% endhighlight %}

----

## Show

#### CURL Command, and variations::
{% highlight sh %}
curl -su <APIKEY>:U https://api.copperegg.com/v2/annotations/<ANNOTATION_ID>.json

curl -s https://<APIKEY>:U@api.copperegg.com/v2/annotations/<ANNOTATION_ID>.json
{% endhighlight %}

#### CURL Response:

Response is a JSON-encoded Annotation Hash:

{% highlight sh %}
{
  "id": 2,
  "note": "Annotations are sweet!",
  "starttime": 1341515302,
  "endtime": 1341517702,
  "label": null,
  "tags": ["www"],
  "created_by": "devguy@example.com",
  "created_at": 1341518331,
  "updated_at": 1341518331
}
{% endhighlight %}

----

## Create

#### Required parameters:
* note: text string describing the event (max 250 chars)
* starttime: seconds from the epoch
* endtime: seconds from the epoch, must be AFTER starttime

#### Optional parameters:
* label: one of: \[yellow green blue orange red purple\]
* tags: comma separated list (Allowed chars: A-Za-z0-9_)


#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U -XPOST https://api.copperegg.com/v2/annotations.json -d 'note=API&starttime=1342119638&endtime=1342119950'

curl -s  -XPOST https://<APIKEY>:U@api.copperegg.com/v2/annotations.json -d 'note=API&starttime=1342119638&endtime=1342119950'

curl -s  https://<APIKEY>:U@api.copperegg.com/v2/annotations.json -H "Content-Type: application/json" -XPOST -d '{"note":"API","starttime":1342119638,"endtime":1342119950}'
{% endhighlight %}

#### CURL Response:

Response is a JSON-encoded Annotation Hash:

{% highlight sh %}
{
  "id": 7,
  "note": "API",
  "starttime": 1342119638,
  "endtime": 1342119950,
  "label": null,
  "tags": [],
  "created_by": "devguy@sample.com",
  "created_at": 1342126787,
  "updated_at": 1342126787
}
{% endhighlight %}

----

## Update

#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U https://api.copperegg.com/v2/annotations/<ANNOTATION_ID>.json -XPUT -d 'endtime=1342119990'

curl -s https://<APIKEY>:U@api.copperegg.com/v2/annotations/<ANNOTATION_ID>.json -XPUT -d 'endtime=1342119990'

curl -s https://<APIKEY>:U@api.copperegg.com/v2/annotations/<ANNOTATION_ID>.json -H "Content-Type: application/json" -XPUT -d '{"endtime":1342119990}'
{% endhighlight %}

#### CURL Response:

Response is the JSON-encoded updated Annotation Hash:

{% highlight sh %}
{
  "id": 7,
  "note": "API",
  "starttime": 1342119638,
  "endtime": 1342119990,
  "label": null,
  "tags": [],
  "created_by": "devguy@sample.com",
  "created_at": 1342126787,
  "updated_at": 1342126978
}
{% endhighlight %}

----

## Delete

#### CURL Command, and variations::
{% highlight sh %}
curl -XDELETE -su <APIKEY>:U https://api.copperegg.com/v2/annotations/<ANNOTATION_ID>.json

curl -XDELETE -s  https://<APIKEY>:U@api.copperegg.com/v2/annotations/<ANNOTATION_ID>.json
{% endhighlight %}

#### CURL Response:

Response is Status 200, empty JSON:

{% highlight sh %}
{}
{% endhighlight %}

