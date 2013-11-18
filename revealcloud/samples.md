---
layout: default
title: Servers - Samples
---


##Overview
--------
The API call for obtaining Server Samples has a fair amount of detail, unlike many of the other CopperEgg API calls.  
The calling parameters and abbreviations that appear in the data structures are documented at the outset.
The ideal way to get started is to scan the early sections, and then dig into the examples. Refer back to the parameters, keys and abbreviations when necessary, once you have gotten a feel for using the API.


#####Server Sample Keys  
{% highlight sh %}
key name           valid combinations
uptime                   l_u
health state          h, l_h
running processes     r, l_r
blocked processes     b, l_b
load                  l, l_l
memory                m, l_m
swap                  s, l_s
cpus                  c, l_c, s_c, l_s_c
interfaces            i, l_i, s_i, l_s_i
filesystems                   s_f, l_s_f
diskio                        s_d, l_s_d
processes             p, l_p
{% endhighlight %}  

*** Note:
* the prefacing ‘l_’ means ‘latest’; return most recent sample data.
* the prefacing ‘s_’ means 'separated'; return data from individual components.  

#####Server Samples: Data Types and Units  
{% highlight sh %}
uptime                # server uptime in seconds (integer)
health state          # returns an array of 10 values:       
                      # health index (a value between 0 and 1 that indicates the general health of that system) (float)
                      # health state (0=unknown, 1=ok, 2=warning, 3=critical -- these are generally based on the health index) (int)
                      # uptime state (same 0,1,2,3 values) (int)
                      # processes state (same 0,1,2,3 values) (int)
                      # load state (same 0,1,2,3 values) (int)
                      # cpu state  (same 0,1,2,3 values) (int)    
                      # memory state (same 0,1,2,3 values) (int)
                      # last updated state (i.e. how long ago did copperegg receive data for this system) (same 0,1,2,3 values) (int)
                      # filesystem health index (a value 0 to 1 indicating general health of the filesystems) (float)
                      # filesystem state (same 0,1,2,3 values) (int)
running processes     # number of running processes (integer)
blocked processes     # number of blocked processes (integer)
load                  # l:  1 minute load index (float);  l_h :  1 min, 5 min and 15 min load indices (floats)
memory                # buffer memory, cache memory, free memory, used memory  all in MB (floats)
swap                  # swap used in MB, swap free in MB  (floats)
cpus                  # active, iowait, user, nice, system, irq, softirq, steal, guest; each ranges from 0 to 1 (floats)
interfaces            # bytes received in KB/s, bytes transmitted in KB/s  (floats)
filesystems           # GB used, GB free  (floats)
diskio                # bytes read in KB/s, bytes written in KB/s (floats)
processes             # see below
{% endhighlight %}  


#####Other Server Sample Abbreviations
{% highlight sh %}
term               abbreviation
timestamp             '_ts'
actual sample size    '_bs'
attributes            'a'
system uuid           'uuid'
{% endhighlight %}  


#####The format of the Process and User arrays are described below. 
{% highlight sh %}
Process array:
[
  "bash",       # process name (string, case sensitive)
  null,         # process command line arguments
  53479,        # PID (number)
  "1001",       # UID (number formatted as a string)
  "S",          # state
  0,            # CPU % User, this process     (float, range 0 to 1)
  0,            # CPU % System, this process   (float, range 0 to 1)
  0,            # CPU % Total, this process    (float, range 0 to 1)
  1,            # internal use
  27881472,     # Memory Virtual, this process  (integer, in bytes)
  9695232,      # Memory Resident, this process (integer, in bytes)
  0             # internal use
]

User array:
[
  501,          # UID (number)
  0.051497,     # CPU % User, this user    (float, range 0 to 1)
  0.005440,     # CPU % System, this user  (float, range 0 to 1)
  0.056938,     # CPU % Total, this user   (float, range 0 to 1)
  0,            # internal use
  212672065536, # Memory Virtual, this user  (integer, in bytes)
  4214882304,   # Memory Resident, this user (integer, in bytes)
  0             # internal use
]
{% endhighlight %}  

#####Additional Process notes:  

state  
: The state is given by a sequence of characters, where the first character indicates the run state of the process.
The state symbol is passed from the OS, without translation. If a symbol appears that is not included below, please check your OS documentation.  
  
