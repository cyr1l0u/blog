---
title: "BGP Labs: The Basics"
date: 2023-08-24 06:40:00
tags: [ BGP, netlab ]
series: [ bgp_labs ]
netlab_tag: edu
---
The first [BGP labs](/2023/08/bgp-hands-on-labs.html) are online. They cover the basic stuff (one has to [start with the basics](https://blog.ipspace.net/2015/03/you-must-understand-fundamentals-to-be.html), right?):

* [Configuring an EBGP session](https://ipspace.github.io/bgplab/basic/1-session/)
* [Connecting to multiple upstream ISPs](https://ipspace.github.io/bgplab/basic/2-multihomed/)
* [Advertise your prefixes](https://ipspace.github.io/bgplab/basic/3-originate/)
* [Configure BGP for IPv6](https://ipspace.github.io/bgplab/basic/4-ipv6/)

The labs are supposed to be run on virtual devices, but if you're stubborn enough it's possible to make them [work with the physical gear](https://ipspace.github.io/bgplab/external/). In theory, you could use any system you like to set up the virtual lab (including GNS3 and CML/VIRL), but your life will be way easier if you use [netlab](https://netlab.tools/) -- it [supports BGP on almost 20 different devices](https://netlab.tools/platforms/#platform-routing-support). For more details, read the [Installation and Setup](https://ipspace.github.io/bgplab/1-setup/) documentation.