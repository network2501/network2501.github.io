RX as a router

Mar 17, 2014 · [Comments][1] [juniper][2]

The SRX is a stateful firewall but I want to use the vSRX as a router for study. I intend to configure IPv6, MPLS and ISIS so a few changes need to be made.
    
    
    set security forwarding-options family inet6 mode packet-based
    set security forwarding-options family mpls mode packet-based
    set security forwarding-options family iso mode packet-based
    

If the above wasn't configured even with all the security configuration remove the stateful process of the firewall would drop traffic. Now that it's set I can ping between interfaces just fine to confirm connectivity.
    
    
    root@lab-srx00> ping 10.0.0.2 
    PING 10.0.0.2 (10.0.0.2): 56 data bytes 64 bytes 
    from 10.0.0.2: icmp_seq=0 ttl=64 time=8.971 ms 64 bytes 
    from 10.0.0.2: icmp_seq=1 ttl=64 time=2.076 ms 64 bytes 
    from 10.0.0.2: icmp_seq=2 ttl=64 time=2.528 ms 64 bytes
    

[1]: http://blog.network2501.com/2014/03/17/vsrx-as-a-router/#disqus_thread
[2]: http://blog.network2501.com/categories/juniper

