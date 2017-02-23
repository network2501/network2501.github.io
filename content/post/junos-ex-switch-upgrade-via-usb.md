---
title: "Junos EX Switch Upgrade via USB"
description: "Step by step USB upgrade for an EX series switch"
tags: [ "junos", "upgrade", "howto", "EX2200c", "juniper" ]
date: "2013-06-21"
categories:
    - "juniper"
---

I have a Juniper EX2200c switch that needs upgrading. So here goes the quick and dirty run down.

Jump into the shell.

{{< highlight Junos >}}
root> start shell
{{< /highlight >}}

Make a folder to mount your FAT16/32 USB drive, then mount it.

{{< highlight Junos >}}
root> start shell
root@:RE:0% mkdir /var/tmp/usb 
root@:RE:0% mount -t msdosfs /dev/da1s1 /var/tmp/usb
{{< /highlight >}}

Jump back to the CLI and install your new Junos.

{{< highlight Junos >}}
root> start shell
root@:RE:0% cli {master:0} root> request system software add /var/tmp/usb/jinstall-ex-2200-12.3R3.4-domestic-signed.tgz validate reboot
{{< /highlight >}}

If you're not upgrading from a version prior to 10.4R2 that's all there is to it. However a boot loader upgrade is required for EX devices when upgrading from Junos version 10.4R2 or earlier.

![ex2200c][3]

[1]: http://blog.network2501.com/2013/06/21/junos-ex-switch-upgrade-via-usb/#disqus_thread
[2]: http://blog.network2501.com/categories/juniper
[3]: http://blog.network2501.com/images/ex2200c.jpg

