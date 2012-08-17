---
layout: default
title: RevealCloud - Samples
---



Overview
--------
The API call for obtaining samples has a fair amount of detail, unlike many of the other CopperEgg API calls. The calling parameters and abbreviations that appear in the data structures are documented at the outset. The ideal way to get started is to scan the early sections, and then dig into the examples. Refer back to the parameters, keys and abbreviations when necessary, once you have gotten a feel for using the API.  
  
  
###Required Parameters:  
  
  
* uuids  
    You must specify at least one system uuid. Up to 20 uuids can be specified in each request. Multiple uuids can be formatted as either a comma separated string, or an array represented by multiple HTTP parameters named “uuids\[ \]”  
      
  

###Optional Parameters:  
  
* starttime  
    An integer unix timestamp (seconds since epoch) representing the beginning of your query timeframe. (NOTE: if neither starttime or endtime are provided, the last 5 minutes of samples are returned)  
  
* endtime  
    An integer unix timestamp (seconds since epoch) representing the end of your query timeframe. (NOTE: if neither starttime or endtime are provided, the last 5 minutes of samples are returned)  
  
* keys  
    A list of keys you want to include (see "key reference"). This can either be a comma separated string, or an array represented by multiple HTTP parameters named "keys\[ \]".  Default: "l_u,l_r,l_b,l_l,m,s,c,i,d".  
  
* sample_size  
    Override the default sample size that is determined by the starttime/endtime range. This will only work if you specify a sample_size larger than what is automatically calculated for the time range. If you specify a smaller sample_size, the default sample_size will be used. Valid sample size values are: 5, 15, 60, 300, 900, 3600, 21600, 86400.  
  
  
          
###RevealCloud Keys
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
filesystems              s_f, l_s_f
diskio                d, l_d, s_d, l_s_d
processes             p, l_p
{% endhighlight %}
Note:
* the prefacing ‘l_’ means ‘latest’; return most recent sample data.
* the prefacing ‘s_’ means 'separated'; return data from individual components 
   

    
###Other RevealCloud Abbreviations
{% highlight sh %}
term               abbreviation
timestamp             '_ts'
attributes            'a'
system uuid           'uuid'
{% endhighlight %}  
        

    
Example 1  
---------  
Obtain samples from one system, specifying only the UUID. This will demonstrate the default set of data returned when no keys are included in the command, and he starttime and endtime are not specified.
As noted above, the default keys are "l_u,l_r,l_b,l_l,m,s,c,i,d".  

CURL Command:
{% highlight sh %}
curl -u APIKEY:U "http://api.copperegg.com/v2/revealcloud/samples.json?uuids=UUID"
{% endhighlight %}

CURL Response:  

Response is a JSON array of default system Sample hash.   