* I       Marks a process that is idle (sleeping for longer than about 20 seconds).
* R       Marks a runnable process.
* S       Marks a process that is sleeping for less than about 20 seconds.
* T       Marks a stopped process.
* U       Marks a process in uninterruptible wait.
* Z       Marks a dead process (a zombie).

  


##Retrieve Server Samples
----

####Required Parameters:  

uuids
: You must specify at least one Server UUID. Up to 20 uuids can be specified in each request. Multiple uuids are specified as a comma separated string.  
      
####Optional Parameters:  
  
starttime  
: An integer unix timestamp (seconds since epoch) representing the beginning of your query timeframe.  
*** NOTE: if neither starttime or endtime are provided, the last 5 minutes of samples are returned. 
    
endtime  
: An integer unix timestamp (seconds since epoch) representing the end of your query timeframe.   
*** NOTE: if neither starttime or endtime are provided, the last 5 minutes of samples are returned)  
  
keys  
: A list of keys you want to include (see "key reference"). Multiple keys are specified as a comma separated string.  
Default: "l_u,l_r,l_b,l_l,m,s,c,i,d".  
*** NOTE: the 'd' key is not implemented; however, if you call this api command specifying no keys, the result includes the last 5 minutes of aggregate DiskIO data; meaning that each sample has two values, reads in  KB/s, and writes in KB/s

sample_size  
: Override the default sample size that is determined by the starttime/endtime range. This will only work if you specify a sample_size larger than what is automatically calculated for the time range.   
If you specify a smaller sample_size, the default sample_size will be used.  
Valid sample sizes range from 5 to 86400 seconds.  
    


###Example 1 Retrieving Server Samples, using defaults.
----
Obtain samples from one system, specifying only the UUID. This will demonstrate the default set of data returned when:    
* no keys are included in the command, and  
* the starttime and endtime are not specified.   
   
As noted above, the default keys are "l_u,l_r,l_b,l_l,m,s,c,i,d".  

####CURL Command, and variations:  
{% highlight sh %}
curl -su <APIKEY>:U "https://api.copperegg.com/v2/revealcloud/samples.json?uuids=<UUID>"

curl -s "https://<APIKEY>:U@api.copperegg.com/v2/revealcloud/samples.json?uuids=<UUID>"

curl -s -XGET https://<APIKEY>:U@api.copperegg.com/v2/revealcloud/samples.json -H "Content-Type: application/json" -d '{"uuids":[<UUID>]}'
{% endhighlight %}  

####CURL Response:  
  
Response is a JSON-encoded array containing one Server Sample Hash, with 5 min of data.  

{% highlight sh %}
[
 {
  "uuid":"ac1f5ef85c1177ef97596f334f877370",        # unique system identifier
  "a":                                              # baked attributes
  {
   "p":1364954577                                   # most recent update time (unix timestamp) 
  },                           
  "hid":0,                                          # hidden; true == 1, false == 0
  "_ts":1364954290,                                 # unix timestamp of offet 0
  "_bs":5,                                          # actual sample interval, in seconds
  "l_u":645013,                                     # latest uptime
  "l_r":0,                                          # latest count of running procs
  "l_b":0,                                          # latest count of blocked procs
  "l_l":[0.98,1.36,1.4],                            # latest load indices, short, mid and long term
  "m":                                              # last 5 min of memory metrics
  {                                                 # each value in MB
   "0":[1335.72,1786.73,1275.4,3784.5],             # buffer memory, cache memory, free memory, used memory
   "15":[1335.71,1786.73,1273.43,3787.66],
               .........
		"270":[1342.15,1788.38,1267.18,3790.12],
		"285":[1342.48,1788.56,1264.47,3788.75]
  },
		"s":                                            # last 5 min of swap metrics
  {
   "0":[131.0,380.0],                               # swap used in MB, swap free in MB
			"15":[131.0,380.0],
           .........           
			"270":[131.0,380.0],
			"285":[131.0,380.0]
  },
		"c":                                            # last 5 min of aggregate CPU metrics
  {                                                 # each value ranges from 0 to 1.0, representing a percentage
   "0":[0.036,0.0,0.0193,0.0,0.0168,0.0,0.0,0.0,0.0],   # active, iowait,user, nice, system, irq, softirq, steal, guest
			"15":[0.0335,0.0,0.0195,0.0,0.014,0.0,0.0,0.0,0.0],
                        .........
			"270":[0.0377,0.0,0.025,0.0,0.0127,0.0,0.0,0.0,0.0],
			"285":[0.0415,0.0,0.0245,0.0,0.017,0.0,0.0,0.0,0.0]
  },
		"i":                                            # last 5 min of aggregate network interface metrics
  {
   "0":[0.0022,0.0018],                             # average received bytes in KB/s, average transmitted bytes in KB/s
			"15":[0.0016,0.0011],
           .........
			"270":[0.0014,0.0021],
			"285":[0.0036,0.0027]
  },
		"d":                                            # last 5 min of aggregate diskio metrics
  {
   "0":[0,6553],                                    # average bytes read in KB/s, average bytes written in KB/s
			"15":[0,192102],
        .........
			"270":[0,0],  
			"285":[0,0]
  }
 }
]
{% endhighlight %}  
  
  
###Example 2
---------
Obtain samples from a single system specifying sample_size of 60 seconds. Default keys.   
  
