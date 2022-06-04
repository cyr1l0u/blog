---
title: "netsim-tools VLAN Trunk Example"
date: 2022-06-06 06:12:00
tags: [ automation ]
series: netsim
netsim_tag: vlan_vrf
series_title: VLAN Trunk Example
---
Last week I described [how easy it is to use access VLANs](https://blog.ipspace.net/2022/05/netsim-vlan-simple.html) in *netsim-tools*. Next step: VLAN trunks. 

{{<note info>}}[VLAN trunks](https://netsim-tools.readthedocs.io/en/latest/module/vlan.html) are supported from [*netsim-tools* release 1.2.2](https://netsim-tools.readthedocs.io/en/latest/release/1.2.html) and are [currently implemented](https://netsim-tools.readthedocs.io/en/latest/module/vlan.html#platform-support) on Arista EOS, Cisco IOSv, VyOS, Dell OS10 and Nokia SR Linux.{{</note>}}

We'll add two Linux hosts to the lab topology used in the previous blog post, resulting in two switches, two Linux hosts in *red* VLAN and two Linux hosts in *blue* VLAN.
<!--more-->
{{<figure src="/2022/06/vlan-trunk.png" caption="Lab topology">}}

Like in the previous example, we'll use *[groups](/2021/11/netsim-groups-deployment-templates.html)* in the [lab topology file](https://github.com/ipspace/netsim-examples/blob/master/VLAN/vlan-trunk/topology.yml) to define our devices. Members of the *hosts* group will be Linux containers, members of the *switches* group will be Arista EOS containers using *vlan* configuration module:

{{<cc>}}Defining nodes and groups{{</cc>}}
```
provider: clab

nodes: [ h1, h2, h3, h4 s1, s2 ]

groups:
  hosts:
    members: [ h1, h2, h3, h4 ]
    device: linux
  switches:
    members: [ s1, s2 ]
    module: [ vlan ]
    device: eos
```

Next, we'll define the VLANs. We need *red* and *blue* VLANs; as before, *netsim-tools* will assign 802.1q tags to VLANs as needed.

{{<cc>}}Defining VLANs{{</cc>}}
```
vlans:
  red:
  blue:
```

Finally, we need links between nodes. Access VLANs with be defined on switch interfaces. List of VLANs in the VLAN trunk will be defined on the link itself, as it applies to all nodes connected to the trunk. Note that we're working with VLAN names and don't have to worry about the VLAN 802.1q tags.

{{<cc>}}Defining links{{</cc>}}
```
links:
- h1:
  s1:
    vlan.access: red
- h3:
  s1:
    vlan.access: blue
- s1:
  s2:
  vlan.trunk: [ red, blue ]
- h2:
  s2:
    vlan.access: red
- h4:
  s2:
    vlan.access: blue
```

And that's all you have to do. Execute **netlab up**[^HW] and enjoy your first multi-VLAN lab.

[^HW]: After doing the mandatory homework like [creating a Ubuntu VM](https://netsim-tools.readthedocs.io/en/latest/install/ubuntu-vm.html), [installing the software](https://netsim-tools.readthedocs.io/en/latest/labs/clab.html), and [downloading Arista cEOS container](https://netsim-tools.readthedocs.io/en/latest/labs/ceos.html).

Here are the relevant parts of Arista cEOS configuration (for the two readers who still don't have a working *netsim-tools* environment):

{{<cc>}}Arista cEOS multi-VLAN configuration{{</cc>}}
```
spanning-tree mode mstp
!
vlan 1000
   name red
!
vlan 1001
   name blue
!
interface Ethernet1
   mac-address 52:dc:ca:fe:05:01
   switchport access vlan 1000
!
interface Ethernet2
   mac-address 52:dc:ca:fe:05:02
   switchport access vlan 1001
!
interface Ethernet3
   description s1 -> s2
   mac-address 52:dc:ca:fe:05:03
   switchport trunk allowed vlan 1000-1001
   switchport mode trunk
!
interface Vlan1000
   description VLAN red (1000) -> [h1,s2,h2]
   ip address 172.16.0.5/24
!
interface Vlan1001
   description VLAN blue (1001) -> [h3,s2,h4]
   ip address 172.16.1.5/24
```

Want to run this lab on your own, or [try it out with different devices](https://github.com/ipspace/netsim-examples/tree/master/VLAN/vlan-trunk#changing-device-types)? No problem:

* [Install netsim-tools](https://netsim-tools.readthedocs.io/en/latest/install.html)
* [Download the relevant containers](https://netsim-tools.readthedocs.io/en/latest/labs/clab.html) or [create Vagrant boxes](https://netsim-tools.readthedocs.io/en/latest/labs/libvirt.html)
* Download the [topology file](https://github.com/ipspace/netsim-examples/blob/master/VLAN/vlan-trunk/topology.yml) into an empty directory
* Execute **netlab up**
* Enjoy! 😊