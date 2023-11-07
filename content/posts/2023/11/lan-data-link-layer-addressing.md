---
title: "LAN Data Link Layer Addressing"
date: 2023-11-13 07:06:00
draft: True
tags: [ networking fundamentals ]
comment: |
  In early 2020 I created the _[Local Area Network Addressing](https://my.ipspace.net/bin/get/Net101/NA2.2%20-%20Local%20Area%20Network%20Addressing.mp4?doccode=Net101)_ video as part of the _[How Networks Really Work webinar](https://www.ipspace.net/How_Networks_Really_Work)_. This blog post is an edited transcript of the second part of that video.
---
Whenever we talk about LAN data-link-layer addressing, most engineers automatically switch to the "*must be like Ethernet*" mentality, assuming all data-link-layer LAN framing must somehow resemble Ethernet frames.

That makes no sense on point-to-point links. As explained in *[Early Data-Link Layer Addressing](https://blog.ipspace.net/2023/10/data-link-addressing.html)* article, you don't need layer-2 addresses on a point-to-point link between two layer-3 devices. Interestingly, there is one LAN technology (that I'm aware of) that got data link addressing right: [Fibre Channel](https://en.wikipedia.org/wiki/Fibre_Channel) (FC). 
<!--more-->
Fibre Channel[^FCSP] switches are routers. To understand that claim, we have to dive a bit deeper into the [Fibre Channel Protocol](https://en.wikipedia.org/wiki/Fibre_Channel_Protocol) stack because Fibre Channel layers don't line up with the OSI layer we're familiar with:

[^FCSP]: Yes, it is spelt that way to (quoting Wikipedia) "_avoid confusion and to create a unique name._"

-   FC0 is the physical layer. No doubt there.
-   They call FC1 the "transmission protocol." This layer handles encoding, error control, framing, and start/end of frame signaling. FC1 is what we would call the data link layer. 
-   Signaling protocol (FC2) provides end-to-end transport, which we would call the network+transport layer.
-   FC3 provides common services for advanced features, including hunt groups and multicast. FC3 might be the FC equivalent of a session layer.
-   Finally, FC4 is the application layer.

There are only FC2 addresses in the FC. There is no need for FC1 addressing because every FC switch (intermediate node in an FC network) is an FC2 forwarder. It might not be correct to call an FC switch a router or a bridge -- those are IP/Ethernet terms. However, an FC switch forwards packets based on FC2 addresses, and because FC2 is the FC network layer equivalent, we would call it a layer three switch or a router in the IP world.

I had heated discussions with FC gurus who claimed that FC switches were bridges. I read the FC standards, which used "*routing*" to describe FC packet forwarding. So, I don't think you should blame me for the terminology straight out of the FC standards. However, what tripped the FC gurus was the lack of two pairs of source and destination addresses. Their conclusion: "_Obviously, the first address in the payload must be the MAC address._" "_FC must be bridging,_" they said because they've never seen a data link layer with no addresses.   

However, all FC switches are layer three (FC2) switches, and because there are only point-to-point links between a fiber channel node and a fiber channel switch, there is absolutely no need for data link layer addressing.
<!--
On the other hand, there is a technology that got data link layer addressing totally right, which is Ethernet and token ring and FDI and all the other local area or Wi-Fi technologies. When those things started, they were all running on a physical multi-access network. Ethernet started as coax cable that you had to drill into to tap to the wires with a transceiver. Later it became cable with connectors that you put together and build the whole network segment out of pieces of cable. But in both cases, it was one single multi-access network on the physical layer. And they had no master station. They wanted to have a true peer-to-peer network. So any node could send data to any other node. Which means that, A, you need data link addressing because they didn't want to use any higher level protocol. Remember that in the days when Ethernet was created, there were like a dozen network layer protocols. So it wouldn't be good to use any of those. They wanted to use their own addressing. And so we have the destination MAC address and source MAC address in the Ethernet frame. MAC stands for Media Access Control. Protocol or the agreement or standard that allows you to get to the shared media, grab it and transmit data. Now MAC addresses have local significance. They should never be seen outside of a single Ethernet segment. We'll not go into how we stretch Ethernet segments with all sorts of craziness, starting with bridges and then long distance bridging. And finally, bridging over IP with VXLAN or Geneve. The idea was that the MAC addresses have local significance. There were implementations like some IBM implementations where you actually had to enter MAC addresses so they were manually configured. In Ethernet, they had another idea from day one, namely the addresses should be globally administered to simplify deployment. And they split the MAC addresses in the middle. The top part is Organizationally Unique Identifier or OUI and the bottom part is whatever ID. So you have 24 bits that identify the organization. Even today, you can look at any Ethernet frame and Wireshark, for example, would tell you, oh, this is coming from an Intel NIC or this is coming from a Cisco NIC or this is coming from an Arista NIC because all of those manufacturers went to IEEE, they got their own OUI, and then in the manufacturing process, they're assigning unique IDs to individual interface cards they're producing. Interesting side story, some manufacturers were too lazy for that. What they did was they didn't want to pay the OUI assignment fee, so they would put all zeros in there and you would get an interface card that would transmit with MAC addresses of all zeros plus whatever in the ID field. I actually knew someone who got those interface cards and started complaining to the manufacturer and the manufacturer said, well, you know, we get it that you don't like all zeros in there, so just tell us what would you like us to put in there? It's like, no, guys, this is not how Ethernet works. Anyway, as you know, we have multicast and unicast in Ethernet. They solve this by saying, well, if the first bit on the wire, if the first bit that is transmitted by the transmitting station is zero, then it is a unicast frame. So just figure out whether the other 47 bits are yours and if they are, start listening. If the first bit is one, then it's a multicast or a broadcast frame, so everyone should listen and at least figure out whether they should be interested in this. And then second bit on the wire is zero for globally administered addresses and one for locally administered addresses. So you would say, well, what is first or second bit on the wire? Because, you know, if you take a look at a byte, the first or the second bit in a byte should be like this one or this one. If the left-hand bit, the most significant bit on the wire is the first one, then this would be the hex value 80. If the least significant bit is the first one, this would be the hex value one. It turns out that they couldn't agree what to do. This has been dichotomy for the last probably 60 years. There were always manufacturers that thought that most significant bits should come first. This was primarily IBM, but also, for example, Motorola. There were manufacturers who always thought that the least significant bit or the least significant byte in a multibyte digit should come first. Two of these so-called little-endians were Intel and Digital. And guess who created Ethernet? The third one was Xerox. And that's why they originally called this the DIX Ethernet, Digital Internet and Xerox. So on Ethernet, the least significant bit is transmitted first, so multicast addresses always have one in them. They're always odd numbers. Whereas on Token Ring, which was created by IBM, and on FDDI, the most significant bit is transmitted first, which is why you would see multicast addresses in Token Ring or FDDI if you ever managed to see one of those, starting with 80. And the second bit, 02, which is why you would see locally administered addresses like, I don't know whether I've ever seen one outside of DECnet, but in DECnet we would have addresses starting with 02 dot something, because that would be the locally administered address and then there would be some garbage and then there would be cluster ID in here, or the node address. And in Token Ring and FDDI, locally administered address would have value 40 hex, which is why all the Token Ring addresses for IBM mainframes started with 4000. Not that it would matter in 2019, but now you know how things work.
-->