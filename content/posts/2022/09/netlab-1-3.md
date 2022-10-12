---
title: "netlab Release 1.3: VXLAN and EVPN"
series_title: "VXLAN and EVPN (Release 1.3)"
date: 2022-09-05 07:05:00
tags: [ automation ]
series: netlab
netlab_tag: release
---
*netlab* release 1.3 contains two major additions:

* [VXLAN transport](https://netsim-tools.readthedocs.io/en/latest/module/vxlan.html) using static ingress replication or EVPN control plane -- implemented on Arista EOS, Cisco Nexus OS, Dell OS10, Nokia SR Linux and VyOS.
* [EVPN control plane](https://netsim-tools.readthedocs.io/en/latest/module/evpn.html) supporting VXLAN transport, VLAN bridging, VLAN-aware bundles, and symmetric IRB -- implemented on Arista EOS, Dell OS10, Nokia SR Linux, Nokia SR OS (control plane), VyOS, and FRR (control plane).

Here are some of the other goodies included in this release:
<!--more-->
* [MPLS 6PE](https://netsim-tools.readthedocs.io/en/latest/module/mpls.html) implemented on Arista EOS, Cisco IOS, and Cisco IOS XE
* [Default route origination on EBGP sessions](https://netsim-tools.readthedocs.io/en/latest/plugins/ebgp.utils.html)
* [gRPC client installation script](https://netsim-tools.readthedocs.io/en/latest/netlab/install.html)
* VLANs and VRFs on Cisco Nexus OS
* VRFs on Nokia SR Linux
* Complete implementation of VLAN interfaces on Nokia SR Linux
* Statically configured IPv6 hosts on Cisco IOS and Arista EOS

New to *netlab*? Start with the [Getting Started document](https://netsim-tools.readthedocs.io/en/latest/tutorials.html) and the [installation guide](https://netsim-tools.readthedocs.io/en/latest/install.html).