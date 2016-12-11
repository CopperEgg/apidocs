---
layout: default
title: Custom Metrics - Tags
---

## Index

Retrieve all defined Custom Metrics tags.

#### CURL Command, and variations:
{% highlight sh %}
curl -u <APIKEY>:U https://api.copperegg.com/v2/revealmetrics/tags.json
{% endhighlight %}

#### CURL Response:

Response is a JSON-encoded array of hashes, one hash per Custom Metrics tag.

{% highlight sh %}
[
  {
    "id":"Win2008r2",                              # TAG_ID
    "objects":[                                    # objects associated with this tag
      {
        "idp":"custom|",                           # will always be "custom" for custom metrics
        "idv":"AMAZONA-G8RT2L3|",                  # the 'id value' (unique ID) of a custom object with this tag
        "attrs":{"hostname":null,"label":null}     # hoatsname and label will always be null for a custom object
      },
      {
        "idp":"custom|",
        "idv":"AMAZONA-TS5KSQ6|",
        "attrs":{"hostname":null,"label":null}
      }
    ]
  },
  {
    "id":"netclr",
    "objects":[
      {
        "idp":"custom|",
        "idv":"AMAZONA-G8RT2L3|",
        "attrs":{"hostname":null,"label":null}
      }
    ]
  },
  {
    "id":"aspnet",
    "objects":[
      {
        "idp":"custom|",
        "idv":"AMAZONA-TS5KSQ6|",
        "attrs":{"hostname":null,"label":null}
      }
    ]
  }
]
{% endhighlight %}

In the example above: three tags are returned by the Index command; "Win2008r2", "netclr" and "aspnet".
Note that each tag hash contains a single TAG_ID ("id"), and an array of objects, one or more for each object with the tag of reference.


----
## Show

Show in-depth information about a single custom metric tag.

#### Required Parameters:
TAG_ID as part of the path.

#### CURL Command, and variations:
{% highlight sh %}
curl -u <APIKEY>:U https://api.copperegg.com/v2/revealmetrics/tags/TAG_ID.json
{% endhighlight %}

#### CURL Response:

Response is JSON with an array of hashes containing details of all custom objects associated with the specified tag.

Continuing with the Index example, here we pass the tag "Win2008r2":

{% highlight sh %}
[
  {
    "identifier":"my_test_metric_identifier", # identifier for custom metrics object
    "idp":"custom|",                          # always 'custom' for custom metrics tags
    "idv":"AMAZONA-TS5KSQ6|",                 # custom object with this tag
    "state":"enabled",                        # specify the state for custom metric object
    "hidden":false,                           # if "hidden" is true, the tag will not be visible in the UI (nor active)
    "last_updated":1357680889,                # time when this object was last updated
    "created_at":1357675665,                  # time when this object was created
    "tags":["Win2008r2","aspnet"],            # tags associated with this custom object
    "attrs":{"hostname":null,"label":null},   # hostname and label will always be null for custom objects
    "label":null,                             # Label for custom metric group, if any
    "meta":{}                                 # meta-data for metic object, used internally
  },
  {
    "identifier":"my_test_metric_identifier",
    "idp":"custom|",
    "idv":"AMAZONA-G8RT2L3|",
    "state":"enabled",
    "hidden":false,
    "last_updated":1357680891,
    "created_at":1357672420,
    "tags":["Win2008r2","netclr"],
    "attrs":{"hostname":null,"label":null},
    "label":null,
    "meta":{}
  }
]
{% endhighlight %}


----
## Create / Update

Add a new tag to one or more defined custom objects.

Required params:

* a tag  Tags may contain a-z, A-Z, 0-9, - and \_

* one or more custom object idv to which the tag will be applied. idv for object is identifier for mertic object (can be found from UI).

* if specifying more than one idv, use a comma-separated list

In the following example, a tag named "ElasticBeanstalk" will be applied to one existing custom object, with idv of AMAZONA-TS5KSQ6.

Note: the format of the Custom Object Create Tag API call is somewhat different than the Create Tag calls for System and Probe.
  The tag is specified 'tag=TAG_ID', and the custom object ids are specified at 'ids=CUSTOMOBJECT_ID1,CUSTOMOBJECT_ID2'


#### CURL Command, and variations:
{% highlight sh %}
curl -u <APIKEY>:U -XPOST https://api.copperegg.com/v2/revealmetrics/tags.json -d 'tag=ElasticBeanstalk&ids=AMAZONA-TS5KSQ6'
{% endhighlight %}

Response is Status 200, empty JSON:

{% highlight sh %}
{}
{% endhighlight %}


----
## Delete

Delete a tag from one custom object.

Required params:
TAG_ID as part of the path

CUSTOMOBJECT_ID
the Id of the custom object from which the tag will be removed

Note: the format of the Custom Object Remove Tag API call is somewhat different than the Remove Tag calls for System and Probe.
  The TAG_ID is specified as part of the path; the custom object ids are specified as 'ids=\[CUSTOMOBJECT_ID1,CUSTOMOBJECT_ID2\]'

#### CURL Command, and variations:
{% highlight sh %}

Deleting tag from one Custom Metric Object
curl -XDELETE -u <APIKEY>:U https://api.copperegg.com/v2/revealmetrics/tags/<TAG_ID>.json -d 'ids[]=CUSTOMOBJECT_ID'

Deleting tag two (more than one) Custom Metric Object
curl -XDELETE -u <APIKEY>:U https://api.copperegg.com/v2/revealmetrics/tags/<TAG_ID>.json -d 'ids[]=CUSTOMOBJECT_ID1&ids[]=CUSTOMOBJECT_ID2'
{% endhighlight %}

#### CURL Response:

Response is Status 200, empty JSON:

{% highlight sh %}
{}
{% endhighlight %}


In the following example, the tag 'ElasticBeanstalk' will be removed from the custom object AMAZONA-TS5KSQ6, (see the Show example).

#### CURL Command, and variations:
{% highlight sh %}
curl -XDELETE -u <APIKEY>:U https://api.copperegg.com/v2/revealmetrics/tags/ElasticBeanstalk.json -d 'ids[]=AMAZONA-TS5KSQ6'
{% endhighlight %}