{% highlight sh %}
[
  {
    "a":{"p":1345166746},                         # attributes (only last_updated is included)
    "uuid":"15e30940c372590c25df341af1fb7eed",    # system unique identifier
    "hid":0,                                      # 1=hidden, 0=visible (not present means visible)
    "_ts":1345166445,                             # timestamp at '0'
    "l_u":62813,                                  # last uptime (in seconds)
    "l_r":1,                                      # last number of running processes
    "l_b":0,                                      # last number of blocked processes
    "l_l":[1.04,1.68,1.79],                       # last load (short, mid, long)  
    "m":{                                         # memory samples indexed by sample timestamp, (buffer MB, cached MB, free mb, used MB)
      "0":[10.64,17711.86,5493.46,37490.69],
      "5":[10.64,17703.81,5490.33,37501.88],
      "10":[10.65,17716.04,5471.98,37507.98],  
                    .... ,  
      "300":[11.0,17777.67,5170.44,37747.55],  
      "305":[11.01,17804.17,5123.29,37768.18]      # last memory sample
    },
    "s":{                                          # swap samples indexed by sample timestamp, (swap used MB, swap free MB)
      "0":[0.0,0.0],
      "5":[0.0,0.0],  
          .... ,  
      "300":[0.0,0.0],  
      "305":[0.0,0.0]                              # last swap sample
    },
    "c":{                                          # last aggregated cpu sample in % (active, iowait, user, nice, system, irq, softirq, steal, guest) 
      "0":[0.0721,0.0001,0.0241,0.0,0.0393,0.0,0.0033,0.0054,0.0],    # note that 1-active = idle.  everything else is the breakdown of active.
      "5":[0.2616,0.0011,0.1671,0.0,0.0786,0.0,0.0046,0.0101,0.0],    # also note, these may not exactly add up due to rounding error
                    .... ,  
      "300":[0.1301,0.0001,0.0665,0.0,0.0526,0.0,0.004,0.0069,0.0],
      "305":[0.2106,0.0013,0.1236,0.0,0.0723,0.0,0.0054,0.0081,0.0]   # last cpu sample
    },
    "i":{                                          # aggregated network interface samples indexed by sample timestamp,
      "0":[145110.824,171367.119],                 # (rx KB/s average, tx KB/s average)
      "5":[145122.128,171381.055],
                .... ,  
      "300":[145801.064,172177.116],
      "305":[145813.101,172190.545]                # last network interface sample
    },
    "d":{                                          # aggregated diskio samples indexed by sample timestamp
      "0":[3686,3665510],    
      "5":[124518,19208192],
               .... ,  
      "300":[3276,8188723],
      "305":[6553,10753228]                        # last diskio sample
    }
  }
]
{% endhighlight %}  

  
Example 2  
---------
Obtain samples from a single system (with UUID 15e30940c372590c25df341af1fb7eed, same as above), specifying sample_size of 60 seconds. Default keys.  

CURL Command:
{% highlight sh %}
curl -u APIKEY:U "http://api.copperegg.com/v2/revealcloud/samples.json?sample_size=60&uuids=UUID"
{% endhighlight %}

CURL Response:

Response is a JSON array of system Sample hashes, same as default except for 60 second samples.   

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

  
Example 3
---------
Obtain samples from a single system (with UUID 15e30940c372590c25df341af1fb7eed, same as above), specifying sample_size of 60 seconds, and separate network interface metrics. 
  

CURL Command:
{% highlight sh %}
curl -u APIKEY:U "http://api.copperegg.com/v2/revealcloud/samples.json?sample_size=60&uuids=UUID&keys=s_i"
{% endhighlight %}
  

CURL Response:  
  
Response is a JSON array of Sample hashes, one for each network interface. Notice that as specified, the sample sizes returned at 60 seconds. 

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

Example 4
---------
Obtain samples from a single system (with UUID 15e30940c372590c25df341af1fb7eed, same as above), focusing only on processes.
  
CURL Command:
{% highlight sh %}
curl -u APIKEY:U "http://api.copperegg.com/v2/revealcloud/samples.json?uuids=UUID&keys=l_p,l_r,l_b"
{% endhighlight %}
  
The format of the process and user arrays are described below. The examples are from the example below, with escape characters removed.  

{% highlight sh %}
Process array: 
[
  "bash",       # process name (string, case sensitive)
  null,         # internal use
  53479,        # PID (number)
  "1001",       # UID (number formatted as a string)
  "S",          # state 
  0,            # CPU % User, this process     (number, range 0 to 1)
  0,            # CPU % System, this process   (number, range 0 to 1)
  0,            # CPU % Total, this process    (number, range 0 to 1)
  1,            # internal use
  27881472,     # Memory Virtual, this process  (number, in bytes)
  9695232,      # Memory Resident, this process (number, in bytes)
  0             # internal use
]  
  
