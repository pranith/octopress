---
layout: post
title: "QEMU 2.7 Statistics"
date: 2016-09-13 20:26:48 -0400
comments: true
categories: qemu, statistics
published: true
---

I had a great time hacking on QEMU over the summer as part of Google Summer of
Code. If you are interested in the details, my mentor, Alex Bennée, has
written an excellent summary of the project on
[lwn.net](<http://lwn.net/Articles/697265/>).  While I eagerly wait for my
patches to be merged upstream, I decided to analyze some statistics in the
most recent release of QEMU, version 2.7. This analysis is done using the
[gitdm](<https://github.com/pranith/gitdm>) tool written by Jonathan Corbet for
analyzing the Linux Kernel releases. The current analysis is neither as
thorough nor as accurate as the analysis done for Linux. It is just an amateur
attempt at understanding the developer world of QEMU.

QEMU has quite many similarities with the linux kernel, which I guess is
because of an overlap of developers among the two projects. Both the projects
are mainly written in C and use the dreaded checkpatch script in their patch
submission workflow. The technical discussions happen on the mailing list
(i.e., posting patches, reviews etc.,) although quite a few QEMU developers
often hangout on [IRC](<//irc.oftc.net/qemu>) for discussions and to help
out users facing problems with QEMU.

With that background information, let us look at the version 2.7 release of
QEMU. The releases in QEMU are tagged by Peter Maydell who also merges in the
changesets from the pull requests posted by various subsystem maintainers. In
the 2.7 release there were a total of 2292 non-merge commits in the tree, as
compared to 2427 commits in the 2.6 release. Individual developers with the
most commits are listed below.

**QEMU Developers in 2.7 release**

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="left" />

<col  class="right" />

<col  class="right" />
</colgroup>
<thead>
<tr>
<th scope="col" class="left">Name</th>
<th scope="col" class="right">Number of Commits</th>
<th scope="col" class="right">Percentage</th>
</tr>
</thead>

<tbody>
<tr>
<td class="left">Eric Blake</td>
<td class="right">169</td>
<td class="right">7.4%</td>
</tr>


<tr>
<td class="left">Peter Maydell</td>
<td class="right">156</td>
<td class="right">6.8%</td>
</tr>


<tr>
<td class="left">Paolo Bonzini</td>
<td class="right">155</td>
<td class="right">6.8%</td>
</tr>


<tr>
<td class="left">Kevin Wolf</td>
<td class="right">118</td>
<td class="right">5.1%</td>
</tr>


<tr>
<td class="left">Daniel P. Berrange</td>
<td class="right">102</td>
<td class="right">4.5%</td>
</tr>


<tr>
<td class="left">Igor Mammedov</td>
<td class="right">77</td>
<td class="right">3.4%</td>
</tr>


<tr>
<td class="left">Marc-André Lureau</td>
<td class="right">71</td>
<td class="right">3.1%</td>
</tr>


<tr>
<td class="left">Xiaoqiang Zhao</td>
<td class="right">55</td>
<td class="right">2.4%</td>
</tr>


<tr>
<td class="left">Eduardo Habkost</td>
<td class="right">54</td>
<td class="right">2.4%</td>
</tr>


<tr>
<td class="left">Fam Zheng</td>
<td class="right">53</td>
<td class="right">2.3%</td>
</tr>
</tbody>
</table>

From what I could gather, Eric Blake works mostly in the block layer with
quite a few commits in the nbd, replay and qapi subsystems. Peter Maydell has
contributions all over the tree with his main contributions being to user mode
emulation and the ARM subsystems. Paolo Bonzini too has contributions all over
the tree with most of them related to all TCG targets (arm and i386 in
particular), nbd and general QEMU execution infrastructure.

**Top changeset contributors by employer**

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="left" />

<col  class="right" />

<col  class="right" />
</colgroup>
<thead>
<tr>
<th scope="col" class="left">Company</th>
<th scope="col" class="right">Number of Commits</th>
<th scope="col" class="right">Percentage</th>
</tr>
</thead>

<tbody>
<tr>
<td class="left">Red Hat</td>
<td class="right">1225</td>
<td class="right">53.4%</td>
</tr>


<tr>
<td class="left">(Unknown)</td>
<td class="right">503</td>
<td class="right">21.9%</td>
</tr>


<tr>
<td class="left">Linaro</td>
<td class="right">214</td>
<td class="right">9.3%</td>
</tr>


<tr>
<td class="left">IBM</td>
<td class="right">111</td>
<td class="right">4.8%</td>
</tr>


<tr>
<td class="left">Fujitsu</td>
<td class="right">65</td>
<td class="right">2.8%</td>
</tr>


<tr>
<td class="left">Intel</td>
<td class="right">35</td>
<td class="right">1.5%</td>
</tr>


<tr>
<td class="left">Parallels</td>
<td class="right">30</td>
<td class="right">1.3%</td>
</tr>


<tr>
<td class="left">Xilinx</td>
<td class="right">23</td>
<td class="right">1.0%</td>
</tr>


<tr>
<td class="left">Bull</td>
<td class="right">20</td>
<td class="right">0.9%</td>
</tr>


<tr>
<td class="left">Novell</td>
<td class="right">18</td>
<td class="right">0.8%</td>
</tr>
</tbody>
</table>

I counted about 21 companies (I am sure there are more) which sponsor QEMU
development.  The major ones among these are Red Hat, Linaro and IBM.  I think
the main reason for the overwhelming showing by Red Hat is mainly because of
their involvement in KVM, which is their virtualization tool of choice. The
unknown row is supposed to be contributions from individuals with no
affiliation, but I think the case here that of missing information. Many
developers use their personal non-affiliated email id in the commit messages,
which makes it difficult to identify the company employing them.

Having said that, let us look at who is employing the hackers working on QEMU.

**Employers with the most hackers (total 189)**

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="left" />

<col  class="right" />

<col  class="right" />
</colgroup>
<thead>
<tr>
<th scope="col" class="left">Company</th>
<th scope="col" class="right">Number of Employees</th>
<th scope="col" class="right">Percentage</th>
</tr>
</thead>

<tbody>
<tr>
<td class="left">(Unknown)</td>
<td class="right">83</td>
<td class="right">43.9%</td>
</tr>


<tr>
<td class="left">Red Hat</td>
<td class="right">39</td>
<td class="right">20.6%</td>
</tr>


<tr>
<td class="left">IBM</td>
<td class="right">19</td>
<td class="right">10.1%</td>
</tr>


<tr>
<td class="left">Fujitsu</td>
<td class="right">9</td>
<td class="right">4.8%</td>
</tr>


<tr>
<td class="left">Intel</td>
<td class="right">7</td>
<td class="right">3.7%</td>
</tr>


<tr>
<td class="left">Linaro</td>
<td class="right">6</td>
<td class="right">3.2%</td>
</tr>


<tr>
<td class="left">Novell</td>
<td class="right">6</td>
<td class="right">3.2%</td>
</tr>


<tr>
<td class="left">Xilinx</td>
<td class="right">3</td>
<td class="right">1.6%</td>
</tr>


<tr>
<td class="left">Huawei</td>
<td class="right">3</td>
<td class="right">1.6%</td>
</tr>


<tr>
<td class="left">Citrix</td>
<td class="right">3</td>
<td class="right">1.6%</td>
</tr>
</tbody>
</table>

Most of the developers working on QEMU are not properly attributed as working
for a company. So the unknown tag shows up at the top. Red Hat is the most
known employer funding twenty percent of the known QEMU developers.

**Employers with the most signoffs (total 1851)**

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="left" />

<col  class="right" />

<col  class="right" />
</colgroup>
<thead>
<tr>
<th scope="col" class="left">Company</th>
<th scope="col" class="right">Number of Commits</th>
<th scope="col" class="right">Percentage</th>
</tr>
</thead>

<tbody>
<tr>
<td class="left">Red Hat</td>
<td class="right">1036</td>
<td class="right">56.0%</td>
</tr>


<tr>
<td class="left">Linaro</td>
<td class="right">362</td>
<td class="right">19.6%</td>
</tr>


<tr>
<td class="left">(Unknown)</td>
<td class="right">278</td>
<td class="right">15.0%</td>
</tr>


<tr>
<td class="left">IBM</td>
<td class="right">65</td>
<td class="right">3.5%</td>
</tr>


<tr>
<td class="left">Telecom-Service</td>
<td class="right">58</td>
<td class="right">3.1%</td>
</tr>


<tr>
<td class="left">Fujitsu</td>
<td class="right">16</td>
<td class="right">0.9%</td>
</tr>


<tr>
<td class="left">Parallels</td>
<td class="right">14</td>
<td class="right">0.8%</td>
</tr>


<tr>
<td class="left">Xilinx</td>
<td class="right">11</td>
<td class="right">0.6%</td>
</tr>


<tr>
<td class="left">Huawei</td>
<td class="right">7</td>
<td class="right">0.4%</td>
</tr>


<tr>
<td class="left">Intel</td>
<td class="right">2</td>
<td class="right">0.1%</td>
</tr>
</tbody>
</table>

And the 20% developers funded by Red Hat contributed more than half of the
commits that went into the 2.7 QEMU release.

As I mentioned earlier, the information here is not accurate. If you want to
correct or contribute to such analysis, please comment, send an email or a
pull request in the [gitdm-qemu](<https://github.com/pranith/gitdm-qemu>)
repository. This repo has the configuration scripts I used to generate the
above information. Hopefully I will get more accurate for the 2.8 release.

All the stats generated by gitdm can be found in
[this](http://pranith.org/stats-qemu-2.7.html) file.