####CURL Command, and variations:  
{% highlight sh %}
curl -su <APIKEY>:U "https://api.copperegg.com/v2/revealcloud/samples.json?sample_size=60&uuids=<UUID>"

curl -s "https://<APIKEY>:U@api.copperegg.com/v2/revealcloud/samples.json?sample_size=60&uuids=<UUID>"

curl -s -XGET https://<APIKEY>:U@api.copperegg.com/v2/revealcloud/samples.json -H "Content-Type: application/json" -d '{"uuids":[<UUID>],"sample_size":60}'
{% endhighlight %}  
  
####CURL Response:  
  
Response is a JSON-encoded array of Server Sample Hashes, same as default except for 60 second samples.  

{% highlight sh %}
[
  {
    "a":{"p":1345214089},
    "uuid":"15e30940c372590c25df341af1fb7eed",
    "hid":0,
    "_ts":1345213680,
    "l_u":109954,
    "l_r":2,
    "l_b":0,
    "l_l":[0.77,1.19,1.46],
    "m":{
      "0":[9.42,14170.61,1522.83,45003.79],
      "60":[9.59,14303.58,1337.73,45055.75],
      "120":[9.44,14194.54,1463.34,45039.35],
      "180":[9.37,14328.52,1305.38,45063.39]
    },
    "s":{
      "0":[0.0,0.0],
      "60":[0.0,0.0],
      "120":[0.0,0.0],
      "180":[0.0,0.0]
    },
    "c":{
      "0":[0.1639,0.0018,0.0894,0.0,0.0574,0.0,0.0038,0.0114,0.0],
      "60":[0.1683,0.003,0.0907,0.0,0.0609,0.0,0.0038,0.0099,0.0],
      "120":[0.249,0.0064,0.1396,0.0,0.0827,0.0,0.0048,0.0154,0.0],
      "180":[0.1686,0.0021,0.093,0.0,0.0592,0.0,0.0039,0.0104,0.0]
    },
    "i":{
      "0":[251809.301,294678.256],
      "60":[251944.56,294839.16],
      "120":[252073.715,294992.258],
      "180":[252211.661,295158.556]
    },
    "d":{
      "0":[150015,19809245],
      "60":[318702,19733230],
      "120":[686489,24908697],
      "180":[535688,18995984]
    }
  }
]
{% endhighlight %}  
  

###Example 3
---------
Obtain samples from a single system specifying sample_size of 60 seconds, and separate network interface metrics.  
  

####CURL Command, and variations:  
{% highlight sh %}
curl -su <APIKEY>:U "https://api.copperegg.com/v2/revealcloud/samples.json?sample_size=60&uuids=<UUID>&keys=s_i"

curl -s < "https://APIKEY>:U@api.copperegg.com/v2/revealcloud/samples.json?sample_size=60&uuids=<UUID>&keys=s_i"

curl -s -XGET https://<APIKEY>:U@api.copperegg.com/v2/revealcloud/samples.json -H "Content-Type: application/json" -d '{"uuids":[<UUID>],"sample_size":60,"keys":["s_l"]}'
{% endhighlight %}  
  

####CURL Response:  
  
Response is a JSON-encoded array, containing one Server Sample Hash, with one set of data for each network interfaace.  
  
