---
layout: single
title: Building a BPF/XDP coding environment
tags:
  - eBPF
  - XDP
  - C
---

The following is a reliable way to create an eBPF/XDP environemnt which works outside of the coding tree. 

This used to be a pain in the neck to setup but the XDP Project has managed to make it easy and accessible.

In a brand spanking new Debian Bookworm basic install, run the following commands as root.

```shell
apt install git build-essential linux-headers-amd64 pkg-config clang llvm \
        bpftool libmnl-dev m4 libpcap-dev libc6-dev-i386 libcap-dev \
        linux-perf ethtool
git clone https://github.com/xdp-project/xdp-tutorial.git 
cd xdp-tutorial
git submodule update --init
cd basic01-xdp-pass
make
```

I use VirtualBox for build VMs and by default it uses the "Intel PRO/1000 MT Destop" NIC driver. Unfortunately, this driver only supports XDP generic mode. I change the NIC driver to "Paravirtualized Network", in order to ensure XDP works in native mode.

To check that everything as worked as expected run the compiled program as root:

```shell
> ./xdp_pass_user -d enp78s0
Success: Loading XDP prog name:xdp_prog_simple(id:51) on device:enp78s0(ifindex:2)
>
```

And then double check with bpftool:
```shell
> bpftool net show 
xdp:
enp78s0(2) generic id 51

tc:

flow_dissector:
> bpftool prog dump xlated id 51
int xdp_prog_simple(struct xdp_md * ctx):
; return XDP_PASS;
   0: (b7) r0 = 2
   1: (95) exit
>
```

All done and working.

Sources:
  - [XPD Project](https://xdp-project.net/)
  - [XDP Project Github repositories](https://github.com/xdp-project)


