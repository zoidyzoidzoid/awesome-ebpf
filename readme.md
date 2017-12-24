# Awesome EBPF [![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome)

> A curated list of awesome projects related to eBPF

Thank you to Quentin Monnet and Daniel Borkmann for their original work on [Dive into BPF: A List of Reading Material](https://qmonnet.github.io/whirl-offload/2016/09/01/dive-into-bpf/) which became the basis for this list.

## Contents

- [What is BPF?](#what-is-bpf)
- [Resources](#resources)
- [Documentation](#documentation)
- [Tutorials](#tutorials)
- [Examples](#examples)
- [The Code](#the-code)
- [Troubleshooting](#troubleshooting)
- [Playing With BPF and XDP](#playing-with-bpf-and-xdp)
- [BPF Development](#bpf-development)
- [Contributing To This List](#contribute)
- [License](#license)

## What is BPF?

TODO: Update with concise overview of BPF (cBPF and eBPF), and what it's
used for already.

## Resources

### Generic presentations

The documents linked below provide a generic overview of BPF, or of some
closely related topics. If you are very new to BPF, you can try picking a
couple of presentation among the first ones and reading the ones you like most.
If you know eBPF already, you probably want to target specific topics instead,
lower down in the list.

### Generic Presentations About eBPF

* [_Making the Kernel’s Networking Data Path Programmable with BPF and XDP_](http://schd.ws/hosted_files/ossna2017/da/BPFandXDP.pdf)
  (Daniel Borkmann, OSSNA17, Los Angeles, September 2017):<br />
  One of the best set of slides available to understand quickly all the basics about eBPF and XDP (mostly for network processing).

* [The BSD Packet Filter](https://speakerdeck.com/tuxology/the-bsd-packet-filter)
  (Suchakra Sharma, June 2017): <br />
  A very nice introduction, mostly about the tracing aspects.

* [_BPF: tracing and more_](http://www.slideshare.net/brendangregg/bpf-tracing-and-more)
  (Brendan Gregg, January 2017):<br />
  Mostly about the tracing use cases.

* [_Linux BPF Superpowers_](http://fr.slideshare.net/brendangregg/linux-bpf-superpowers)
  (Brendan Gregg, March 2016):<br />
  With a first part on the use of **flame graphs**.

* [_IO Visor_](https://www.socallinuxexpo.org/sites/default/files/presentations/Room%20211%20-%20IOVisor%20-%20SCaLE%2014x.pdf)
  (Brenden Blanco, SCaLE 14x, January 2016):<br />
  Also introduces **IO Visor project**.

* [_eBPF on the Mainframe_](https://events.linuxfoundation.org/sites/events/files/slides/ebpf_on_the_mainframe_lcon_2015.pdf)
  (Michael Holzheu, LinuxCon, Dubin, October 2015)

* [_New (and Exciting!) Developments in Linux Tracing_](https://events.linuxfoundation.org/sites/events/files/slides/tracing-linux-ezannoni-linuxcon-ja-2015_0.pdf)
  (Elena Zannoni, LinuxCon, Japan, 2015)

* [_BPF — in-kernel virtual machine_](https://events.linuxfoundation.org/sites/events/files/slides/bpf_collabsummit_2015feb20.pdf)
  (Alexei Starovoitov, February 2015):<br />
  Presentation by the author of eBPF.

* [_Extending extended BPF_](https://lwn.net/Articles/603983/)
  (Jonathan Corbet, July 2014)

### BPF internals

* Daniel Borkmann has been doing an amazing work to present **the internals** of eBPF, in particular about **its use with tc**, through several talks and papers.
    * [*Advanced programmability and recent updates with tc's cls_bpf*](http://netdevconf.org/1.2/session.html?daniel-borkmann)
      (netdev 1.2, Tokyo, October 2016):<br />
      Daniel provides details on eBPF, its use for tunneling and encapsulation,
      direct packet access, and other features.
    * [*cls_bpf/eBPF updates since netdev 1.1*](http://netdevconf.org/1.2/slides/oct5/07_tcws_daniel_borkmann_2016_tcws.pdf)
      (netdev 1.2, Tokyo, October 2016, part of
      [this tc workshop](http://netdevconf.org/1.2/session.html?jamal-tc-workshop))
    * [*On getting tc classifier fully programmable with cls_bpf*](http://www.netdevconf.org/1.1/proceedings/slides/borkmann-tc-classifier-cls-bpf.pdf)
      (netdev 1.1, Sevilla, February 2016):<br />
      After introducing eBPF, this presentation provides insights on many
      internal BPF mechanisms (map management, tail calls, verifier). A
      must-read! For the most ambitious,
      [the full paper is available here](http://www.netdevconf.org/1.1/proceedings/papers/On-getting-tc-classifier-fully-programmable-with-cls-bpf.pdf).
    * [_Linux tc and eBPF_](https://archive.fosdem.org/2016/schedule/event/ebpf/attachments/slides/1159/export/events/attachments/ebpf/slides/1159/ebpf.pdf)
      (fosdem16, Brussels, Belgium, January 2016)
    * [_eBPF and XDP walkthrough and recent updates_](https://fosdem.org/2017/schedule/event/ebpf_xdp/)
      (fosdem17, Brussels, Belgium, February 2017)

  These presentations are probably one of the best sources of documentation to
  understand the design and implementation of internal mechanisms of eBPF.

The [**IO Visor blog**](https://www.iovisor.org/resources/blog) has some
interesting technical articles about BPF. Some of them contain a bit of
marketing talks.

### Kernel tracing

* [_Meet-cute between eBPF and Kerne Tracing_](http://www.slideshare.net/vh21/meet-cutebetweenebpfandtracing)
  (Viller Hsiao, July 2016):<br />
  Kprobes, uprobes, ftrace

* [_Linux Kernel Tracing_](http://www.slideshare.net/vh21/linux-kernel-tracing)
  (Viller Hsiao, July 2016):<br />
  Systemtap, Kernelshark, trace-cmd, LTTng, perf-tool, ftrace, hist-trigger,
  perf, function tracer, tracepoint, kprobe/uprobe…

Regarding **event tracing and monitoring**, Brendan Gregg uses eBPF a lot and
does an excellent job at documenting some of his use cases. If you are in
kernel tracing, you should see his blog articles related to eBPF and flame
graphs. Most of it are accessible
[from this article](http://www.brendangregg.com/blog/2016-03-05/linux-bpf-superpowers.html)
or by browsing his blog.

Introducing BPF, but also presenting **generic concepts of Linux networking**:

* [_Linux Networking Explained_](http://www.slideshare.net/ThomasGraf5/linux-networking-explained)
  (Thomas Graf, LinuxCon, Toronto, August 2016)

* [_Kernel Networking Walkthrough_](http://www.slideshare.net/ThomasGraf5/linuxcon-2015-linux-kernel-networking-walkthrough)
  (Thomas Graf, LinuxCon, Seattle, August 2015)

### Hardware offload

* eBPF with tc or XDP supports hardware offload, starting with Linux kernel
  version 4.9 and introduced by Netronome. Here is a presentation about this
  feature:<br />
  [eBPF/XDP hardware offload to SmartNICs](http://netdevconf.org/1.2/session.html?jakub-kicinski)
  (Jakub Kicinski and Nic Viljoen, netdev 1.2, Tokyo, October 2016)

### About cBPF

* [_The BSD Packet Filter: A New Architecture for User-level Packet Capture_](http://www.tcpdump.org/papers/bpf-usenix93.pdf)
  (Steven McCanne and Van Jacobson, 1992):<br />
  The original paper about (classic) BPF.

* [The FreeBSD manual page about BPF](http://www.gsp.com/cgi-bin/man.cgi?topic=bpf)
  is a useful resource to understand cBPF programs.

* Daniel Borkmann realized at least two presentations on cBPF,
  [one in 2013 on mmap, BPF and Netsniff-NG](http://borkmann.ch/talks/2013_devconf.pdf), and
  [a very complete one in 2014 on tc and cls\_bpf](http://borkmann.ch/talks/2014_devconf.pdf).

* On Cloudflare's blog, Marek Majkowski presented his
  [use of BPF bytecode with the `xt_bpf` module for **iptables**](https://blog.cloudflare.com/introducing-the-bpf-tools/).
  It is worth mentioning that eBPF is also supported by this module, starting
  with Linux kernel 4.10 (I do not know of any talk or article about this,
  though).

* [Libpcap filters syntax](http://biot.com/capstats/bpf.html)

### About XDP

* [XDP overview](https://www.iovisor.org/technology/xdp) on the IO Visor
  website.

* [_eXpress Data Path (XDP)_](https://github.com/iovisor/bpf-docs/raw/master/Express_Data_Path.pdf)
  (Tom Herbert, Alexei Starovoitov, March 2016):<br />
  The first presentation about XDP.

* [_BoF - What Can BPF Do For You?_](https://events.linuxfoundation.org/sites/events/files/slides/iovisor-lc-bof-2016.pdf)
  (Brenden Blanco, LinuxCon, Toronto, August 2016).<br />

* [_eXpress Data Path_](http://www.slideshare.net/IOVisor/express-data-path-linux-meetup-santa-clara-july-2016)
  (Brenden Blanco, Linux Meetup at Santa Clara, July 2016):<br />
  Contains some (somewhat marketing?) **benchmark results**! With a single core:
  * ip routing drop: ~3.6 million packets per second (Mpps)
  * tc (with clsact qdisc) drop using BPF: ~4.2 Mpps
  * XDP drop using BPF: 20 Mpps (<10 % CPU utilization)
  * XDP forward (on port on which the packet was received) with rewrite: 10 Mpps

  (Tests performed with the mlx4 driver).

* Jesper Dangaard Brouer has several excellent sets of slides, that are
  essential to fully understand the internals of XDP.
  * [_XDP − eXpress Data Path, Intro and future use-cases_](http://people.netfilter.org/hawk/presentations/xdp2016/xdp_intro_and_use_cases_sep2016.pdf)
    (September 2016):<br />
    _“Linux Kernel’s fight against DPDK”_. **Future plans** (as of this
    writing) for XDP and comparison with DPDK.
  * [_Network Performance Workshop_](http://netdevconf.org/1.2/session.html?jesper-performance-workshop)
    (netdev 1.2, Tokyo, October 2016):<br />
    Additional hints about XDP internals and expected evolution.
  * [_XDP – eXpress Data Path, Used for DDoS protection_](http://people.netfilter.org/hawk/presentations/OpenSourceDays2017/XDP_DDoS_protecting_osd2017.pdf)
    (OpenSourceDays, March 2017):<br />
    Contains details and use cases about XDP, with **benchmark results**, and
    **code snippets** for **benchmarking** as well as for **basic DDoS
    protection** with eBPF/XDP (based on an IP blacklisting scheme).
  * [_Memory vs. Networking, Provoking and fixing memory bottlenecks_](http://people.netfilter.org/hawk/presentations/MM-summit2017/MM-summit2017-JesperBrouer.pdf)
    (LSF Memory Management Summit, March 2017):<br />
    Provides a lot of details about current **memory issues** faced by XDP
    developers. Do not start with this one, but if you already know XDP and
    want to see how it really works on the page allocation side, this is a very
    helpful resource.
  * [_XDP for the Rest of Us_](http://netdevconf.org/2.1/session.html?gospodarek)
    (netdev 2.1, Montreal, April 2017), with Andy Gospodarek:<br />
    How to get started with eBPF and XDP for normal humans. This presentation
    was also summarized by Julia Evans on
    [her blog](http://jvns.ca/blog/2017/04/07/xdp-bpf-tutorial/).

  (Jesper also created and tries to extend some documentation about eBPF and
  XDP, see [related section](#about-xdp-1).)

* [_XDP workshop — Introduction, experience, and future development_](http://netdevconf.org/1.2/session.html?herbert-xdp-workshop)
  (Tom Herbert, netdev 1.2, Tokyo, October 2016) — as of this writing, only the
  video is available, I don't know if the slides will be added.

* [_High Speed Packet Filtering on Linux_](https://cdn.shopify.com/s/files/1/0177/9886/files/phv2017-gbertin.pdf)
  (Gilberto Bertin, DEF CON 25, Las Vegas, July 2017) — an excellent
  introduction to state-of-the-art packet filtering on Linux, oriented towards
  DDoS protection, talking about packet processing in the kernel, kernel
  bypass, XDP and eBPF.

### About other components related or based on eBPF

* [_P4 on the Edge_](https://schd.ws/hosted_files/2016p4workshop/1d/Intel%20Fastabend-P4%20on%20the%20Edge.pdf)
  (John Fastabend, May 2016):<br />
  Presents the use of **P4**, a description language for packet processing,
  with BPF to create high-performance programmable switches.

* If you like audio presentations, there is an associated
  [OvS Orbit episode (#11), called _**P4** on the Edge_](https://ovsorbit.benpfaff.org/#e11),
  dating from August 2016. OvS Orbit are interviews realized by Ben Pfaff, who
  is one of the core maintainers of Open vSwitch. In this case, John Fastabend
  is interviewed.

* [_P4, EBPF and Linux TC Offload_](https://open-nfp.org/documents/12/Open-NFP_eBPF-Offload-Starting-Guide_tqigvIR.pdf)
  (Dinan Gunawardena and Jakub Kicinski, August 2016):<br />
  Another presentation on **P4**, with some elements related to eBPF hardware
  offload on Netronome's **NFP** (Network Flow Processor) architecture.

* **Cilium** is a technology initiated by Cisco and relying on BPF and XDP to
  provide “fast in-kernel networking and security policy enforcement for
  containers based on eBPF programs generated on the fly”.
  [The code of this project](https://github.com/cilium/cilium)
  is available on GitHub. Thomas Graf has been performing a number of
  presentations of this topic:
    * [_Cilium: Networking & Security for Containers with BPF & XDP_](http://www.slideshare.net/ThomasGraf5/clium-container-networking-with-bpf-xdp),
      also featuring a load balancer use case
      (Linux Plumbers conference, Santa Fe, November 2016)
    * [_Cilium: Networking & Security for Containers with BPF & XDP_](http://www.slideshare.net/Docker/cilium-bpf-xdp-for-containers-66969823)
      (Docker Distributed Systems Summit, October 2016 —
      [video](https://www.youtube.com/watch?v=TnJF7ht3ZYc&list=PLkA60AVN3hh8oPas3cq2VA9xB7WazcIgs))
    * [_Cilium: Fast IPv6 container Networking with BPF and XDP_](http://www.slideshare.net/ThomasGraf5/cilium-fast-ipv6-container-networking-with-bpf-and-xdp)
      (LinuxCon, Toronto, August 2016)
    * [_Cilium: BPF & XDP for containers_](https://fosdem.org/2017/schedule/event/cilium/)
      (fosdem17, Brussels, Belgium, February 2017)

  A good deal of contents is repeated between the different presentations; if
  in doubt, just pick the most recent one. Daniel Borkmann has also written
  [a generic introduction to Cilium](https://opensource.googleblog.com/2016/11/cilium-networking-and-security.html)
  as a guest author on Google Open Source blog.

* There are also podcasts about **Cilium**: an
  [OvS Orbit episode (#4)](https://ovsorbit.benpfaff.org/),
  in which Ben Pfaff interviews Thomas Graf (May 2016), and
  [another podcast by Ivan Pepelnjak](http://blog.ipspace.net/2016/10/fast-linux-packet-forwarding-with.html),
  still with Thomas Graf about eBPF, P4, XDP and Cilium (October 2016).

* **Open vSwitch** (OvS), and its related project **Open Virtual Network**
  (OVN, an open source network virtualization solution) are considering to use
  eBPF at various level, with several proof-of-concept prototypes already
  implemented:<br >
    * [Offloading OVS Flow Processing using eBPF](http://openvswitch.org/support/ovscon2016/7/1120-tu.pdf)
      (William (Cheng-Chun) Tu, OvS conference, San Jose, November 2016)
    * [Coupling the Flexibility of OVN with the Efficiency of IOVisor](http://openvswitch.org/support/ovscon2016/7/1245-bertrone.pdf)
      (Fulvio Risso, Matteo Bertrone and Mauricio Vasquez Bernal, OvS
      conference, San Jose, November 2016)

  These use cases for eBPF seem to be only at the stage of proposals (nothing
  merge to OvS main branch) as far as I know, but it will be very interesting
  to see what comes out of it.

* XDP is envisioned to be of great help for protection against Distributed
  Denial-of-Service (DDoS) attacks. More and more presentations focus on this.
  For example, the talks from people from Cloudflare
  ([_XDP in practice: integrating XDP in our DDoS mitigation pipeline_](http://netdevconf.org/2.1/session.html?bertin))
  or from Facebook
  ([_Droplet: DDoS countermeasures powered by BPF + XDP_](http://netdevconf.org/2.1/session.html?zhou))
  at the netdev 2.1 conference in Montreal, Canada, in April 2017, present such
  use cases.

* [_CETH for XDP_](http://www.slideshare.net/IOVisor/ceth-for-xdp-linux-meetup-santa-clara-july-2016)
  (Yan Chan and Yunsong Lu, Linux Meetup, Santa Clara, July 2016):<br />
  **CETH** stands for Common Ethernet Driver Framework for faster network I/O,
  a technology initiated by Mellanox.

* [**The VALE switch**](http://info.iet.unipi.it/~luigi/vale/), another virtual
  switch that can be used in conjunction with the netmap framework, has [a BPF
  extension module](https://github.com/YutaroHayakawa/vale-bpf).

* **Suricata**, an open source intrusion detection system,
  [seems to rely on eBPF components](https://www.stamus-networks.com/2016/09/28/suricata-bypass-feature/)
  for its “capture bypass” features:<br />
  [_The adventures of a Suricate in eBPF land_](http://netdevconf.org/1.2/slides/oct6/10_suricata_ebpf.pdf)
  (Éric Leblond, netdev 1.2, Tokyo, October 2016)<br />
  [_eBPF and XDP seen from the eyes of a meerkat_](https://www.slideshare.net/ennael/kernel-recipes-2017-ebpf-and-xdp-eric-leblond)
  (Éric Leblond, Kernel Recipes, Paris, September 2017)

* [InKeV: In-Kernel Distributed Network Virtualization for DCN](https://github.com/iovisor/bpf-docs/blob/master/university/sigcomm-ccr-InKev-2016.pdf)
  (Z. Ahmed, M. H. Alizai and A. A. Syed, SIGCOMM, August 2016):<br />
  **InKeV** is an eBPF-based datapath architecture for virtual networks,
  targeting data center networks. It was initiated by PLUMgrid, and claims to
  achieve better performances than OvS-based OpenStack solutions.

* [_**gobpf** - utilizing eBPF from Go_](https://fosdem.org/2017/schedule/event/go_bpf/)
  (Michael Schubert, fosdem17, Brussels, Belgium, February 2017):<br />
  A “library to create, load and use eBPF programs from Go”

* [**ply**](https://wkz.github.io/ply/) is a small but flexible open source
  dynamic **tracer** for Linux, with some features similar to the bcc tools,
  but with a simpler language inspired by awk and dtrace, written by Tobias
  Waldekranz.

* If you read my previous article, you might be interested in this talk I gave
  about [implementing the OpenState interface with eBPF](https://fosdem.org/2017/schedule/event/stateful_ebpf/),
  for stateful packet processing, at fosdem17.

## Documentation

Once you managed to get a broad idea of what BPF is, you can put aside generic
presentations and start diving into the documentation. Below are the most
complete documents about BPF specifications and functioning. Pick the one you
need and read them carefully!

### About BPF

* The **specification of BPF** (both classic and extended versions) can be
  found within the documentation of the Linux kernel, and in particular in file
  [linux/Documentation/networking/filter.txt][filter.txt].
  The use of BPF as well as its internals are documented there. Also, this is
  where you can find **information about errors thrown by the verifier** when
  loading BPF code fails. Can be helpful to troubleshoot obscure error
  messages.

* Also in the kernel tree, there is a document about **frequent Questions &
  Answers** on eBPF design in file
  [linux/Documentation/bpf/bpf_design_QA.txt](https://git.kernel.org/pub/scm/linux/kernel/git/davem/net-next.git/tree/Documentation/bpf/bpf_design_QA.txt?id=2e39748a4231a893f057567e9b880ab34ea47aef).

* … But the kernel documentation is dense and not especially easy to read. If
  you look for a simple description of eBPF language, head for
  [its **summarized description**](https://github.com/iovisor/bpf-docs/blob/master/eBPF.md)
  on the IO Visor GitHub repository instead.

* By the way, the IO Visor project gathered a lot of **resources about BPF**.
  Mostly, it is split between
  [the documentation directory](https://github.com/iovisor/bcc/tree/master/docs)
  of its bcc repository, and the whole content of
  [the bpf-docs repository](https://github.com/iovisor/bpf-docs/), both on
  GitHub. Note the existence of this excellent
  [BPF **reference guide**][refguide]
  containing a detailed description of BPF C and bcc Python helpers.

* To hack with BPF, there are some essential **Linux manual pages**. The first
  one is
  [the `bpf(2)` man page](http://man7.org/linux/man-pages/man2/bpf.2.html)
  about the `bpf()` **system call**, which is used to manage BPF programs and
  maps from userspace. It also contains a description of BPF advanced features
  (program types, maps and so on). The second one is mostly addressed to people
  wanting to attach BPF programs to tc interface: it is [the `tc-bpf(8)` man
  page](http://man7.org/linux/man-pages/man8/tc-bpf.8.html), which is a
  reference for **using BPF with tc**, and includes some example commands and
  samples of code.

* Jesper Dangaard Brouer initiated an attempt to **update eBPF Linux
  documentation**, including **the different kinds of maps**.
  [He has a draft](https://prototype-kernel.readthedocs.io/en/latest/bpf/index.html)
  to which contributions are welcome. Once ready, this document should be
  merged into the man pages and into kernel documentation.

* The Cilium project also has an excellent [**BPF and XDP Reference
  Guide**](http://docs.cilium.io/en/latest/bpf/), written by core eBPF
  developers, that should prove immensely useful to any eBPF developer.

* David Miller has sent several enlightening emails about eBPF/XDP internals on
  the [xdp-newbies](http://vger.kernel.org/vger-lists.html#xdp-newbies) mailing
  list. I could not find a link that gathers them at a single place, so here is
  a list:
    * [bpf.h and you…](https://www.spinics.net/lists/xdp-newbies/msg00179.html)
    * [Contextually speaking…](https://www.spinics.net/lists/xdp-newbies/msg00181.html)
    * [BPF Verifier Overview](https://www.spinics.net/lists/xdp-newbies/msg00185.html)

  The last one is possibly the best existing summary about the verifier at this
  date.

* Ferris Ellis started
  [a **blog post series about eBPF**](https://ferrisellis.com/tags/ebpf/).
  As I write this paragraph, the first article is out, with some historical
  background and future expectations for eBPF. Next posts should be more
  technical, and look promising.

* [A **list of BPF features per kernel version**][kernfeatures] is available in
  bcc repository. Useful is you want to know the minimal kernel version that is
  required to run a given feature. I contributed and added the links to the
  commits that introduced each feature, so you can also easily access the
  commit logs from there.

[filter.txt]: https://www.kernel.org/doc/Documentation/networking/filter.txt
[refguide]: https://github.com/iovisor/bcc/blob/master/docs/reference_guide.md
[kernfeatures]: https://github.com/iovisor/bcc/blob/master/docs/kernel-versions.md

### About tc

When using BPF for networking purposes in conjunction with tc, the Linux tool
for **t**raffic **c**ontrol, one may wish to gather information about tc's
generic functioning. Here are a couple of resources about it.

* It is difficult to find simple tutorials about **QoS on Linux**. The two
  links I have are long and quite dense, but if you can find the time to read
  it you will learn nearly everything there is to know about tc (nothing about
  BPF, though). There they are:
  [_Traffic Control HOWTO_ (Martin A. Brown, 2006)](http://linux-ip.net/articles/Traffic-Control-HOWTO/),
  and the
  [_Linux Advanced Routing & Traffic Control HOWTO_ (“LARTC”) (Bert Hubert & al., 2002)](http://lartc.org/lartc.html).

* **tc manual pages** may not be up-to-date on your system, since several of
  them have been added lately. If you cannot find the documentation for a
  particular queuing discipline (qdisc), class or filter, it may be worth
  checking the latest
  [manual pages for tc components](https://git.kernel.org/cgit/linux/kernel/git/shemminger/iproute2.git/tree/man/man8).

* Some additional material can be found within the files of iproute2 package
  itself: the package contains [some documentation](https://git.kernel.org/pub/scm/linux/kernel/git/shemminger/iproute2.git/tree/doc?h=v4.13.0),
  including some files that helped me understand better
  [the functioning of **tc's actions**](https://git.kernel.org/pub/scm/linux/kernel/git/shemminger/iproute2.git/tree/doc/actions?h=v4.13.0).<br />
  **Edit:** While still available from the Git history, these files have been
  deleted from iproute2 in October 2017.

* Not exactly documentation: there was
  [a workshop about several tc features](http://netdevconf.org/1.2/session.html?jamal-tc-workshop)
  (including filtering, BPF, tc offload, …) organized by Jamal Hadi Salim
  during the netdev 1.2 conference (October 2016).

* Bonus information—If you use `tc` a lot, here are some good news: I [wrote a
  bash completion
  function](https://git.kernel.org/cgit/linux/kernel/git/shemminger/iproute2.git/commit/bash-completion/tc?id=27d44f3a8a4708bcc99995a4d9b6fe6f81e3e15b)
  for this tool, and it should be shipped with package iproute2 coming with
  kernel version 4.6 and higher!

### About XDP

* Some
  [work-in-progress documentation (including specifications)](https://prototype-kernel.readthedocs.io/en/latest/networking/XDP/index.html)
  for XDP started by Jesper Dangaard Brouer, but meant to be a collaborative
  work. Under progress (September 2016): you should expect it to change, and
  maybe to be moved at some point (Jesper
  [called for contribution](https://marc.info/?l=linux-netdev&m=147436253625672),
  if you feel like improving it).

* The [BPF and XDP Reference Guide](http://docs.cilium.io/en/latest/bpf/) from
  Cilium project… Well, the name says it all.

### About P4 and BPF

[P4](http://p4.org/) is a language used to specify the behavior of a switch. It
can be compiled for a number of hardware or software targets. As you may have
guessed, one of these targets is BPF… The support is only partial: some P4
features cannot be translated towards BPF, and in a similar way there are
things that BPF can do but that would not be possible to express with P4.
Anyway, the documentation related to **P4 use with BPF**
[used to be hidden in bcc repository](https://github.com/iovisor/bcc/tree/master/src/cc/frontends/p4).
This changed with P4_16 version, the p4c reference compiler including
[a backend for eBPF](https://github.com/p4lang/p4c/blob/master/backends/ebpf/README.md).

## Tutorials

Brendan Gregg has produced excellent **tutorials** intended for people who want
to **use bcc tools** for tracing and monitoring events in the kernel.
[The first tutorial about using bcc itself](https://github.com/iovisor/bcc/blob/master/docs/reference_guide.md)
comes with eleven steps (as of today) to understand how to use the existing
tools, while
[the one **intended for Python developers**](https://github.com/iovisor/bcc/blob/master/docs/tutorial_bcc_python_developer.md)
focuses on developing new tools, across seventeen “lessons”.

Sasha Goldshtein also has some
[_**Linux Tracing Workshops Materials**_](https://github.com/goldshtn/linux-tracing-workshop)
involving the use of several BPF tools for tracing.

Another post by Jean-Tiare Le Bigot provides a detailed (and instructive!)
example of
[using perf and eBPF to setup a low-level tracer](https://blog.yadutaf.fr/2017/07/28/tracing-a-packet-journey-using-linux-tracepoints-perf-ebpf/)
for ping requests and replies

Few tutorials exist for network-related eBPF use cases. There are some
interesting documents, including an _eBPF Offload Starting Guide_, on the
[Open NFP](https://open-nfp.org/dataplanes-ebpf/technical-papers/) platform
operated by Netronome. Other than these, the talk from Jesper,
[_XDP for the Rest of Us_](http://netdevconf.org/2.1/session.html?gospodarek),
is probably one of the best ways to get started with XDP.

## Examples

It is always nice to have examples. To see how things really work. But BPF
program samples are scattered across several projects, so I listed all the ones
I know of. The examples do not always use the same helpers (for instance, tc
and bcc both have their own set of helpers to make it easier to write BPF
programs in C language).

### From the kernel

The kernel contains examples for most types of program: filters to bind to
sockets or to tc interfaces, event tracing/monitoring, and even XDP. You can
find these examples under the
[linux/samples/bpf/](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/samples/bpf)
directory.

Also do not forget to have a look to the logs related to the (git) commits that
introduced a particular feature, they may contain some detailed example of the
feature.

### From package iproute2

The iproute2 package provide several examples as well. They are obviously
oriented towards network programming, since the programs are to be attached to
tc ingress or egress interfaces. The examples dwell under the
[iproute2/examples/bpf/](https://git.kernel.org/cgit/linux/kernel/git/shemminger/iproute2.git/tree/examples/bpf)
directory.

### From bcc set of tools

Many examples are [provided with bcc](https://github.com/iovisor/bcc/tree/master/examples):

* Some are networking example programs, under the associated directory. They
  include socket filters, tc filters, and a XDP program.

* The `tracing` directory include a lot of example **tracing programs**. The
  tutorials mentioned earlier are based on these. These programs cover a wide
  range of event monitoring functions, and some of them are
  production-oriented. Note that on certain Linux distributions (at least for
  Debian, Ubuntu, Fedora, Arch Linux), these programs have been
  [packaged](https://github.com/iovisor/bcc/blob/master/INSTALL.md) and can be
  “easily” installed by typing e.g. `# apt install bcc-tools`, but as of this
  writing (and except for Arch Linux), this first requires to set up IO Visor's
  own package repository.

* There are also some examples **using Lua** as a different BPF back-end (that
  is, BPF programs are written with Lua instead of a subset of C, allowing to
  use the same language for front-end and back-end), in the third directory.

### Manual pages

While bcc is generally the easiest way to inject and run a BPF program in the
kernel, attaching programs to tc interfaces can also be performed by the `tc`
tool itself. So if you intend to **use BPF with tc**, you can find some example
invocations in the
[`tc-bpf(8)` manual page](http://man7.org/linux/man-pages/man8/tc-bpf.8.html).

## The Code

Sometimes, BPF documentation or examples are not enough, and you may have no
other solution that to display the code in your favorite text editor (which
should be Vim of course) and to read it. Or you may want to hack into the code
so as to patch or add features to the machine. So here are a few pointers to
the relevant files, finding the functions you want is up to you!

### BPF code in the kernel

* The file
  [linux/include/linux/bpf.h](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/include/linux/bpf.h)
  and its counterpart
  [linux/include/uapi/bpf.h](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/include/uapi/linux/bpf.h)
  contain **definitions** related to eBPF, to be used respectively in the
  kernel and to interface with userspace programs.

* On the same pattern, files
  [linux/include/linux/filter.h](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/include/linux/filter.h)
  and
  [linux/include/uapi/filter.h](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/include/uapi/linux/filter.h)
  contain information used to **run the BPF programs**.

* The **main pieces of code** related to BPF are under
  [linux/kernel/bpf/](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/bpf)
  directory. **The different operations permitted by the system call**, such as
  program loading or map management, are implemented in file `syscall.c`, while
  `core.c` contains the **interpreter**. The other files have self-explanatory
  names: `verifier.c` contains the **verifier** (no kidding), `arraymap.c` the
  code used to interact with **maps** of type array, and so on.

* The **helpers**, as well as several functions related to networking (with tc,
  XDP…) and available to the user, are implemented in
  [linux/net/core/filter.c](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/core/filter.c).
  It also contains the code to migrate cBPF bytecode to eBPF (since all cBPF
  programs are now translated to eBPF in the kernel before being run).


* The **JIT compilers** are under the directory of their respective
  architectures, such as file
  [linux/arch/x86/net/bpf\_jit\_comp.c](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/arch/x86/net/bpf_jit_comp.c)
  for x86.

* You will find the code related to **the BPF components of tc** in the
  [linux/net/sched/](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/sched)
  directory, and in particular in files `act_bpf.c` (action) and `cls_bpf.c`
  (filter).

* I have not hacked with **event tracing** in BPF, so I do not really know
  about the hooks for such programs. There is some stuff in
  [linux/kernel/trace/bpf\_trace.c](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/trace/bpf_trace.c).
  If you are interested in this and want to know more, you may dig on the side
  of Brendan Gregg's presentations or blog posts.

* Nor have I used **seccomp-BPF**. But the code is in
  [linux/kernel/seccomp.c](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/seccomp.c),
  and some example use cases can be found in
  [linux/tools/testing/selftests/seccomp/seccomp\_bpf.c](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/tools/testing/selftests/seccomp/seccomp_bpf.c).

### XDP hooks code

Once loaded into the in-kernel BPF virtual machine, **XDP** programs are hooked
from userspace into the kernel network path thanks to a Netlink command. On
reception, the function `dev_change_xdp_fd()` in file
[linux/net/core/dev.c](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/core/dev.c)
is called and sets a XDP hook. Such hooks are located in the drivers of
supported NICs. For example, the mlx4 driver used for some Mellanox hardware
has hooks implemented in files under the
[drivers/net/ethernet/mellanox/mlx4/](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/drivers/net/ethernet/mellanox/mlx4/)
directory. File en\_netdev.c receives Netlink commands and calls
`mlx4_xdp_set()`, which in turns calls for instance `mlx4_en_process_rx_cq()`
(for the RX side) implemented in file en\_rx.c.

### BPF logic in bcc

One can find the code for the **bcc** set of tools
[on the bcc GitHub repository](https://github.com/iovisor/bcc/).
The **Python code**, including the `BPF` class, is initiated in file
[bcc/src/python/bcc/\_\_init\_\_.py](https://github.com/iovisor/bcc/blob/master/src/python/bcc/__init__.py).
But most of the interesting stuff—to my opinion—such as loading the BPF program
into the kernel, happens
[in the libbcc **C library**](https://github.com/iovisor/bcc/blob/master/src/cc/libbpf.c).

### Code to manage BPF with tc

The code related to BPF **in tc** comes with the iproute2 package, of course.
Some of it is under the
[iproute2/tc/](https://git.kernel.org/cgit/linux/kernel/git/shemminger/iproute2.git/tree/tc)
directory. The files f\_bpf.c and m\_bpf.c (and e\_bpf.c) are used respectively
to handle BPF filters and actions (and tc `exec` command, whatever this may
be). File q\_clsact.c defines the `clsact` qdisc especially created for BPF.
But **most of the BPF userspace logic** is implemented in
[iproute2/lib/bpf.c](https://git.kernel.org/cgit/linux/kernel/git/shemminger/iproute2.git/tree/lib/bpf.c)
library, so this is probably where you should head to if you want to mess up
with BPF and tc (it was moved from file iproute2/tc/tc_bpf.c, where you may
find the same code in older versions of the package).

### BPF utilities

The kernel also ships the sources of three tools (`bpf_asm.c`, `bpf_dbg.c`,
`bpf_jit_disasm.c`) related to BPF, under the
[linux/tools/net/](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/tools/net)
or
[linux/tools/bpf/](https://git.kernel.org/pub/scm/linux/kernel/git/davem/net-next.git/tree/tools/bpf)
directory depending on your version:

* `bpf_asm` is a minimal cBPF assembler.
* `bpf_dbg` is a small debugger for cBPF programs.
* `bpf_jit_disasm` is generic for both BPF flavors and could be highly useful
  for JIT debugging.
* `bpftool` is a generic utility written by Jakub Kicinski, and that can be
  used to interact with eBPF programs and maps from userspace, for example to
  show, dump, pin programs, or to show, create, pin, update, delete maps.

Read the comments at the top of the source files to get an overview of their
usage.

### Other interesting chunks

If you are interested the use of less common languages with BPF, bcc contains
[a **P4 compiler** for BPF targets](https://github.com/iovisor/bcc/tree/master/src/cc/frontends/p4/compiler)
as well as
[a **Lua front-end**](https://github.com/iovisor/bcc/tree/master/src/lua) that
can be used as alternatives to the C subset and (in the case of Lua) to the
Python tools.

### LLVM backend

The BPF backend used by clang / LLVM for compiling C into eBPF was added to the
LLVM sources in
[this commit](https://reviews.llvm.org/D6494)
(and can also be accessed on
[the GitHub mirror](https://github.com/llvm-mirror/llvm/commit/4fe85c75482f9d11c5a1f92a1863ce30afad8d0d)).

### Running in userspace

As far as I know there are at least two eBPF userspace implementations. The
first one, [uBPF](https://github.com/iovisor/ubpf/), is written in C. It
contains an interpreter, a JIT compiler for x86_64 architecture, an assembler
and a disassembler.

The code of uBPF seems to have been reused to produce a
[generic implementation](https://github.com/YutaroHayakawa/generic-ebpf),
that claims to support FreeBSD kernel, FreeBSD userspace, Linux kernel,
Linux userspace and MacOSX userspace. It is used for the [BPF extension module
for VALE switch](https://github.com/YutaroHayakawa/vale-bpf).

The other userspace implementation is my own work:
[rbpf](https://github.com/qmonnet/rbpf), based
on uBPF, but written in Rust. The interpreter and JIT-compiler work (both under
Linux, only the interpreter for MacOSX and Windows), there may
be more in the future.

### Commit logs

As stated earlier, do not hesitate to have a look at the commit log that
introduced a particular BPF feature if you want to have more information about
it. You can search the logs in many places, such as on
[git.kernel.org](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git),
[on GitHub](https://github.com/torvalds/linux), or on your local
repository if you have cloned it. If you are not familiar with git, try things
like `git blame <file>` to see what commit introduced a particular line of
code, then `git show <commit>` to have details (or search by keyword in `git
log` results, but this may be tedious). See also [the list of eBPF features per
kernel version][kernfeatures] on bcc repository, that links to relevant
commits.

## Playing With BPF and XDP

* In case you would like to easily **test XDP**, there is
  [a Vagrant setup](https://github.com/iovisor/xdp-vagrant) available. You can
  also **test bcc**
  [in a Docker container](https://github.com/zlim/bcc-docker).

## BPF Development

* The kernel patches always end up
  [on the netdev mailing list](http://lists.openwall.net/netdev/)
  (related to the Linux kernel networking stack development): search for “BPF”
  or “XDP” keywords. Since April 2017, there is also
  [a mailing list specially dedicated to XDP programming](http://vger.kernel.org/vger-lists.html#xdp-newbies)
  (both for architecture or for asking for help). Many discussions and debates
  also occur
  [on the IO Visor mailing list](http://lists.iovisor.org/pipermail/iovisor-dev/),
  since BPF is at the heart of the project. If you only want to keep informed
  from time to time, there is also an
  [@IOVisor Twitter account](https://twitter.com/IOVisor).

## Contribute

Contributions welcome! Read the [contribution guidelines](contributing.md) first.

## License

[![CC0](http://mirrors.creativecommons.org/presskit/buttons/88x31/svg/cc-zero.svg)](http://creativecommons.org/publicdomain/zero/1.0)

To the extent possible under law, zoidbergwill has waived all copyright and
related or neighboring rights to this work.
