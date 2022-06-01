---
title: Multi-Chassis Link Aggregation
layout: custom
minimal_sidebar: true
deep_dive:
- page: /posts/2022/06/mlag-deep-dive-mac-learning.md
  title: Dynamic MAC Learning
- title: Layer-2 Flooding
- title: ARP Handling
- title: Routing Protocols
- title: Using EVPN as MLAG Control Plane
- title: Replacing Peer-Link with Fabric
- title: Using VXLAN Fabric as MLAG Peer-Link
- title: Load Balancing in VXLAN MLAG Scenarios
---
Multi-Chassis Link Aggregation (MLAG) is a solution that allows you to terminate a link aggregation group (sometimes also known as *etherchannel*) on multiple devices. 

It's often used to implement redundant server connections; it was also popular in the days of layer-2 fabrics built with Spanning Tree Protocol (STP). The latter use case is mostly obsolete in the VXLAN/EVPN world.

### What Is Multi-Chassis Ling Aggregation?

{{<series-listing tag="overview" weight="1">}}

{{<series-listing tag="deepdive" title="Technology Deep Dive" soon="deep_dive">}}

### Design Guidelines

{{<series-listing tag="design">}}

### MLAG Implementations

{{<series-listing tag="implement">}}

### Using MLAG on Server-to-Network Links

{{<series-listing tag="server">}}