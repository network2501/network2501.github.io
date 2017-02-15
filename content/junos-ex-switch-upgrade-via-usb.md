[Source](http://blog.network2501.com/2013/06/21/junos-ex-switch-upgrade-via-usb/ "Permalink to Junos EX Switch Upgrade via USB")

# Junos EX Switch Upgrade via USB

Jun 21, 2013 · [Comments][1] [juniper][2]

I have a Juniper EX2200c switch that needs upgrading. So here goes the quick and dirty run down.

Jump into the shell.
    
    
    root> start shell
    

Make a folder to mount your FAT16/32 USB drive, then mount it.
    
    
    root@:RE:0% mkdir /var/tmp/usb 
    root@:RE:0% mount -t msdosfs /dev/da1s1 /var/tmp/usb
    

Jump back to the CLI and install your new Junos.
    
    
    root@:RE:0% cli {master:0} root> request system software add /var/tmp/usb/jinstall-ex-2200-12.3R3.4-domestic-signed.tgz validate reboot
    

If you're not upgrading from a version prior to 10.4R2 that's all there is to it. However a boot loader upgrade is required for EX devices when upgrading from Junos version 10.4R2 or earlier.

![ex2200c][3]

[1]: http://blog.network2501.com/2013/06/21/junos-ex-switch-upgrade-via-usb/#disqus_thread
[2]: http://blog.network2501.com/categories/juniper
[3]: http://blog.network2501.com/images/ex2200c.jpg

