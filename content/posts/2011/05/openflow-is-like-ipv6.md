---
url: /2011/05/openflow-is-like-ipv6.html
title: "OpenFlow is like IPv6"
date: "2011-05-10T06:45:00.000+02:00"
tags: [ SDN,OpenFlow ]
---
Frequent eruptions of OpenFlow-related hype (a [recent one](http://community.brocade.com/community/brocadeblogs/wingspan/blog/2011/05/03/being-open-about-virtualization-and-cloud-interoperability) caused by [Brocade Technology Day Summit](http://newsroom.brocade.com/easyir/customrel.do?easyirid=74A6E71C169DEDA9&version=live&prid=750964&releasejsp=custom_184); I’m positive Interop will not lag behind) call for a continuous myth-busting efforts. Let’s start with a [widely-quoted](http://bit.ly/iQW55Y) (and immediately glossed-over) fact from [Professor Scott Shenker](http://www.eecs.berkeley.edu/Faculty/Homepages/shenker.html), a [founding board member](http://www.networkworld.com/news/2011/041411-open-flow.html) of the [ONF](http://www.opennetworkingfoundation.org/): “\[OpenFlow\] doesn't let you do anything you couldn't do on a network before.”

To understand his statement, remember that OpenFlow is nothing more than a standardized version of communication protocol between [control and data plane](/2013/08/management-control-and-data-planes-in.html). It does not define a radically new architecture, it does not solve distributed or virtualized networking challenges and it does not create new APIs that the applications could use. The only thing it provides is the [exchange of TCAM (flow) data between a controller and one or more switches](https://blog.ipspace.net/2011/04/what-is-openflow.html).

Cold fusion-like claims are nothing new in the IT industry. More than a decade ago another group of people tried to persuade us that changing the network layer address length from 32 bits to 128 bits and writing it in hex instead of decimal solves [global routing and multihoming and improves QoS, security and mobility](https://blog.ipspace.net/2010/02/ipv6-myths.html). After the reality distortion field collapsed, we were left with the [same set of problems](https://blog.ipspace.net/2009/05/lack-of-ipv6-multihoming-elephant-in.html) [exacerbated](https://blog.ipspace.net/2011/02/ipv6-provider-independent-addresses.html) by the [purist approach](https://blog.ipspace.net/2010/12/small-site-multihoming-in-ipv6-mission.html) of the original IPv6 architects.

Learn from the past bubble bursts. Whenever someone makes an extraordinary claim about OpenFlow, remember the “it can’t do anything you couldn’t do before” fact and ask yourself:

-   Did we have a similar functionality in the past? If not, why not? Was there no need or were the vendors too lazy to implement it (don't forget they usually follow the money)?
-   Did it work? If not, why not?
-   If it did - do we really need a new technology to replace a working solution?
-   Did it get used? If not, why not? What were the roadblocks? Why would OpenFlow remove them?

Repeat this exercise regularly and you’ll probably discover the new emperor’s clothes aren’t nearly as shiny as some people would make you believe.