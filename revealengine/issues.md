---
layout: default
title: RevealEngine - Issues
---

Index
-----

CURL Command:
{% highlight sh %}
curl -u pxAJ7BSmPXXl3k9W:U https://api.copperegg.com/v2/alerts/issues.json
{% endhighlight %}

CURL Response:

Response is JSON with an array of all issues.

{% highlight javascript %}
[
  {
    "id":"50183b776cc66909b7758065","state":"cleared","short_msg":"my_website: Lores_Health (Health Index 90% < 95%)",
    "attr_description":"Additional Information",
    "attrs":[
      ["label","my_website","],               // probe label
      ["description","Lores_Health"],         // alert description
      ["destination","http://mywebsite.com"], // probe dest URL
      ["frequency","60"],
      ["type","GET"]
    ],
    "type":"ce_revealuptime",
    "created_at":1343765367,
    "updated_at":1343765380,
    "cleared_date":1343765380,
    "notified_date":1343765368,
    "ignore_until":1343765372,
    "annotation_id":"",
    "obj_idv":"5004a81187517319f4000238|cjwTwDzL2q9QE8x16fGrSGoVRUPm0Jrk|"
  },
  {
    "id":"50183b796cc66909b775807c","state":"cleared","short_msg":"my_website: Hires_Uptime (Uptime 86% < 90%) ",
    "attr_description":"Additional Information",
    "attrs":[
      ["label","my_website","],               // probe label
      ["description","Hires_Uptime"],         // alert description
      ["destination","http://mywebsite.com"], // probe dest URL
      ["frequency","15"],
      ["type","GET"]
    ],
    "type":"ce_revealuptime",
    "created_at":1343765368,
    "updated_at":1343765379,
    "cleared_date":1343765379,
    "notified_date":1343765369,
    "ignore_until":1343765373,
    "annotation_id":"",
    "obj_idv":"5004a884b0175d20c00000be|2BStibjEMVMGA34daPVpNnU7zQKAspes|"
  },
  {
    "id":"501fe1696cc66909b77648e3","state":"cleared","short_msg":"my_website: Hires_Latency (Response Time 3106 ms > 3000.0 ms) ",
    "attr_description":"Additional Information",
    "attrs":[
      ["label","my_website","],               // probe label
      ["description","Hires_Latency"],        // alert description
      ["destination","http://mywebsite.com"], // probe dest URL
      ["frequency","15"],
      ["type","GET"]
    ],
    "type":"ce_revealuptime",
    "created_at":1344266601,
    "updated_at":1344266683,
    "cleared_date":1344266683,
    "notified_date":1344266601,
    "ignore_until":1344266606,
    "annotation_id":"",
    "obj_idv":"501fdad0d9106a6976000006|dvb09eoPMqPrJipzHuQcqkRJjqc6Cp9x|"
  },
  { 
    "id":"501b40596cc66909b7760cd0","state":"cleared","short_msg":"DBServer: Lost nfsd (Process list does not contain nfsd)",
    "attr_description":"Additional Information",
    "attrs":[
      [
        "ce_processes","{
          \"p\":[
            [\"launchd\",null,1,\"0\",\"S\",0.000003,0.000003,0.000007,0,2568998912,2162688,0],
            [\"netbiosd\",null,104,\"222\",\"S\",0,0,0,0,2597040128,3117056,0],[\"UserEventAgent\",null,11,\"0\",\"S\",0,0,0,0,2587148288,4882432,0],[\"CVMServer\",null,114,\"0\",\"S\",0,0,0,0,2592595968,1576960,0],[\"login\",null,11526,\"0\",\"S\",0,0,0,0,2538340352,4784128,0],[\"zsh\",null,11527,\"501\",\"S\",0,0,0,0,2493644800,3256320,0],[\"bash\",null,11567,\"501\",\"S\",0,0,0,0,2491838464,1290240,0],[\"kextd\",null,12,\"0\",\"S\",0,0,0,0,2570461184,4075520,0],[\"usbmuxd\",null,12591,\"213\",\"S\",0,0,0,0,2578001920,3567616,0],[\"coreaudiod\",null,130,\"202\",\"S\",0,0,0,0,2579312640,11640832,0],[\"logind\",null,131,\"0\",\"S\",0,0,0,0,2566336512,1695744,0],[\"ssh-agent\",null,13548,\"501\",\"S\",0,0,0,0,2574430208,3137536,0],[\"launchd\",null,137,\"501\",\"S\",0.000008,0.000020,0.000029,0,2568564736,1261568,0],[\"notifyd\",null,14,\"0\",\"S\",0.000006,0.000006,0.000012,0,2577952768,1880064,0],[\"distnoted\",null,140,\"501\",\"S\",0.000004,0.000012,0.000016,0,2587471872,9814016,0],[\"pboard\",null,147,\"501\",\"S\",0,0,0,0,2493284352,401408,0],[\"fontd\",null,148,\"501\",\"S\",0,0,0,0,2619887616,6782976,0],[\"diskarbitrationd\",null,15,\"0\",\"S\",0,0,0,0,2566459392,2072576,0],[\"SystemUIServer\",null,152,\"501\",\"S\",0.000060,0.000047,0.000108,0,2778714112,36315136,0],[\"talagent\",null,154,\"501\",\"S\",0,0,0,0,2607443968,7471104,0],[\"securityd\",null,16,\"0\",\"S\",0,0,0,0,2589335552,7815168,0],[\"Terminal\",null,161,\"501\",\"S\",0.000017,0.000012,0.000030,0,2759577600,61239296,0],[\"diskimages-helpe\",null,16493,\"501\",\"S\",0,0,0,0,2577788928,5189632,0],[\"Dock\",null,169,\"501\",\"S\",0.000004,0.000002,0.000006,0,2715754496,49344512,0],[\"JewelryBox\",null,16947,\"501\",\"S\",0,0,0,0,19954356224,85581824,0],[\"powerd\",null,17,\"0\",\"S\",0.000001,0.000002,0.000002,0,2585518080,2424832,0],[\"Finder\",null,170,\"501\",\"S\",0.000037,0.000036,0.000072,0,4140310528,220651520,0],[\"NetworkBrowserAg\",null,173,\"501\",\"S\",0,0,0,0,2587217920,4157440,0],[\"filecoordination\",null,174,\"0\",\"S\",0,0,0,0,2573021184,5926912,0],[\"storeagent\",null,17495,\"501\",\"S\",0,0,0,0,3733344256,19673088,0],[\"maspushagent\",null,17523,\"501\",\"S\",0,0,0,0,2573131776,4554752,0],[\"configd\",null,18,\"0\",\"S\",0,0,0,0,2754359296,29265920,0],[\"httpd\",null,20,\"0\",\"S\",0.000001,0.000003,0.000005,0,2494619648,622592,0],[\"cfprefsd\",null,20371,\"501\",\"S\",0.000003,0.000008,0.000011,0,2571300864,7041024,0],[\"NotificationCent\",null,211,\"501\",\"S\",0.000128,0.000186,0.000314,0,2668707840,20353024,0],[\"usernoted\",null,212,\"501\",\"S\",0,0,0,0,2585980928,6578176,0],[\"com.apple.dock.e\",null,213,\"501\",\"S\",0.000000,0.000001,0.000001,0,2619453440,12800000,0],[\"apsd\",null,214,\"0\",\"S\",0.000001,0.000002,0.000002,0,2588852224,11395072,0],[\"warmd\",null,22,\"-2\",\"S\",0.000001,0.000003,0.000004,0,2572431360,5767168,0],[\"lsboxd\",null,235,\"501\",\"S\",0,0,0,0,2598920192,3543040,0],[\"syslogd\",null,25,\"0\",\"S\",0.000006,0.000009,0.000015,0,2579668992,1597440,0],[\"HipChat\",null,25320,\"501\",\"S\",0.000340,0.000081,0.000421,0,1434718208,560562176,0],[\"cfprefsd\",null,25670,\"0\",\"S\",0.000001,0.000004,0.000005,0,2566860800,1634304,0],[\"SleepServicesD\",null,25691,\"0\",\"S\",0,0,0,0,2533888000,1785856,0],[\"printtool\",null,25745,\"501\",\"S\",0,0,0,0,2566909952,3141632,0],[\"CalendarAgent\",null,25835,\"501\",\"S\",0.000002,0.000005,0.000007,0,2610409472,45006848,0],[\"launchd\",null,25890,\"89\",\"S\",0,0,0,0,2568433664,1003520,0],[\"distnoted\",null,25918,\"89\",\"S\",0,0,0,0,2585374720,1789952,0],[\"cfprefsd\",null,25919,\"89\",\"S\",0,0,0,0,2566860800,1384448,0],[\"imagent\",null,262,\"501\",\"S\",0,0,0,0,2589855744,5574656,0],[\"Google Chrome\",null,26571,\"501\",\"D\",0.003502,0.001164,0.004666,0,1166454784,150794240,0],[\"pbs\",null,26649,\"501\",\"S\",0,0,0,0,2569433088,3903488,0],[\"Google Chrome He\",null,26671,\"501\",\"S\",0,0,0,0,839241728,26431488,0],[\"Google Chrome He\",null,26677,\"501\",\"S\",0.000491,0.000169,0.000661,0,888680448,45826048,0],[\"Google Chrome He\",null,26678,\"501\",\"S\",0,0,0,0,838930432,25874432,0],[\"Google Chrome He\",null,26679,\"501\",\"S\",0.000005,0.000003,0.000008,0,878100480,33705984,0],[\"Google Chrome He\",null,26680,\"501\",\"S\",0.000006,0.000004,0.000010,0,839503872,26763264,0],[\"Google Chrome He\",null,26686,\"501\",\"S\",0.000083,0.000034,0.000117,0,896032768,49963008,0],[\"Google Chrome He\",null,26687,\"501\",\"S\",0.001866,0.000818,0.002684,0,912924672,56381440,0],[\"xpcd\",null,26865,\"501\",\"S\",0,0,0,0,2560811008,5017600,0],[\"Google Chrome He\",null,26884,\"501\",\"S\",0.000190,0.000106,0.000297,0,813322240,12861440,0],[\"stackshot\",null,27,\"0\",\"S\",0.000001,0.000004,0.000005,0,2567413760,823296,0],[\"UserEventAgent\",null,271,\"501\",\"S\",0.000205,0.000139,0.000344,0,2592509952,10899456,0],[\"SIMBL Agent\",null,283,\"501\",\"S\",0,0,0,0,19890212864,25952256,0],[\"UFR II BackGroun\",null,284,\"501\",\"S\",0.000003,0.000003,0.000006,0,763453440,1986560,0],[\"Canon FAX BackGr\",null,285,\"501\",\"S\",0.000002,0.000002,0.000004,0,729645056,1916928,0],[\"Canon CMFP BackG\",null,286,\"501\",\"S\",0.000002,0.000002,0.000004,0,729616384,1843200,0],[\"KodakAiOBonjourA\",null,287,\"501\",\"S\",0.000002,0.000003,0.000005,0,758861824,9605120,0],[\"Grabbit\",null,290,\"501\",\"S\",0,0,0,0,2622058496,8495104,0],[\"Canon MF Network\",null,292,\"501\",\"S\",0.000001,0.000002,0.000003,0,739639296,9170944,0],[\"Alfred\",null,298,\"501\",\"S\",0.000010,0.000007,0.000017,0,3722387456,14458880,0],[\"revisiond\",null,30,\"0\",\"S\",0.000001,0.000003,0.000004,0,2597154816,3821568,0],[\"AppleSpell\",null,315,\"501\",\"S\",0.000074,0.000009,0.000084,0,2621640704,19312640,0],[\"opendirectoryd\",null,33,\"0\",\"S\",0.000020,0.000025,0.000045,0,2592063488,10649600,0],[\"AirPort Base Sta\",null,334,\"501\",\"S\",0,0,0,0,2567041024,1716224,0],[\"mds\",null,36,\"0\",\"S\",0.000057,0.000050,0.000107,0,3790622720,244359168,0],[\"diskimages-helpe\",null,36406,\"501\",\"S\",0,0,0,0,2576211968,2387968,0],[\"hdiejectd\",null,36407,\"0\",\"S\",0,0,0,0,2561429504,1699840,0],[\"mDNSResponder\",null,37,\"65\",\"S\",0.000010,0.000011,0.000021,0,2578763776,4583424,0],[\"mdworker\",null,37189,\"501\",\"S\",0.000029,0.000024,0.000053,0,2583330816,19484672,0],[\"Google Chrome He\",null,37202,\"501\",\"S\",0.014209,0.001270,0.015479,0,983740416,163409920,0],[\"VMware Fusion\",null,37220,\"501\",\"S\",0.000208,0.000102,0.000310,0,4045484032,237023232,0],[\"vmware-usbArbitr\",null,37248,\"0\",\"S\",0.000001,0.000003,0.000004,0,2570342400,5816320,0],[\"VMware Fusion Se\",null,37251,\"0\",\"S\",0,0,0,0,2538479616,1216512,0],[\"vmnet-bridge\",null,37292,\"0\",\"S\",0,0,0,0,2557710336,3125248,0],[\"vmnet-netifup\",null,37295,\"0\",\"S\",0,0,0,0,2493587456,294912,0],[\"vmnet-dhcpd\",null,37297,\"0\",\"S\",0,0,0,0,2493710336,253952,0],[\"vmnet-natd\",null,37300,\"0\",\"S\",0.000003,0.000016,0.000019,0,2563305472,1892352,0],[\"vmnet-netifup\",null,37302,\"0\",\"S\",0,0,0,0,2493587456,294912,0],[\"vmnet-dhcpd\",null,37304,\"0\",\"S\",0,0,0,0,2493710336,532480,0],[\"helpd\",null,37329,\"501\",\"S\",0,0,0,0,2574307328,2523136,0],[\"Google Chrome He\",null,37473,\"501\",\"S\",0.000005,0.000002,0.000007,0,881463296,36118528,0],[\"Google Chrome He\",null,37483,\"501\",\"S\",0,0,0,0,888283136,34902016,0],[\"Google Chrome He\",null,37522,\"501\",\"S\",0.000001,0.000002,0.000002,0,905457664,50937856,0],[\"cupsd\",null,37944,\"0\",\"S\",0.000001,0.000002,0.000002,0,2558496768,4349952,0],[\"ocspd\",null,37952,\"0\",\"S\",0,0,0,0,2491404288,2007040,0],[\"ruby\",null,37954,\"501\",\"S\",0.000140,0.000306,0.000446,0,2537910272,24064000,0],[\"taskgated\",null,37955,\"0\",\"S\",0,0,0,0,2503458816,1970176,0],[\"ruby\",null,37957,\"501\",\"S\",0.000021,0.000046,0.000066,0,2506649600,15745024,0],[\"mdworker\",null,37961,\"501\",\"S\",0,0,0,0,2575298560,12025856,0],[\"vmware-vmx\",null,37966,\"0\",\"S\",0.002431,0.011326,0.013757,0,3914526720,1163055104,0],[\"mdworker\",null,37972,\"501\",\"S\",0,0,0,0,2590834688,12587008,0],[\"thnuclnt\",null,37974,\"501\",\"S\",0.000001,0.000006,0.000007,0,2493693952,3129344,0],[\"thnuclnt\",null,37976,\"501\",\"S\",0,0,0,0,2552954880,1851392,0],[\"thnuclnt\",null,37977,\"501\",\"S\",0,0,0,0,2492645376,323584,0],[\"thnuclnt\",null,37979,\"501\",\"S\",0,0,0,0,2493693952,299008,0],[\"thnuclnt\",null,37982,\"501\",\"S\",0,0,0,0,2493693952,212992,0],[\"thnuclnt\",null,37983,\"501\",\"S\",0.000020,0.000059,0.000079,0,2493693952,241664,0],[\"loginwindow\",null,40,\"501\",\"S\",0.000421,0.000249,0.000670,0,2719391744,18526208,0],[\"KernelEventAgent\",null,42,\"0\",\"S\",0,0,0,0,2551750656,765952,0],[\"kdc\",null,43,\"0\",\"S\",0.000001,0.000002,0.000003,0,2568159232,2068480,0],[\"TextEdit\",null,44522,\"501\",\"S\",0.000001,0.000003,0.000004,0,3824128000,39366656,0],[\"hidd\",null,45,\"0\",\"S\",0.000890,0.000751,0.001641,0,2569089024,3514368,0],[\"fseventsd\",null,46,\"0\",\"S\",0.000016,0.000080,0.000096,0,2609983488,14626816,0],[\"httpd\",null,46199,\"70\",\"S\",0,0,0,0,2494619648,1662976,0],[\"Mail\",null,47337,\"501\",\"S\",0.000005,0.000007,0.000012,0,4721381376,354377728,0],[\"WebKitPluginAgen\",null,47509,\"501\",\"S\",0,0,0,0,2562682880,995328,0],[\"dynamic_pager\",null,48,\"0\",\"S\",0,0,0,0,2491166720,430080,0],[\"appleeventsd\",null,51,\"71\",\"S\",0,0,0,0,2585939968,2985984,0],[\"login\",null,51072,\"0\",\"S\",0,0,0,0,2528903168,3227648,0],[\"zsh\",null,51073,\"501\",\"S\",0,0,0,0,2494758912,3235840,0],[\"Microsoft PowerP\",null,52682,\"501\",\"S\",0.000203,0.000109,0.000311,0,1196818432,126967808,0],[\"Microsoft AU Dae\",null,52687,\"501\",\"S\",0,0,0,0,729964544,3117056,0],[\"httpd\",null,53856,\"70\",\"S\",0,0,0,0,2494619648,1617920,0],[\"blued\",null,54,\"0\",\"S\",0.000001,0.000004,0.000005,0,2587074560,7589888,0],[\"autofsd\",null,56,\"0\",\"S\",0,0,0,0,2566979584,1691648,0],[\"Microsoft Word\",null,57860,\"501\",\"S\",0.000251,0.000114,0.000365,0,1612648448,149897216,0],[\"distnoted\",null,60,\"0\",\"S\",0,0,0,0,2585374720,4390912,0],[\"installd\",null,61913,\"0\",\"S\",0.000001,0.000002,0.000002,0,2642505728,75984896,0],[\"FreeMemory\",null,61941,\"501\",\"S\",0.000044,0.000005,0.000049,0,2669891584,12181504,0],[\"coreservicesd\",null,62,\"0\",\"S\",0.000010,0.000009,0.000018,0,2641518592,16121856,0],[\"geod\",null,62535,\"56\",\"S\",0,0,0,0,2566537216,3780608,0],[\"revealcloud\",null,62890,\"0\",\"S\",0,0,0,0,2560847872,5087232,0],[\"revealcloud\",null,62894,\"0\",\"R\",0.000309,0.000470,0.000779,0,2565988352,7286784,0],[\"VMware Fusion St\",null,638,\"501\",\"S\",0,0,0,0,2608820224,6356992,0],[\"DashboardClient\",null,76336,\"501\",\"S\",0.000001,0.000003,0.000004,0,3738140672,23670784,0],[\"login\",null,82565,\"0\",\"S\",0,0,0,0,2527854592,3469312,0],[\"zsh\",null,82566,\"501\",\"S\",0,0,0,0,2493644800,1830912,0],[\"bash\",null,82637,\"501\",\"S\",0,0,0,0,2491838464,913408,0],[\"Sublime Text 2\",null,83846,\"501\",\"S\",0,0,0,0,2710155264,35696640,0],[\"appleprofilepoli\",null,90426,\"0\",\"S\",0,0,0,0,2491166720,417792,0],[\"networkd\",null,92,\"24\",\"S\",0,0,0,0,2566905856,1388544,0],[\"TextWrangler\",null,92639,\"501\",\"S\",0.001355,0.000187,0.001541,0,1592455168,680062976,0],[\"WindowServer\",null,93,\"88\",\"S\",0.001999,0.000763,0.002762,0,3631882240,155607040,0],[\"httpd\",null,94,\"70\",\"S\",0,0,0,0,2494619648,1331200,0],[\"syspolicyd\",null,963,\"0\",\"S\",0,0,0,0,2586939392,5038080,0],[\"login\",null,96768,\"0\",\"S\",0,0,0,0,2547777536,3268608,0],[\"zsh\",null,96769,\"501\",\"S\",0,0,0,0,2493644800,1650688,0],[\"bash\",null,96851,\"501\",\"S\",0,0,0,0,2491838464,983040,0],[\"ntpd\",null,98,\"0\",\"S\",0.000002,0.000006,0.000008,0,2560475136,1245184,0],[\"SystemStarter\",null,99,\"0\",\"S\",0,0,0,0,2559008768,745472,0]
            
            ],
          \"u\":[
            [-2,0.000001,0.000003,0.000004,0,2572431360,5767168,0],
            [0,0.003760,0.012779,0.016539,0,138357985280,1688731648,0],
            [501,0.023961,0.005368,0.029330,0,221265072128,3804700672,0],[65,0.000010,0.000011,0.000021,0,2578763776,4583424,0],
            [88,0.001999,0.000763,0.002762,0,3631882240,155607040,0]
          ]
        }"
      ],
      ["hostname","mysql_1.localdomain"],
      ["label","DBServer"]
    ],
    "type":"ce_revealcloud",
    "created_at":1343963225,
    "updated_at":1343963357,
    "cleared_date":1343963357,
    "notified_date":1343963228,
    "ignore_until":1343963230,
    "annotation_id":"",
    "obj_idv":"ac1f5ef85c1177ef97596f334f877370|"
  }
]
{% endhighlight %}


Show
----
Show in-depth information about a single issue.

Required Parameters: the id of the issue of interest; in the example below, the id is 188.

CURL Command:
{% highlight sh %}
curl -u pxAJ7BSmPXXl3k9W:U https://api.copperegg.com/v2/alerts/issues/188.json
{% endhighlight %}

CURL Response:

Response is JSON with a structure containing details of the specified issue:
{% highlight javascript %}
{
  "id":188,
  "state":"notified",
  "short_msg":"fastapi-7c-1: Memory Use - High (Active Memory 0.958 >= 0.95)",
  "attr_description":"Additional Information",
  "attrs":{
    "aws_profile":"default-paravirtual",
    "hostname":"fastapi-7c-1",
    "aws_availability_zone":"us-east-1b",
    "linux_distro":"Ubuntu 12.04 LTS \\n \\l\n",
    "aws_public_hostname":"ec2-174-129-80-99.compute-1.amazonaws.com",
    "aws_reservation_id":"r-fa90679e",
    "aws_inst_type":"c1.xlarge",
    "aws_hostname":"ip-10-42-90-138.ec2.internal",
    "aws_public_ipv4":"174.129.80.99",
    "aws_ami_id":"ami-0674d66f",
    "aws_sec_group":"API Server",
    "aws_local_hostname":"ip-10-42-90-138.ec2.internal",
    "aws_inst_id":"i-941c58ec",
    "aws_mac_addr":"12:31:38:1F:74:7C",
    "aws_local_ipv4":"10.42.90.138",
    "aws_kernel_id":"aki-825ea7eb"
  },
  "type":"ce_revealcloud",
  "created_at":1344521344,
  "updated_at":0,
  "cleared_at":0,
  "notified_at":1344521506,
  "ignore_until":1344521349,
  "annotation_id":"",
  "obj_idv":"d16b38d742a8ada6ccc7b8b33d5eb7dd|"
}

{% endhighlight %}



Update 
----
Update a single issue.

Required Parameters: the id of the issue of interest; in the example below, the id is 188.

CURL Command:
{% highlight sh %}
curl -XPUT https://EUBJAOOIUHmFsMdl:U@api.copperegg.com/v2/alerts/issues/188.json -d "state=cleared"
{% endhighlight %}

CURL Response:

{% highlight javascript %}
{
}
{% endhighlight %}


Remove
----
Remove a single issue.

Required Parameters: the id of the issue of interest; in the example below, the id is 188.

CURL Command:
{% highlight sh %}
curl -XPUT https://EUBJAOOIUHmFsMdl:U@api.copperegg.com/v2/alerts/issues/188.json -d "state=deleted"
{% endhighlight %}

CURL Response:

{% highlight javascript %}
{
}
{% endhighlight %}



The Issue structure:
{% highlight sh %}
{ 

{% endhighlight %}


Definition of fields in the Issue structure:
* "id":"188" :          Unique id for this issue structure. Read-only string.

* "state":"cleared"     Current state of this issue. "active", "notified", cleared", 
                        and "deleted". Read / Write string. Writing is limited to 
                        Updating, and only for writoing "cleared and "deleted". Any other 
                        value writtne will be silently ignored.

* "short_msg":"DBServer: CPU-total (CPU Total Usage 0.945 > 0.9)" 
                        This string is a human-readable description of what triggered
                        this specific alert. Read-only.

* "attr_description":"Additional Information"           
                        A string describing the contents of the following 'attrs' field,
                        which may be useful for parsing its contents. Read-only.

* "attrs":{ "hostname","DBtier-s1",  "label","DBServer" }           
                        A hash containing information pertinent to the issue. This 
                        information may be different for different hosts. Read-only.
  
* "type":"ce_revealcloud"   Type of issue, "ce_revealcloud" or "ce_revealuptime". 
                            Read-only, string.

* "created_at":1344631403       Time of alert & issue creation, UTC -> unix timestamp
* "updated_at":1344632039       Time of most recent update.
* "cleared_date":0,             Time when the issue was cleared, or 0.
* "notified_date":1344631404    Time when notified, or 0.
* "ignore_until":1344631408,    *** don't know *** 
* "annotation_id":"",           Associated annotation, if any.
* "obj_idv":"ac1f5ef85c1177ef97596f334f877370|"     Ignore this field.



{
    "id":"502940cafbaa0e9224a3d1f3",
    "state":"cleared",
    "short_msg":"Herkoku-app: Slow Response Time (Response Time 110 ms >= 40.0 ms) ",
    "attr_description":"Additional Information",
    "attrs":[
      ["label","Herkoku-app"],
      ["description","Herkoku-app"],
      ["destination","http://peaceful-lake-1814.herokuapp.com"],
      ["frequency","15"],["type","GET"]
    ],
    "type":"ce_revealuptime",
    "created_at":1344880840,
    "updated_at":1344880853,
    "cleared_date":1344880853,
    "notified_date":1344880842,
    "ignore_until":1344880845,
    "annotation_id":"",
    "obj_idv":"50271cebd9106a2208000004|bjiRJTlKgfnOLq5ecb3jxaA3OmrGGqMt|"
  }



{
  "id":"188",                                  // Unique id for this issue
  "state":"cleared",                           // current state of the issue
  "short_msg":"DBServer: CPU-total (CPU Total Usage 0.945 > 0.9)",
  "attr_description":"Additional Information",  
  "attrs":[                                    // attributes may differ by host
    ["hostname","DBtier-server1.local"],
    ["label","DBServer"]
  ],
  "type":"ce_revealcloud",                     // type of issue, system or website
  "created_at":1344631403,                     // time of alert & issue creation 
  "updated_at":1344632039,                     // time of most recent update
  "cleared_date":1344632039,                   // time when cleared, or 0
  "notified_date":1344631404,                  // time when notified, or 0
  "ignore_until":1344631408,                   // *** don't know *** 
  "annotation_id":"",                          // associated annotation, if any
  "obj_idv":"ac1f5ef85c1177ef97596f334f877370|" // ignore this field
}
{
  "id":"188",                                  // Unique id for this issue
  "state":"cleared",                           // current state of the issue
  "short_msg":"DBServer: CPU-total (CPU Total Usage 0.945 > 0.9)",
  "attr_description":"Additional Information",  
  "attrs":[                                    // attributes may differ by host
    ["hostname","DBtier-server1.local"],
    ["label","DBServer"]
  ],
  "type":"ce_revealcloud",                     // type of issue, system or website
  "created_at":1344631403,                     // time of alert & issue creation 
  "updated_at":1344632039,                     // time of most recent update
  "cleared_date":1344632039,                   // time when cleared, or 0
  "notified_date":1344631404,                  // time when notified, or 0
  "ignore_until":1344631408,                   // *** don't know *** 
  "annotation_id":"",                          // associated annotation, if any
  "obj_idv":"ac1f5ef85c1177ef97596f334f877370|" // ignore this field
}







{
  "id":"188",                                  // Unique id for this issue
  "state":"cleared",                           // current state of the issue
  "short_msg":"DBServer: CPU-total (CPU Total Usage 0.945 > 0.9)",
  "attr_description":"Additional Information",  
  "attrs":[                                    // attributes may differ by host
    ["hostname","DBtier-server1.local"],
    ["label","DBServer"]
  ],
  "type":"ce_revealcloud",                     // type of issue, system or website
  "created_at":1344631403,                     // time of alert & issue creation 
  "updated_at":1344632039,                     // time of most recent update
  "cleared_date":1344632039,                   // time when cleared, or 0
  "notified_date":1344631404,                  // time when notified, or 0
  "ignore_until":1344631408,                   // *** don't know *** 
  "annotation_id":"",                          // associated annotation, if any
  "obj_idv":"ac1f5ef85c1177ef97596f334f877370|" // ignore this field
}
{% endhighlight %}


Fields that may be updated, and content allowd:
* state .... may set to "cleared" or "deleted";  an other values are not allowed
  
Any other updates to the Issue structure will be quietly ignored.


{
  "id":"502940cafbaa0e9224a3d1f3",
  "state":"cleared",
  "short_msg":"Herkoku-app: Slow Response Time (Response Time 110 ms >= 40.0 ms) ",
  "attr_description":"Additional Information",
  "attrs":[
    ["label","Herkoku-app"],
    ["description","Herkoku-app"],
    ["destination","http://peaceful-lake-1814.herokuapp.com"],
    ["frequency","15"],["type","GET"]
  ],
  "type":"ce_revealuptime",
  "created_at":1344880840,
  "updated_at":1344880853,
  "cleared_date":1344880853,
  "notified_date":1344880842,
  "ignore_until":1344880845,
  "annotation_id":"",
  "obj_idv":"50271cebd9106a2208000004|bjiRJTlKgfnOLq5ecb3jxaA3OmrGGqMt|"
}















{
  "id":188,
  "state":"cleared",
  "short_msg":"fastapi-7c-1: Memory Use - High (Active Memory 0.958 >= 0.95)",
  "attr_description":"Additional Information",
  "attrs":{
    "aws_profile":"default-paravirtual",
    "hostname":"fastapi-7c-1",
    "aws_availability_zone":"us-east-1b",
    "linux_distro":"Ubuntu 12.04 LTS \\n \\l\n",
    "aws_public_hostname":"ec2-174-129-80-99.compute-1.amazonaws.com",
    "aws_reservation_id":"r-fa90679e",
    "aws_inst_type":"c1.xlarge",
    "aws_hostname":"ip-10-42-90-138.ec2.internal",
    "aws_public_ipv4":"174.129.80.99",
    "aws_ami_id":"ami-0674d66f",
    "aws_sec_group":"API Server",
    "aws_local_hostname":"ip-10-42-90-138.ec2.internal",
    "aws_inst_id":"i-941c58ec",
    "aws_mac_addr":"12:31:38:1F:74:7C",
    "aws_local_ipv4":"10.42.90.138",
    "aws_kernel_id":"aki-825ea7eb"
  },
  "type":"ce_revealcloud",
  "created_at":1344521344,
  "updated_at":0,
  "cleared_at":1344527743,
  "notified_at":1344521506,
  "ignore_until":1344521349,
  "annotation_id":"",
  "obj_idv":"d16b38d742a8ada6ccc7b8b33d5eb7dd|"
}


