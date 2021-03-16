---
title: "Unequal-Cost Multipath in Link State Protocols"
date: 2021-03-23 07:36:00
tags: [ IP routing, OSPF, IS-IS ]
---
Continuing our [exploration of the Unequal-Cost Multipath world](https://blog.ipspace.net/2021/02/does-ucmp-make-sense.html), why was it implemented in EIGRP decades ago, but not in OSPF or IS-IS?

Ignoring for the moment the "*does it make sense*" dilemma: finding *downstream paths* (paths strictly shorter than the current best path) is a side effect of running distance vector algorithms. 

{{<note>}}For a more formal discussion of loop-free alternates and downstream paths, please read [RFC 5714](https://tools.ietf.org/html/rfc5714) and [RFC 5286](https://tools.ietf.org/html/rfc5286).{{</note>}}
<!--more-->
Getting the same results in a link-state protocol requires calculating loop-free alternates, and that was simply too CPU-intensive in ye olde times. We shouldn't have similar problems in the last decades... apart from the minor detail that hardware vendors put the cheapest possible CPU they could get away with on top of the switching silicon to maximize gross margins. 

Anyway, here's what Minh Ha had to say on the topic in a [comment to my previous UCMP blog post](https://blog.ipspace.net/2021/02/does-ucmp-make-sense.html#427):

{{<long-quote>}}
Use-cases aside, I think the bigger question is: is it technically viable to implement UCMP in Link State Protocols? LFA, in its simplest form, is the LS' version of UCMP, and it's computationally intensive when you do it for 1 leaf destination. When you generalize it to calculate UCMP paths to every destination in the network, and the number of nodes gets really huge, into the thousands, this can be computationally intractable. That's why vendors have to take shortcuts, for ex, not implementing TI-LFA for the case of node failure, only link-failure.

The architects of SPB also faced this computational problem earlier on during their design phase. SPB's SPF calculation is way more painful than that of OSPF/ISIS, because instead of doing it once from the perspective of the computing router, a SPB switch has to do all-pair SPF calculations, once for each pair of source-destination in the whole topology. Even though they claim that the all-pair SPFs can be trivially parallelized on multi-core CPUs using B-VIDs as the tree identifiers, I don't believe SPB has ever been tested on real topology of 1000s of nodes. And there's a limit to multi-core, as the inter-core bus contention and the LLC become the dominating bottleneck factor. Finally, SPB is fundamentally incapable of doing UCMP because the requirement of LFA conflicts with SPB's path congruency requirement and RPFC will make sure LFA won't work.

So even if there are situations that require the use of UCMP, one of which brought up by Pete, I don't think it's worth the pain for vendors to come up with a UCMP solution for LS protocols Ivan. This is because Link-state protocols essentially work on a common LSDB of global info, and this centralized model won't scale to very large DB sizes, just like Openflow has tried and failed. Advanced distance vector protocols handle this way more elegantly.

Come to think of it, from the very beginning, in order to scale LS, their inventors had to resort to areas, basically turning LS protocols into distance-vector ones, inter-area-wise. And RIFT, in order to scale better than existing LS protocols in flood-heavy environments, also has to resort to distance-vector principles :)). BGP, the most scalable routing protocol, is a distance-vector protocol after all.
{{</long-quote>}}

Henk Smit quickly provided [hands-on counterargument](https://blog.ipspace.net/2021/02/does-ucmp-make-sense.html#429):

{{<long-quote>}}
It's not that bad. In LS-protocols, doing UCMP scales with the number of direct neighbors a router has. If a router wants to do UCMP, it has to do one SPF-computation for itself, and one SPF-computation for each neighbor. Note, once you know all the feasible (unequal-cost) paths to all routers (nodes) in the network, computing the ip-prefixes (leafs) needs to be done only once.

I remember discussing this in 1996. The first time I read about a vendor implementing UCMP in IS-IS was in 2015. I think IOS-XR can do it (please correct me if I'm wrong). The fact that it took 20 years to implement UCMP makes me suspect that no customer has ever asked for this feature.
{{</long-quote>}}

In any case, Cisco IOS XR documentation claims that:

> Traditionally, EIGRP has been the only IGP that supports UCMP feature, but in IOS-XR UCMP is supported for all IGPs, static routing, and BGP.

**Lesson learned**: while it's much more computationally expensive to get unequal-cost multipathing with link-state routing protocols than it is with distance-vector routing protocols, there's at least one production-grade OSPF/IS-IS UCMP implementation.

### More Details

We started the [Multipath Forwarding](https://my.ipspace.net/bin/list?id=Net101#ADV_ROUTING) discussion in [How Networks Really Work](https://www.ipspace.net/How_Networks_Really_Work) webinar late last year. More to come in the Spring 2021 live session.