---
title: "DPU Hype Considered Harmful"
date: 2022-12-13 07:11:00
tags: [ switching, virtualization ]
---
The hype generated by the "[VMware supports DPU offload](https://www.servethehome.com/amd-pensando-dpu-to-run-vmware-vsphere-and-offload-key-functions/)" announcement already resulted in fascinating misunderstandings. Here's what I got from a System Architect:

> We are dealing with an interesting scenario where a customer had limited data center space, but applications demand more resources. We are evaluating whether we could offload ESXi processing to DPUs (Pensando) to use existing servers as bare-metal servers. Would it be a use case for DPU?

First of all, congratulations to whichever vendor marketer managed to put that guy in that state of mind. Well done, sir, well done. Now for a dose of reality.
<!--more-->
**They might be trying to solve the wrong problem**. Unless their customer's workload is a bunch of ginormous VMs running in a one-VM-per-server environment, or a Kubernetes cluster, one cannot replace ESX hosts with bare-metal servers. In most cases, you still need a mechanism to share a single server's memory and CPU resources across multiple workloads, and you can usually choose between VMs (requiring a hypervisor) or containers.

**You cannot move the ESXi hypervisor to a DPU**. AWS [managed to do that with their Nitro cards](https://docs.aws.amazon.com/whitepapers/latest/security-design-of-aws-nitro-system/the-components-of-the-nitro-system.html), but they had to rewrite a hypervisor from scratch to get there. I would be extremely (pleasantly) surprised if VMware manages to get anywhere close to that in the future -- it's usually impossible to start a clean-slate project in a large company focused on quarterly results and singing the "doing more with less" jingles.

In any case, most of the ESXi hypervisor still runs on the primary server; the only task you can [offload to a DPU in vSphere release 8 is vSphere Distributed Switch](https://docs.vmware.com/en/VMware-vSphere/8.0/vsphere-esxi-installation/GUID-EC3CE886-63A9-4FF0-B79F-111BCB61038F.html)[^LS]. Whether that's a [significant improvement](https://blog.ipspace.net/2022/12/are-dpu-any-good.html) depends on how network-intensive your applications are.

[^LS]: ... and [lose Network IO Control, traffic shaping policies, and security intercept at the NIC level](https://docs.vmware.com/en/VMware-vSphere/8.0/vsphere-networking/GUID-41AB1101-D943-490A-BF1A-E53433855C07.html) (DV filter) while doing that.

Finally, VMware **does not support DPU offload with bare-metal servers** in the initial vSphere 8/NSX 4.0.1 release anyway. The whole idea was a non-starter.

Now for an off-topic thought. This particular instance of hype got me thinking about how far System Architects need to understand the underlying technologies used in their solutions. It's pretty clear one cannot trust vendor marketing or industry press which often does a great job cluelessly rephrasing vendor press releases[^SP]. Depending on the in-house experts would be the obvious solution, but we all know how well that works. Unfortunately, I have no good answer and would appreciate your comments.

[^SP]: We'll ignore sponsored podcasts with technically competent hosts politely avoiding pointed questions for the moment.