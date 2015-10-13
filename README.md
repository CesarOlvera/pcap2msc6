The purpose of this project is to add IPv6 support to pcap2msc (http://code.google.com/p/pcap2msc/)

**How do I use it?**

$ pcap2msc6 ipv6_ndp.cap ipv6 | mscgen -T png -o ipv6_ndp.png

Which generates a mscgen formatted text from the CAP file, and then a PNG sequence chart as follow.

The mscgen formatted text:

    msc {
      u0[label=""],u1[label=""],u2[label=""],u3[label=""],u4[label=""];
      u0 rbox u0[label="'::'"],u1 rbox u1[label="'ff02::1:ffa8:2192'"],u2 rbox u2[label="'fe80::a6b1:e9ff:fea8:2192'"],u3 rbox u3[label="'ff02::1'"],u4 rbox u4[label="'fe80::20a:aff:fe00:1'"];
      u0=>u1 [ label = "ICMPv6 78 Neighbor Solicitation for fe80::a6b1:e9ff:fea8:2192" ] ;
      u2=>u3 [ label = "ICMPv6 86 Neighbor Advertisement fe80::a6b1:e9ff:fea8:2192 (rtr, ovr) is at a4:b1:e9:a8:21:92" ] ;
      u2=>u4 [ label = "ICMPv6 86 Neighbor Solicitation for fe80::20a:aff:fe00:1 from a4:b1:e9:a8:21:92" ] ;
      u2<=u4 [ label = "ICMPv6 86 Neighbor Advertisement fe80::20a:aff:fe00:1 (sol, ovr) is at 00:0a:0a:00:00:01" ] ;
    }

And the graph:

![alt tag](https://github.com/CesarOlvera/pcap2msc6/blob/master/ipv6_ndp.png)


**How could be force tshark to decode other protocol?**

tshark options and display filters can be given on command line after the pcap file name. To force to decode other protocol, use

$ pcap2msc6 ipv6_ndp.cap <options> <protocol> | mscgen -T png -o ipv6_ndp.png

**Acknowledgements**

This project is a modification and enhancement of two other projects:

  - pcap2msc (http://code.google.com/p/pcap2msc/) which transforms pcap files into mscgen-compatible file to produce a message sequence chart, but that doesn't parse IPv6.
  - pcap2z120.py (http://www.fi.muni.cz/~xrehak/) which parses IPv6, but doesn't produce a mscgen-compatible file. 

Then, based on pcap2msc there is added the part that parses IPv6 from pcap2z120.py.

Also it has been added:

  - The parse for IPv6 unspecified address (::) as source address.
  - A guard in the case tshark's protocol filter doesn't produce packets.
  - Use round boxes to enclose the IP addresses in the graph. 
