---
layout: post
title: "ARM and ARM64 synchronization primitives"
date: 2015-02-28 18:18:35 -0500
comments: true
author: Pranith Kumar
published: false
categories: [Synchronization, ARM, ARM64]

---

Synchronization is used to co-ordinate accesses to shared data from concurrent
threads. It is a neccesity to prevent data races in a parallel program. High level
synchronization primitives include mutexes, locks, semaphores etc.,. These high
level primitives are implemented using atomic read-modify-write instructions
provided by most processors. x86 processors provide instructions like cmpxchg
and xchg to implement these primitives. In the current article we look at the
synchronization instructions provided by ARM and ARM64 processors and how to use
them in implementing high level synchronization primitives. We take a lot of help
from studying the current implementation in the Linux Kernel.

The synchronization instructions in ARM/ARM64 architecture are tabulated
below. 


 Instruction | starting from ARM arch. | function                     | alternatives              
-------------|:-----------------------:|------------------------------|---------------------------
 swp         | v5                      | swap values                  | swpb                      
 ldrex       | v6                      | load value exclusively       | ldrexb, ldrexh (v6k)      
 strex       | v6                      | store value exclusively      | strexb, strexh (v6k)      
 ldraex      | v8                      | load exclusive with acquire  | ldraexb, ldraexh, ldraexd 
 strlex      | v8                      | store exclusive with release | strlexb, strlexh, strlexd 



Alternatives are versions of the same instructions which work on
different word sizes. Suffix b stands for byte, h for half word and d for
double word.


References:

[1] http://infocenter.arm.com/help/index.jsp?topic=/com.arm.doc.dht0008a/ch01s02s01.html
