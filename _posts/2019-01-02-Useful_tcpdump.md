---
layout: single
title: "Useful: tcpdump"
date: 2019-01-02
tags: 
 - networking 
---

You may want to check Daniel's [tcpdump Examples — 50 Ways to Isolate Specific Traffic](https://danielmiessler.com/study/tcpdump/). You probably don't need much more to do what you're trying to do with tcpdump. 

## The safety nets: -n & -c 

I use the following two options on 99% on my packet captures: -n and -c <number>. 

-n prevents IP addresses from being resolved into hostname, which is good for OpSec and very good for performance. Older versions of tcpdump differentiated resoling IP addresses and ports, requiring -nn .<br />
-c <number> will stop the capture after <number> of packets captured. 

* Example: Capture 100 packets from interface eno1 and do not reslove IP addresses:
{% highlight sh %}
> sudo tcpdump -n -c 100 -i eno1
{% endhighlight %}

## Netflow 
I look at <strong>A LOT</strong> of netflow data on a daily basis. It is occasionally required to decode netflow records at the command line:
* Decoding Netflow:
{% highlight sh %}
> sudo tcpdump -n -c 100 -i eno1 udp port <port> -T cnfp
{% endhighlight %}