User array: 
[
  501,          # UID (number)
  0.051497,     # CPU % User, this user    (number, range 0 to 1)
  0.005440,     # CPU % System, this user  (number, range 0 to 1)
  0.056938,     # CPU % Total, this user   (number, range 0 to 1)
  0,            # internal use
  212672065536, # Memory Virtual, this user  (number, in bytes)
  4214882304,   # Memory Resident, this user (number, in bytes) 
  0             # internal use
]  
  
  
Additional notes:  
* state   
  The state is given by a sequence of characters, where the first character indicates the run state of the process.  
The state symbol is passed from the OS, without translation. If a symbol appears that is not included below, please check your OS documentation.  
  
  * I       Marks a process that is idle (sleeping for longer than about 20 seconds).
  * R       Marks a runnable process.
  * S       Marks a process that is sleeping for less than about 20 seconds.
  * T       Marks a stopped process.
  * U       Marks a process in uninterruptible wait.
  * Z       Marks a dead process (a ``zombie'').
{% endhighlight %}  
  

CURL Response:  
  
Response is a JSON array of sample hashes, containing the most recent process data. The response is an array of hashes because more than one uuid may be included in a single command. In this particular example, the returned array contains a single Sample hash.  
  
{% highlight sh %}
[
  {
    "a":{"p":1345217126},
    "uuid":"15e30940c372590c25df341af1fb7eed",
    "hid":0,
    "_ts":1345216740,
    "l_p":"{                       # most recent process list
      \"p\":[
        [\"System\",null,null,null,\"-\",0,0.000125,0.000125,76,25022464,1679360,0],
        [\"revealcloud\",null,16048,\"999\",\"-\",0.001750,0.006375,0.008125,15,1016483840,5582848,0],
        [\"getty\",null,16076,\"0\",\"-\",0,0,0,2,14843904,819200,0],
        [\"udevd\",null,384,\"0\",\"-\",0,0,0,8,65806336,2572288,0],
        [\"dhclient3\",null,4173,\"0\",\"S\",0,0,0,1,7430144,757760,0],
        [\"sshd\",null,4210,\"0\",\"S\",0,0,0,1,51146752,1462272,0],
        [\"ntpd\",null,4457,\"0\",\"-\",0,0,0,7,38584320,1732608,0],
        [\"iostat\",null,5177,\"1001\",\"S\",0,0,0,1,4435968,782336,0],
        [\"sshd\",null,53475,\"0\",\"S\",0,0,0,1,75112448,1216512,0],
        [\"sshd\",null,53476,\"0\",\"S\",0,0,0,1,75112448,1216512,0],
        [\"bash\",null,53479,\"1001\",\"S\",0,0,0,1,27881472,9695232,0],
        [\"bash\",null,53482,\"1001\",\"S\",0,0,0,1,27885568,9801728,0],
        [\"sh\",null,5368,\"0\",\"S\",0,0,0,1,4497408,548864,0],
        [\"nginx\",null,5509,\"0\",\"-\",0.002250,0.005250,0.007500,9,684847104,122929152,0],
        [\"ruby\",null,8225,\"1001\",\"-\",0.000875,0.002250,0.003125,15,1273081856,233623552,0],
        [\"ruby\",null,8245,\"1001\",\"-\",0.000625,0.000125,0.000750,10,1446060032,553877504,0],
        [\"getty\",null,875,\"0\",\"S\",0,0,0,1,14843904,815104,0],
        [\"getty\",null,883,\"0\",\"S\",0,0,0,1,14843904,815104,0],
        [\"acpid\",null,903,\"0\",\"S\",0,0,0,1,4423680,589824,0],
        [\"irqbalance\",null,930,\"0\",\"S\",0,0,0,1,16355328,696320,0]
      ],
      \"u\":[                      # most recent user list
        [0,0.015250,0.024250,0.039500,141,3216269312,1129074688,0],
        [1001,0.017500,0.024625,0.042125,10066,149139898368,36825632768,0],
        [999,0.001750,0.006375,0.008125,15,1016483840,5582848,0]
      ]
    }",
    "l_r":2,                        # number of running processes
    "l_b":0                         # number of blocked processes
  }
]
{% endhighlight %}
  
  


