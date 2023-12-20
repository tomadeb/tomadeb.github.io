---
layout: single
title: Building Linux BPF samples on Debian Bookworm
tags:
  - eBPF
  - XDP
  - C
---

Here is how to build the sample BPF programs included in the linux kernel. 

```shell
apt install linux-source binutils-dev libreadline6-dev
cd
tar xaf /usr/src/linux-source-6.1.tar.xz
cd linux-source-6.1
cp /boot/config-6.1.0-6-amd64 .config
make tools
make headers_install
cd tools/bpf 
make 
cd ../..
make asm-generic
make VMLINUX_BTF=/sys/kernel/btf/vmlinux M=samples/bpf
```