{% highlight sh %}
[
  {
    "a":{"p":1345215880},
    "uuid":"15e30940c372590c25df341af1fb7eed",
    "hid":0,
    "_ts":1345215480,
    "s_i":{                   #  network interface samples, averaged over 60 seconds, indexed by sample timestamp
      "eth0":{                # for interface 'eth0'
        "0":[1.1232,1.5572],  # (rx KB/s average, tx KB/s average)
        "60":[1.1376,1.5635],
        "120":[1.0717,1.4677],
        "180":[1.0941,1.4834]
      },
      "lo":{                  # for interface 'lo'
        "0":[1.1346,1.1346],
        "60":[1.1354,1.1354],
        "120":[1.0998,1.0998],
        "180":[1.0857,1.0857]
      }
    }
  }
]
{% endhighlight %}  


###Example 4
---------
Obtain the latest health samples from a single system.
  

####CURL Command, and variations:  
{% highlight sh %}
curl -su <APIKEY>:U "https://api.copperegg.com/v2/revealcloud/samples.json?uuids=<UUID>&keys=l_h"

curl -s < "https://APIKEY>:U@api.copperegg.com/v2/revealcloud/samples.json?uuids=<UUID>&keys=l_h"

curl -s -XGET https://<APIKEY>:U@api.copperegg.com/v2/revealcloud/samples.json -H "Content-Type: application/json" -d '{"uuids":[<UUID>],"keys":["l_h"]}'
{% endhighlight %}  
  

####CURL Response:  
  
Response is a JSON-encoded array, containing one Server Sample Hash, with one set of data for each network interfaace.  
  
{% highlight sh %}
[
  {
    "uuid":"15e30940c372590c25df341af1fb7eed",
    "a":{
      "p":1384756036
    },
    "hid":0,
    "_ts":1384755735,
    "_bs":5,
    "l_h":[
      0.88,           # health index ( 0 to 1 )
      2,              # health state (0=unknown, 1=ok, 2=warning, 3=critical)
      1,              # uptime state (0=unknown, 1=ok, 2=warning, 3=critical)
      1,              # processes state (0=unknown, 1=ok, 2=warning, 3=critical)
      1,              # load state (0=unknown, 1=ok, 2=warning, 3=critical)
      1,              # cpu state (0=unknown, 1=ok, 2=warning, 3=critical)
      3,              # memory state (0=unknown, 1=ok, 2=warning, 3=critical)
      1,              # last updated state (0=unknown, 1=ok, 2=warning, 3=critical)
      1.0,            # filesystem health index ( 0 to 1 )
      1               # filesystem state (0=unknown, 1=ok, 2=warning, 3=critical)
    ]
  }
]
{% endhighlight %}  

  
###Example 5
---------
Obtain samples from a single system focusing only on processes.  
  
####CURL Command, and variations:  
{% highlight sh %}
curl -su <APIKEY>:U "https://api.copperegg.com/v2/revealcloud/samples.json?uuids=<UUID>&keys=l_p,l_r,l_b"

curl -s  "https://<APIKEY>:Uapi.copperegg.com/v2/revealcloud/samples.json?uuids=<UUID>&keys=l_p,l_r,l_b"

curl -s -XGET https://<APIKEY>:U@api.copperegg.com/v2/revealcloud/samples.json -H "Content-Type: application/json" -d '{"uuids":[<UUID>],"keys":["l_p","l_r","l_b"}'
{% endhighlight %}  
  
  
####CURL Response:   
  
Response is a JSON-encoded array containing one or more Server Sample Hashes, containing the most recent process data.  
In this particular example, the returned array contains a single Server Sample Hash.

