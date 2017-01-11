---
layout: default
title: IDERA Developer Site
---

### Format of CURL Request

The general format for the curl request in this. You can get the curl software from here - https://curl.haxx.se/

curl -su <APIKEY>:U <HTTP/HTTPS>://api.copperegg.com/v2/alerts/definitions.json

or 

curl -s <HTTP/HTTPS>://<APIKEY>:U@api.copperegg.com/v2/alerts/<API>.<FORMAT>

APIKEY is the user's unique key used for both identification and authentication.

To obtain the APIKEY follow these steps.

- Login to your account on CopperEgg.
- Go to Settings Tab.
- Click on Personal Settings tab on the left hand side.
- Scroll down to 'User API Access' Section, APIKEY is available here.

HTTP and HTTPS both are supported.


### Available APIs

Given below is a brief description of all APIs available.

#### Alert

##### [Definitions](alerts/definitions.html)
Alert Definitions define the conditions which are periodically checked and if the conditions are met then an Alert is generated.
The following actions can be performed using this API.
 - Index - Fetch all your Alert Definition
 - Show - Show in-depth information for a single Alert Definition.
 - Update - Update/Create an Alert Definition.

##### [Notification Profiles](alerts/profiles.html)
Notification Profiles define the various channels defined by the user for sending notifications. There are two notification profile - *User Notification Profiles* and *Custom Notification Profiles*. Each Alert Definition can have one or more than one associated Notification profiles.
The following actions can be performed using this API.
 - Index - Fetch all Notification Profiles
 - Show - Fetch in-depth information for a single Notification Profile.
 - Create - Create a new Notification Profile.
 - Update - Update an existing Notification Profile.
 - Delete - Delete an existing Notification Profile.
 
##### [Issues](alerts/issues.html)
Issues are automatically created by CopperEgg's alerting system whenever one of the conditions defined in Alert Definition is met.
The following actions can be performed using this API.
 - Index - Fetch all Issues.
 - Show - Fetch in-depth information for a single Issue.
 - Update - Update an Issue.
 - Delete - Delete an Issue.

##### [Schedules](alerts/schedules.html)
Schedules are for creating Maintenance periods for the resources monitored by CopperEgg. During which any Issues created will not be notified to the user. 
The following actions can be performed using this API.
 - Index - Fetch all Schedules.
 - Show - Fetch in-depth information for a single Schedules.
 - Create - Create a new Schedules.
 - Update - Update an Schedules.
 - Delete - Delete an Schedules.
 
##### [Annotations](alerts/annotations.html)
Annotations can be used to annotate event time line on monitoring graphs for later inspection.
The following actions can be performed using this API.
 - Index - Fetch all Annotations.
 - Show - Fetch in-depth information for a single Annotations.
 - Create - Create a new Annotations.
 - Update - Update an Annotations.
 - Delete - Delete an Annotations. 
 
 
#### RevealCloud

##### [Servers](revealcloud/servers.html)
Server represent each of the user's system monitored by CopperEgg.
The following actions can be performed using this API.
 - Index - Fetch details of all monitored systems.
 - Hide - Hide/Unhide a system.
 - Delete - Remove a system from being monitored by CopperEgg.
 
##### [Samples](revealcloud/samples.html)
Samples API can be used to fetch collected data for a system.
The only action available in this API is fetching the data for a system and for a given time period.

##### [Tags](revealcloud/samples.html)
Tags are used to group multiple systems monitored by CopperEgg.
The following actions can be performed using this API.
 - Index - Fetch all system Tags.
 - Show - Fetch all system grouped by a tag.
 - Create - Add a new System Tag to one or more monitored Systems.
 - Delete - Remove a tag from on system.


#### RevealUptime

##### [Probes](revealuptime/probes.html)
Probe refers to a periodic test of an internet-connected service. Today the supported Probe types include TCP port connections, ICMP, DNS, HTTP GET/POST and HTTPS GET/POST, REST, SSL. ‘Station’ refers to a location from which the tests are being generated.
The following actions can be performed using this API.
 - Index - Fetch details of all monitored probe.
 - Show - Fetch in-depth of a single probe.
 - Create - Create a new Probe.
 - Update - Update an existing probe.
 - Delete - Remove an existing probe.
 
##### [Samples](revealuptime/samples.html)
Samples API can be used to fetch collected data for a probe.
The only action available in this API is fetching the data for a probe and for a given time period.

##### [Tags](revealuptime/samples.html)
Tags are used to group multiple probes monitored by CopperEgg.
The following actions can be performed using this API.
 - Index - Fetch all probe Tags.
 - Show - Fetch all probe grouped by a tag.
 - Create - Add a new Probe Tag to one or more monitored Systems.
 - Delete - Remove a tag from on probe.
 
 
#### Real Time User Monitoring

##### [Samples](revealapp/samples.html)
Samples API can be used to fetch collected RUM data samples.


#### Custom Metrics

##### [Metric Groups](revealmetrics/metricgroups.html)
Custom Metrics allow user to create custom groups for which data can be collected, monitored. A custom metric group behaves exactly as a probe or a system i.e Users can send data to CopperEgg, define alerts, see the graphs on CopperEgg UI.
Metric Group API allows users to create their own metric groups and perform various functions on them.
 - Index - Fetch all defined Metric Groups.
 - Show - Fetch in-depth details of a Single Metric Group.
 - Create - Create a new Metric Group.
 - Update - Update an existing Metric Group.
 - Delete - Delete an existing Metric Group.

##### [Custom Metric Objects and Staleness](revealmetrics/metricgroups.html)
Each Metric Group has one or more Metric Objects for which data is sent.
CopperEgg provides API for counting and deleting stale Custom objects.

##### [Dashboards](revealmetrics/dashboards..html)
Custom Metrics Dashboards allows user to create dashboard for organize the custom metrics and view their associated charts.
Following operation are available in Custom Metric Dashboard API.
 - Index - Fetch all defined Custom Metric Dashboard.
 - Create - Create a new Custom Metric Dashboard.
 - Update - Update an existing Custom Metric Dashboard.
 - Delete - Delete an existing Custom Metric Dashboard.
 
#### [Samples](revealmetrics/samples.html) 
Samples API can be used to fetch collected data for custom metrics.
The only action available in this API is fetching the data for a custom metric and for a given time period.

##### [Tags](revealmetrics/tags.html)
Tags are used to group multiple custom metrics monitored by CopperEgg.
The following actions can be performed using this API.
 - Index - Fetch all defined Custom Metrics tags.
 - Show - Fetch custom metric object associated with single custom metric tag.
 - Create - Add a new Custom Metrics Tag to a custom metric object.
 - Delete - Remove a Custom Metrics Tag from a custom metric object.
 
 
### Releases

December 10,2015
- Updated API Documentation.

December 31, 2015

- Pagination added to API which allows to fetch issues from Alerts API in batches of 100.

February 12, 2014

- Added Alert Schedules information

January 2, 2014

- Added RUM information
- Fixed missing Servers page

November 18, 2013

- Filled in some missing Server Sample data information
- Changed 'Systems' to 'Servers'



Note:
Get your API key from Settings, Personal Settings, then at the bottom "User API Access"

