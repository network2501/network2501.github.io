---
title: "Cisco And Redback Link Aggregation"
description: "Configuring a LAG between SEOS and IOS"
tags: [ "cisco", "redback", "link aggregation", "ios", "seos" ]
date: "2014-05-27"
categories:
  - "cisco"
  - "redback"
---
Aggregating links is a normal task of any networker. Here's how you can aggregate 4 links between a Redback SEOS and Cisco IOS device.

![redback to cisco][4]

{{< highlight IOS >}}
config t

interface GigabitEthernet1/1
description Po1 - redback01:1/1
channel-group 1 mode on

interface GigabitEthernet1/2
description Po1 - redback01:1/2
channel-group 1 mode on

interface GigabitEthernet1/3
description Po1 - redback01:1/3
channel-group 1 mode on

interface GigabitEthernet1/4
description Po1 - redback01:1/4
channel-group 1 mode on

interface Port-channel1
description 4Gbps LAG redback01:lg-cisco01
ip address 192.168.1.2 255.255.255.254
end 
{{< /highlight >}}

The Redback configuration is a little bit different which makes more sense when you start to delve into the BNG or mutliple context options.

{{< highlight IOS >}}
port 1/1
 link-group lg-cisco01
 no shut
port 1/2
 link-group lg-cisco01
 no shut
port 1/3
 link-group lg-cisco01
 no shut
port 1/4
 link-group lg-cisco01
 no shut

link-group lg-cisco01
 description lg-cisco01:Po1
 bind interface cisco01 local
 maximum-links 4

interface cisco01
 description 4Gbps LAG cisco01:Po1
 ip address 192.168.1.1/31
{{< /highlight >}}

Trying to visualise the configuration hierarchy. The interface on a Redback ends up being a separate component when using a link-group.

![configuration hierarchy 01][5]

Which method of configuration is better? The Cisco method has less moving parts and is going to be more familiar. The Redback way provides some additional flexibility which can be a double edge sword. If I had to pick, I'd choose the Cisco method but keep in mind there's some pretty cool things you can do with the Redbacks.

[4]: http://blog.network2501.com/images/redback-to-cisco.png
[5]: http://blog.network2501.com/images/configuration-hierarchy-012.png