{% highlight sh %}
[ 
 { 
  "_bs" : 5,
  "_ts" : 1364960230,
  "a" : { "p" : 1364960395 },
  "hid" : 0,
  "l_p" : 
   "{
    "p":
    [
      ["launchd",null,1,"0","S",0.000038,0.000063,0.000101,0,2569023488,2809856,0.000000],
      ["accountsd",null,10056,"501","S",0.000001,0.000002,0.000003,0,2587201536,5865472,0.000000],
      ["aosnotifyd",null,10057,"0","S",0.000001,0.000002,0.000003,0,2587017216,6000640,0.000000],
      ["locationd",null,10060,"205","S",0.000000,0.000001,0.000001,0,2591932416,8421376,0.000000],
      ["com.apple.hiserv",null,10430,"501","S",0.000000,0.000000,0,0,2567585792,4648960,0.000000],
      ["coresymbolicatio",null,10593,"0","S",0.000000,0.000000,0,0,2567004160,4665344,0.000000],
      ["CVMServer",null,107,"0","S",0.000000,0.000000,0,0,2626015232,1830912,0.000000],
      ["launchd",null,109,"88","S",0.000000,0.000000,0,0,2568433664,999424,0.000000],
      ["UserEventAgent",null,11,"0","S",0.000001,0.000001,0.000001,0,2587164672,6373376,0.000000],
      ["cfprefsd",null,112,"88","S",0.000000,0.000000,0,0,2532257792,1134592,0.000000],
      ["com.apple.ShareK",null,11357,"501","S",0.000000,0.000000,0,0,2608812032,13807616,0.000000],
      ["kextd",null,12,"0","S",0.000000,0.000001,0.000001,0,2567913472,5349376,0.000000],
      ["launchd",null,12391,"200","S",0.000000,0.000000,0,0,2568433664,1003520,0.000000],
      ["notifyd",null,14,"0","S",0.000046,0.000090,0.000137,0,2577952768,2232320,0.000000],
      ["ssh-agent",null,15786,"501","S",0.000000,0.000000,0,0,2575478784,3354624,0.000000],
      ["httpd",null,16,"0","S",0.000001,0.000003,0.000004,0,2494636032,4382720,0.000000],
      ["com.apple.iCloud",null,16062,"501","S",0.000004,0.000011,0.000015,0,2590511104,10678272,0.000000],
      ["taskgated",null,16145,"0","S",0.000000,0.000000,0,0,2524430336,2039808,0.000000],
      ["revealcloud",null,16147,"0","S",0.000000,0.000000,0,0,2763124736,242524160,0.000000],
      ["revealcloud",null,16149,"0","R",0.000316,0.000370,0.000686,0,2797514752,3944448,0.000000],
      ["warmd",null,18,"-2","S",0.000000,0.000000,0,0,2570420224,7675904,0.000000],
      ["usbmuxd",null,19,"213","S",0.000000,0.000000,0,0,2575851520,2699264,0.000000],
      ["logind",null,208,"0","S",0.000000,0.000000,0,0,2566336512,2158592,0.000000],
      ["syslogd",null,21,"0","S",0.000038,0.000062,0.000100,0,2579668992,2121728,0.000000],
      ["netbiosd",null,214,"222","S",0.000000,0.000000,0,0,2597040128,5120000,0.000000],
      ["launchd",null,219,"501","S",0.000026,0.000044,0.000070,0,2568572928,1859584,0.000000],
      ["UserEventAgent",null,222,"501","S",0.000013,0.000011,0.000023,0,2603483136,11644928,0.000000],
      ["Finder",null,235,"501","S",0.000102,0.000095,0.000197,0,2866835456,105963520,0.000000],
      ["pbs",null,8877,"501","S",0.000002,0.000003,0.000005,0,2571067392,10436608,0.000000],
      ["WindowServer",null,93,"88","S",0.000477,0.000344,0.000820,0,3503648768,208084992,0.000000],
      ["httpd",null,94,"70","S",0.000000,0.000000,0,0,2494636032,716800,0.000000],
      ["tccd",null,9592,"501","S",0.000001,0.000002,0.000002,0,2590035968,5185536,0.000000],
      ["ntpd",null,97,"0","S",0.000002,0.000006,0.000008,0,2562572288,1712128,0.000000],
      ["cupsd",null,98,"0","S",0.000048,0.000013,0.000061,0,2606755840,4665344,0.000000],
      ["SystemStarter",null,99,"0","S",0.000000,0.000000,0,0,2561105920,1327104,0.000000]
    ],
    "u":
    [
     [0,0.013830,0.006750,0.020580,0,122491092992,803528704,0],
     [205,0.000000,0.000001,0.000001,0,2591932416,8421376,0],
     [501,0.015008,0.002462,0.017471,0,174283161600,3252830208,0],
     [65,0.000011,0.000013,0.000024,0,2578227200,4714496,0],
     [88,0.000477,0.000344,0.000820,0,8604340224,210219008,0],
     [89,0.000036,0.000053,0.000089,0,7722815488,4562944,0]
    ]
   }",
  "l_p_ts" : 160,
  "uuid" : "ac1f5ef85c1177ef97596f334f877370"
 } 
]
{% endhighlight %}


