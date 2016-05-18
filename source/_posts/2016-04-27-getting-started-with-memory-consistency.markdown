---
layout: post
title: "Getting started with memory consistency"
date: 2016-04-27 23:39:08 -0400
comments: true
published: true
categories: memory consistency, fences, barriers
---

When I initially started learning about memory consistency, I found it full of
intricacies and it was pretty involved. There are quite a few resources which
helped me get up to speed. These are the ones I refer to whenever I am
confused about anything related to consistency. I am listing them here and I
hope you find it equally useful.

The first document I would recommend would be
["Memory Barriers: a Hardware View for Software Hackers"](http://www2.rdrop.com/~paulmck/scalability/paper/whymb.2010.07.23a.pdf)
by [Paul McKenney](http://paulmck.livejournal.com/). This is a lucid
introduction describing some of the hardware structures which cause
consistency issues to arise. It mainly boils down to optimizations implemented
in hardware to reduce the cost of memory accesses being the cause.

Next would be to read [Jeff Preshing'](http://preshing.com/about) blog which
has quite some articles for those interested in parallel programming. I would
recommend these three articles in particular:
[1](http://preshing.com/20130922/acquire-and-release-fences/),
[2](http://preshing.com/20131125/acquire-and-release-fences-dont-work-the-way-youd-expect/),
[3](http://preshing.com/20130618/atomic-vs-non-atomic-operations/).

Once you get a basic understanding of consistency and fences, the next article
would be the Linux kernel's [memory-barriers.txt](
https://github.com/torvalds/linux/blob/master/Documentation/memory-barriers.txt). This
document goes into quite some depth explaining the various ordering
dependencies which arise in current processors and how to use memory barriers
to ensure consistency. You should also see the barrier.h header file for
different architectures.

You should also read
["A Tutorial Introduction to the ARM and POWER Relaxed Memory Models"](http://www.cl.cam.ac.uk/~pes20/ppc-supplemental/test7.pdf). As
the title says it talks about the ARM and POWER memory models. Another
tutorial worth reading is
["Shared Memory Consistency Models: A Tutorial"](http://cs.nyu.edu/~lerner/spring10/MCP-S10-Read06-ConsistencyTutorial.pdf).

I will keep updating this post with any new articles I find interesting. Hope
you enjoy them!
