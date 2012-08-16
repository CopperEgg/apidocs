---
layout: default
title: RevealEngine - Annotations
---

Index
-----

CURL Command:
{% highlight sh %}
curl -u APIKEY:U https://api.copperegg.com/v2/annotations.json
{% endhighlight %}

CURL Response:

Response is JSON with an array of annotations.

{% highlight javascript %}
[
    {
        "id": 2,
        "note": "Annotations are sweet!",
        "starttime": 1341515302,
        "endtime": 1341517702,
        "label": null,
        "tags": [
            "www"
        ],
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
        "tags": [
            "deploy",
            "www"
        ],
        "created_by": "build@example.com",
        "created_at": 1342123890,
        "updated_at": 1342123890
    }
]
{% endhighlight %}

Show
----

CURL Command:
{% highlight sh %}
curl -u APIKEY:U https://api.copperegg.com/v2/annotations/2.json
{% endhighlight %}

CURL Response:

Response is JSON with details of the requested annotation:

{% highlight javascript %}
{
    "id": 2,
    "note": "Annotations are sweet!",
    "starttime": 1341515302,
    "endtime": 1341517702,
    "label": null,
    "tags": [
        "www"
    ],
    "created_by": "devguy@example.com",
    "created_at": 1341518331,
    "updated_at": 1341518331
}
{% endhighlight %}

Create
------

Required params:
* note: max 250 chars
* starttime: seconds from the epoch
* endtime: seconds from the epoch, must be AFTER starttime

Optional params:
* label: one of: \[yellow green blue orange red purple\]
* tags: comma separated list (Allowed chars: A-Za-z0-9_)

CURL Command:
{% highlight sh %}
curl -u APIKEY:U -XPOST https://api.copperegg.com/v2/annotations.json -d 'note=API&starttime=1342119638&endtime=1342119950'
{% endhighlight %}

CURL Response:

Response is JSON with details of the requested annotation:

{% highlight javascript %}
{
  "id": 7,
  "note": "API",
  "starttime": 1342119638,
  "endtime": 1342119950,
  "label": null,
  "tags": [

  ],
  "created_by": "devguy@sample.com",
  "created_at": 1342126787,
  "updated_at": 1342126787
}
{% endhighlight %}


Update
------

CURL Command:
{% highlight sh %}
curl -s -XPUT -u APIKEY:U http://api.copperegg.com/v2/annotations/7.json -d 'endtime=1342119990'
{% endhighlight %}

CURL Response:

Response is JSON with details of the requested annotation:

{% highlight javascript %}
{
  "id": 7,
  "note": "API",
  "starttime": 1342119638,
  "endtime": 1342119990,
  "label": null,
  "tags": [

  ],
  "created_by": "devguy@sample.com",
  "created_at": 1342126787,
  "updated_at": 1342126978
}
{% endhighlight %}


Destroy
-------

CURL Command:
{% highlight sh %}
curl -s -XDELETE -u APIKEY:U http://api.copperegg.com/v2/annotations/7.json

{% endhighlight %}

CURL Response:

Response is Status 200, empty JSON:

{% highlight javascript %}
{

}
{% endhighlight %}

