# Awesome eBPF [![Awesome](https://awesome.re/badge.svg)](https://github.com/sindresorhus/awesome)

> A curated list of awesome projects related to eBPF.

BPF, as in _Berkeley Packet Filter_, is an in-kernel virtual machine running programs passed from user space. Initially implemented on BSD, then Linux, the (now legacy) "classic BPF" or cBPF machine would be used with tools like tcpdump for filtering packets in the kernel to avoid useless copies to user space. More recently, the BPF infrastructure in Linux has been completely reworked and gave life to the "extended BPF", or eBPF, which gained new features (safety and termination checks, JIT-compiling for programs, persistent maps, a standard library, hardware offload support, etc.) and is now used for many tasks. Processing packets at a very low level (XDP), tracing and monitoring events on the system, or enforcing access control over cgroups are but a few examples to which eBPF brings performance, programmability and flexibility.

Recently, [Cilium](https://cilium.io) launched a great website about eBPF called [ebpf.io](https://ebpf.io/). It serves a similar purpose to this list, with [an introduction to eBPF](https://ebpf.io/what-is-ebpf) and links to [related projects](https://ebpf.io/projects).

> Note: eBPF is an exciting piece of technology, and its ecosystem is constantly evolving. We'd love help from _you_ to keep this awesome list up to date, and improve its signal-to-noise ratio in anyway we can. Please feel free to leave [any feedback](https://github.com/zoidbergwill/awesome-ebpf/issues).

## Contents

- [Reference Documentation](#reference-documentation)
- [Articles and Presentations](#articles-and-presentations)
- [Tutorials](#tutorials)
- [Examples](#examples)
- [eBPF Workflow: Tools and Utilities](#ebpf-workflow-tools-and-utilities)
- [Projects Related to eBPF](#projects-related-to-ebpf)
- [eBPF in Security](#ebpf-in-security)
- [The Code](#the-code)
- [Development and Community](#development-and-community)
- [Other Lists of Resources on eBPF](#other-lists-of-resources-on-ebpf)
- [Acknowledgement](#acknowledgement)

## Reference Documentation

### eBPF Essentials

- [ebpf.io](https://ebpf.io/) - A gateway to discover all the basics of eBPF, including a listing of the main related projects and of community resources.
- [Cilium's BPF and XDP Reference Guide](http://docs.cilium.io/en/latest/bpf/) - In-depth documentation about most features and aspects of eBPF.

### Kernel Documentation

- [BPF Documentation](https://www.kernel.org/doc/html/latest/bpf/index.html) - Index for BPF-related documentation coming with the Linux kernel.
- [linux/Documentation/networking/filter.rst](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/Documentation/networking/filter.rst) - eBPF specification (somewhat outdated; information should still be valid, but not exhaustive).
- [BPF Design Q&A](https://www.kernel.org/doc/html/latest/bpf/bpf_design_QA.html) - Frequently Asked Questions on the decisions behind the BPF infrastructure.
- [HOWTO interact with BPF subsystem](https://www.kernel.org/doc/html/latest/bpf/bpf_devel_QA.html) - Frequently Asked Questions about contributing to eBPF development.

### Manual Pages

- [`bpf(2)`](http://man7.org/linux/man-pages/man2/bpf.2.html) - Manual page about the `bpf()` system call, used to manage BPF programs and maps from userspace.
- [`tc-bpf(8)`](http://man7.org/linux/man-pages/man8/tc-bpf.8.html) - Manual page about using BPF with tc, including example commands and samples of code.
- [`bpf-helpers(7)` man page](http://man7.org/linux/man-pages/man7/bpf-helpers.7.html) - Description of the in-kernel helper functions forming the BPF standard library.

### Other

- [IO Visor's Unofficial eBPF spec](https://github.com/iovisor/bpf-docs/blob/master/eBPF.md) - Summary of eBPF syntax and operation codes.
- [Jesper Dangaard Brouer's documentation](https://prototype-kernel.readthedocs.io/en/latest/bpf/index.html) - Work in progress, contributions welcome.
- Emails from David Miller to the [xdp-newbies](http://vger.kernel.org/vger-lists.html#xdp-newbies) mailing list:

  - [bpf.h and you...](https://www.spinics.net/lists/xdp-newbies/msg00179.html)
  - [Contextually speaking...](https://www.spinics.net/lists/xdp-newbies/msg00181.html)
  - [BPF Verifier Overview](https://www.spinics.net/lists/xdp-newbies/msg00185.html)

- [List of BPF features per kernel version](https://github.com/iovisor/bcc/blob/master/docs/kernel-versions.md)
- [A List of Research Papers](https://pchaigno.github.io/bpf/2025/01/07/research-papers-bpf.html)

## Articles and Presentations

### Generic eBPF Presentations and Articles

If you are new to eBPF, you may want to try the links described as "introductions" in this section.

- [A brief introduction to XDP and eBPF](https://blogs.igalia.com/dpino/2019/01/07/introduction-to-xdp-and-ebpf/) - An accessible introduction providing context, history, and details about the functioning of eBPF.
- An eBPF Overview - Blog series by Adrian Ratiu, covering many aspects of the eBPF infrastructure:

  - [Part 1: Introduction](https://www.collabora.com/news-and-blog/blog/2019/04/05/an-ebpf-overview-part-1-introduction/)
  - [Part 2: Machine & Bytecode](https://www.collabora.com/news-and-blog/blog/2019/04/15/an-ebpf-overview-part-2-machine-and-bytecode/)

- [Ferris Ellis's blog posts about eBPF](https://ferrisellis.com/tags/ebpf/) - They have a few posts about eBPF:
  - [Part 1: Past, Present, and Future](https://ferrisellis.com/content/ebpf_past_present_future/)
  - [Part 2: Syscall and Map Types](https://ferrisellis.com/content/ebpf_syscall_and_maps/)
- [A BPF reference guide](https://github.com/iovisor/bcc/blob/master/docs/reference_guide.md) - About BPF C and bcc Python helpers, from bcc repository.
- [Making the Kernel's Networking Data Path Programmable with BPF and XDP](http://schd.ws/hosted_files/ossna2017/da/BPFandXDP.pdf) - A set of slides covering all the basics about eBPF and XDP (mostly for network processing).
- [The BSD Packet Filter](https://speakerdeck.com/tuxology/the-bsd-packet-filter) - An introduction mostly covering the tracing aspects.
- [BPF: tracing and more](http://www.slideshare.net/brendangregg/bpf-tracing-and-more) - An introduction mostly covering the tracing aspects.
- [Linux BPF Superpowers](http://www.slideshare.net/brendangregg/linux-bpf-superpowers) - An introduction mostly covering the tracing aspects, first part with flame graphs.
- [IO Visor](https://www.socallinuxexpo.org/sites/default/files/presentations/Room%20211%20-%20IOVisor%20-%20SCaLE%2014x.pdf) - Also introduces [IO Visor project](https://www.iovisor.org/).
- [BPF -- in-kernel virtual machine](http://vger.kernel.org/netconf2015Starovoitov-bpf_collabsummit_2015feb20.pdf) - Presentation by the author of eBPF.
- [Extending extended BPF](https://lwn.net/Articles/603983/) - A blog post from 2014 on the development of BPF and demonstrating what can be done with it, using an example of stateful socket filtering by attaching an eBPF program to a socket.
- Greg Marsden made some documentation about eBPF:
  - [A Tour of Program Types](https://blogs.oracle.com/linux/notes-on-bpf-1) - A description of all existing hooks for BPF program types, and of their interest.
  - [BPF helper functions](https://blogs.oracle.com/linux/notes-on-bpf-2) - A review of the kernel functions that can be called from within eBPF programs.
  - [Communicating with Userspace](https://blogs.oracle.com/linux/notes-on-bpf-3) - How BPF communicates with userspace - BPF maps, perf events, bpf_trace_printk.
  - [Building BPF Programs](https://blogs.oracle.com/linux/notes-on-bpf-4) - Setting up your environment to build BPF programs.
  - [The BPF Bytecode and the BPF Verifier](https://blogs.oracle.com/linux/notes-on-bpf-5) - How does BPF ensure that programs are safe?
  - [Using BPF to do Packet Transformation](https://blogs.oracle.com/linux/notes-on-bpf-6) - One eBPF usage about packet transformation.
- [Linux Kernel Observability through eBPF](https://sematext.com/blog/linux-kernel-observability-ebpf/) - A blog post covering the basics of eBPF as well as code samples in Go on how to build and load a minimal eBPF program into the kernel.
- [eBPF - From a Programmer's Perspective](https://www.researchgate.net/publication/349173667_eBPF_-_From_a_Programmer's_Perspective) - A short paper describing the fundamentals of eBPF and how to get started with writing eBPF programs.
- [Cloudflare's blog posts on eBPF](https://blog.cloudflare.com/tag/ebpf/) - Different blog posts about networking use cases and low-level aspects of eBPF.
- [Linux Extended BPF (eBPF) Tracing Tools](https://www.brendangregg.com/ebpf.html) - An in-depth collection of information around examples of performance analysis tools using eBPF. Contains also a section at the end of the page about other resources.
- [Beginner's guide to eBPF](https://github.com/lizrice/ebpf-beginners) - A set of live-coding talks and the accompanying code examples, introducing eBPF programming using a variety of libraries and program types.

### BPF Internals

- Daniel Borkmann has made several presentations and papers covering the internals of eBPF, in particular about its use with tc.

  - [eBPF and XDP walkthrough and recent (2017) updates](https://fosdem.org/2017/schedule/event/ebpf_xdp/)
  - [Advanced programmability and recent updates with tc's cls_bpf](http://netdevconf.org/1.2/session.html?daniel-borkmann) - Details on eBPF, its use for tunneling and encapsulation, direct packet access, and more.
  - [cls_bpf/eBPF updates since netdev 1.1](http://netdevconf.org/1.2/slides/oct5/07_tcws_daniel_borkmann_2016_tcws.pdf) - Part of [this tc workshop](http://netdevconf.org/1.2/session.html?jamal-tc-workshop).
  - [On getting tc classifier fully programmable with cls_bpf](http://www.netdevconf.org/1.1/proceedings/slides/borkmann-tc-classifier-cls-bpf.pdf) - Introduction to eBPF, including several features (map management, tail calls, verifier). The full paper [is also available here](http://www.netdevconf.org/1.1/proceedings/papers/On-getting-tc-classifier-fully-programmable-with-cls-bpf.pdf).
  - [Linux tc and eBPF](https://archive.fosdem.org/2016/schedule/event/ebpf/attachments/slides/1159/export/events/attachments/ebpf/slides/1159/ebpf.pdf)

- [IO Visor blog](https://www.iovisor.org/resources/blog)
- [Linux Networking Explained](http://www.slideshare.net/ThomasGraf5/linux-networking-explained) - Linux networking internals, with a part about eBPF.

### Kernel Tracing

- [Full-system dynamic tracing on Linux using eBPF and bpftrace](https://www.joyfulbikeshedding.com/blog/2019-01-31-full-system-dynamic-tracing-on-linux-using-ebpf-and-bpftrace.html) - A detailed introduction to tracing with eBPF, from listing the available trace points to running bpftrace programs.
- [Meet-cute between eBPF and Kernel Tracing](http://www.slideshare.net/vh21/meet-cutebetweenebpfandtracing) - Kprobes, uprobes, ftrace.
- [Linux Kernel Tracing](http://www.slideshare.net/vh21/linux-kernel-tracing) - Systemtap, Kernelshark, trace-cmd, LTTng, perf-tool, ftrace, hist-trigger, perf, function tracer, tracepoint, kprobe/uprobe, and more.
- Brendan Gregg's blog, and in particular [Linux BPF Superpowers](http://www.brendangregg.com/blog/2016-03-05/linux-bpf-superpowers.html) article.

### XDP

- [The eXpress Data Path](https://blogs.igalia.com/dpino/2019/01/10/the-express-data-path/) - A very accessible introduction to XDP, providing sample code to show how to process packets.
- All XDP details in a technical paper: [The eXpress Data Path: Fast Programmable Packet Processing in the Operating System Kernel](https://github.com/tohojo/xdp-paper), by Toke Høiland-Jørgensen, Jesper Dangaard Brouer, Daniel Borkmann, John Fastabend, Tom Herbert, David Ahern and David Miller, all being essential eBPF and XDP contributors.
- [Work-in-progress documentation for XDP](https://prototype-kernel.readthedocs.io/en/latest/networking/XDP/index.html)
- [BPF and XDP Reference Guide](http://docs.cilium.io/en/latest/bpf/) - Guide from the Cilium project.
- [XDP Project overview](https://www.iovisor.org/technology/xdp)
- [eXpress Data Path (XDP)](https://github.com/iovisor/bpf-docs/raw/master/Express_Data_Path.pdf) - The first presentation about XDP.
- [BoF - What Can BPF Do For You?](https://events.linuxfoundation.org/sites/events/files/slides/iovisor-lc-bof-2016.pdf)
- [eXpress Data Path](http://www.slideshare.net/IOVisor/express-data-path-linux-meetup-santa-clara-july-2016) - Contains some benchmark results obtained with the mlx4 driver.
- Jesper Dangaard Brouer has several sets of slides describing the internals of XDP:

  - [XDP − eXpress Data Path, Intro and future use-cases](http://people.netfilter.org/hawk/presentations/xdp2016/xdp_intro_and_use_cases_sep2016.pdf) - Linux Kernel's fight against DPDK. Future plans (as of this writing) for XDP and comparison with DPDK.
  - [Network Performance Workshop](http://netdevconf.org/1.2/session.html?jesper-performance-workshop) - Additional hints about XDP internals and expected evolution.
  - [XDP – eXpress Data Path, Used for DDoS protection](http://people.netfilter.org/hawk/presentations/OpenSourceDays2017/XDP_DDoS_protecting_osd2017.pdf) - Details and use cases about XDP, with benchmark results, and code snippets for benchmarking as well as for basic DDoS protection with eBPF/XDP (based on an IP blacklisting scheme).
  - [Memory vs. Networking, Provoking and fixing memory bottlenecks](http://people.netfilter.org/hawk/presentations/MM-summit2017/MM-summit2017-JesperBrouer.pdf) - Advanced details about current memory issues faced by XDP developers.
  - [XDP for the Rest of Us](http://netdevconf.org/2.1/session.html?gospodarek) - How to get started with eBPF and XDP for normal humans. Also summarized by Julia Evans on [her blog](http://jvns.ca/blog/2017/04/07/xdp-bpf-tutorial/).
  - [XDP now with REDIRECT](http://people.netfilter.org/hawk/presentations/LLC2018/XDP_LLC2018_redirect.pdf) - Update on XDP, and in particular on the redirect actions.

- [XDP workshop -- Introduction, experience, and future development (Video)](http://netdevconf.org/1.2/session.html?herbert-xdp-workshop)
- [High Speed Packet Filtering on Linux](https://cdn.shopify.com/s/files/1/0177/9886/files/phv2017-gbertin.pdf) - About packet filtering on Linux, DDoS protection, packet processing in the kernel, kernel bypass, XDP and eBPF.
- [How to drop 10 million packets per second](https://blog.cloudflare.com/how-to-drop-10-million-packets/) - Cloudflare's blog post talking about their move to using XDP for packet filtering.

### AF_XDP

- [AF_XDP](https://www.kernel.org/doc/html/latest/networking/af_xdp.html) - Kernel documentation on the AF_XDP address family.
- [Fast Packet Processing in Linux with AF_XDP](https://archive.fosdem.org/2018/schedule/event/af_xdp/)

### bpfilter

- [Why is the kernel community replacing iptables with BPF?](https://cilium.io/blog/2018/04/17/why-is-the-kernel-community-replacing-iptables/) - A blog post by Cilium on the motivations behind eBPF and bpfilter, with a couple examples and links to other projects using eBPF and bpfilter.
- [bpfilter: Linux firewall with eBPF sauce](https://qmo.fr/docs/talk_20180316_frnog_bpfilter.pdf) - Slides from a talk by Quentin Monnet with a background on eBPF and comparing bpfilter to iptables.

### BTF

- [BPF Type Format (BTF)](https://www.kernel.org/doc/html/latest/bpf/btf.html) - Kernel documentation about BTF, explaining how to use it.
- [Enhancing the Linux kernel with BTF type information](https://facebookmicrosites.github.io/bpf/blog/2018/11/14/btf-enhancement.html) - A description of the work done with BTF to provide debugging information for BPF programs.
- [What is BTF (BPF Type Format)](https://cloudchirp.substack.com/p/what-is-btf-bpf-type-format) - A community-authored newsletter enriched with useful code illustrations and hands-on examples.

### cBPF

- [The BSD Packet Filter: A New Architecture for User-level Packet Capture](http://www.tcpdump.org/papers/bpf-usenix93.pdf) - The original paper about (classic) BPF.
- [The FreeBSD manual page about BPF](https://www.freebsd.org/cgi/man.cgi?query=bpf&sektion=4)
- [Linux' packet mmap(2), BPF, and Netsniff-NG](http://borkmann.ch/talks/2013_devconf.pdf)
- [tc and cls bpf: lightweight packet classifying with BPF](http://borkmann.ch/talks/2014_devconf.pdf)
- [Introducing Cloudflare's BPF Tools](https://blog.cloudflare.com/introducing-the-bpf-tools/) - Usage of BPF bytecode with the `xt_bpf` module for iptables.
- [Libpcap filters syntax](http://biot.com/capstats/bpf.html)

### Hardware Offload

- [eBPF/XDP hardware offload to SmartNICs](http://netdevconf.org/1.2/session.html?jakub-kicinski) - Hardware offload for eBPF with TC or XDP (Linux kernel 4.9+), introduced by Netronome.
- [Comprehensive XDP offload---Handling the edge cases](https://www.netdevconf.org/2.2/session.html?viljoen-xdpoffload-talk) - An update on the topic above.
- [hBPF - eBPF in hardware](https://github.com/rprinz08/hBPF) - An eBPF CPU written for FPGAs.
- [OpenCSD eBPF SSD offloading](https://github.com/Dantali0n/qemu-csd) - Computational Storage simulation (QEMU) platform with FUSE LFS filesystem for Zoned Namespaces NVMe SSDs using uBPF for compute kernel offloading, all in userspace.
- [Delilah: eBPF-offload on Computational Storage](https://dl.acm.org/doi/pdf/10.1145/3592980.3595319) - Delilah is a Computational Storage Processor (CSP) built for eBPF offload to storage devices.

## Tutorials

- [bcc Reference Guide](https://github.com/iovisor/bcc/blob/master/docs/reference_guide.md) - Many incremental steps to start using bcc and eBPF, mostly centered on tracing and monitoring.
- [bcc Python Developer Tutorial](https://github.com/iovisor/bcc/blob/master/docs/tutorial_bcc_python_developer.md) - Comes with bcc, but targets the Python bits across seventeen "lessons".
- [Building BPF applications with libbpf-bootstrap](https://nakryiko.com/posts/libbpf-bootstrap/) - Helps generate minimal or advanced templates to bootstrap your own applications (kernel side and user space management for maps and programs) with features like CO-RE, global variables, and ring buffer.
- [How I ended up writing opensnoop in pure C using eBPF](https://bolinfest.github.io/opensnoop-native/) - A thorough walk-through of how to write eBPF programs, first using only bpf() syscall, and then libbpf library, with reproducible code examples.
- [Linux Tracing Workshops Materials](https://github.com/goldshtn/linux-tracing-workshop) - Involves the use of several BPF tools for tracing.
- [Tracing a packet journey using Linux tracepoints, perf and eBPF](https://blog.yadutaf.fr/2017/07/28/tracing-a-packet-journey-using-linux-tracepoints-perf-ebpf/) - Troubleshooting ping requests and replies with perf and bcc programs.
- [Open NFP platform](https://open-nfp.org/dataplanes-ebpf/technical-papers/) - Operated by Netronome: some tutorials for network-related eBPF use cases, including an eBPF Offload Starting Guide.
- [XDP for the Rest of Us](http://netdevconf.org/2.1/session.html?gospodarek) - First edition of a workshop to get started with XDP.
- [XDP for the Rest of Us](https://www.netdevconf.org/2.2/session.html?gospodarek-xdp-workshop) - Second edition, with new contents.
- [Load XDP programs using the ip (iproute2) command](https://medium.com/@fntlnz/load-xdp-programs-using-the-ip-iproute2-command-502043898263)
- [XDP Hands-On Tutorial](https://github.com/xdp-project/xdp-tutorial) - A progressive (three levels of difficulty) tutorial to learn how to process packets with XDP.
- [All your tracing are belong to BPF](https://blog.trailofbits.com/2021/11/09/all-your-tracing-are-belong-to-bpf/) - A step-by-step walkthrough to integrate tracing capabilities in your C++ applications with the LLVM libraries.
- [Firewalling with BPF/XDP: Examples and Deep Dive](https://arthurchiao.art/blog/firewalling-with-bpf-xdp/) - A simple guide to build basic firewalls with TC and XDP.
- [A Deep Dive into eBPF: Writing an Efficient DNS Monitoring.](https://medium.com/@nurkholish.halim/a-deep-dive-into-ebpf-writing-an-efficient-dns-monitoring-2c9dea92abdf) - A detailed explanation of methods used to capture DNS requests at the socket filter layer.
- [eBPF Developer Tutorial - Learn eBPF by examples](https://eunomia.dev/tutorials/) - Start with eBPF basics and progress to advanced topics using 20+ hands-on tutorials and examples. Covers performance, networking, and security with libbpf and CO-RE. Available in Chinese and English.
- [Catch Performance Regressions in eBPF](https://bencher.dev/docs/explanation/talks/#linuxcon-2023-12-may-23) - A step-by-step guide to benchmarking both the client and kernel eBPF code written in Rust.
- [Loops and Iterators in eBPF](https://cloudchirp.substack.com/p/loops-and-iterators-in-ebpf) - Newsletter about all the ways to loop and iterate in eBPF.
- [What Insights Can eBPF Provide into Real-Time SSL/TLS Encrypted Traffic and How?](https://cloudchirp.substack.com/p/what-insights-can-ebpf-provide-into) - A step-by-step guide how eBPF can observe encrypted network traffic.
- [Can eBPF Detect Redis Message Patterns Before They Become Problems?](https://cloudchirp.substack.com/p/can-ebpf-detect-redis-message-patterns) - A step-by-step guide how eBPF can observe Redis communication between client and server.
- [Transparent Proxy Implementation using eBPF and Go](https://cloudchirp.substack.com/p/transparent-proxy-implementation) - A step-by-step guide on how to implement a transparent proxy using eBPF.
- [eBPF-Powered Load Balancing](https://cloudchirp.substack.com/p/ebpf-powered-load-balancing-for-so_reuseport) - Learn how eBPF can infer custom load-balancing for services listening on the same port, through the SO_REUSEPORT TCP option.
- [Unit Testing eBPF Programs](https://ebpfchirp.substack.com/p/unit-testing-ebpf-programs) - Learn how you can unit test your eBPF programs using libbpf.
- [Accelerating Local Socket Communication using eBPF](https://cloudchirp.substack.com/p/optimizing-local-socket-communication) - Learn how eBPF can speed-up local socket communication up to 30%.
- [Writing a basic continuous profiler](https://blog.maxgio.me/posts/unleashing-power-frame-pointers-writing-simple-continuous-profiler/) - A step-by-step guide to write an appliation continuous profiler leveraging the eBPF instrumentation, with a complete project as a reference.
- [Inspektor Gadget - Hello world gadget](https://inspektor-gadget.io/docs/latest/gadget-devel/hello-world-gadget) - An introductory guide to writing image-based eBPF gadgets and sharing them via OCI registries.
- [Inspektor Gadget - Hello world gadget with Wasm](https://inspektor-gadget.io/docs/latest/gadget-devel/hello-world-gadget-wasm) - An introductory guide to writing image-based eBPF gadgets and performing post-processing with WASM.

## Examples

- [linux/samples/bpf/](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/samples/bpf) - In the kernel tree: some sample eBPF programs.
- [linux/tools/testing/selftests/bpf](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/tools/testing/selftests/bpf) - In the kernel tree: Linux BPF selftests, with many eBPF programs.
- [prototype-kernel/kernel/samples/bpf](https://github.com/netoptimizer/prototype-kernel/tree/master/kernel/samples/bpf) - Jesper Dangaard Brouer's prototype-kernel repository contains some additional examples that can be compiled outside of kernel infrastructure.
- [iproute2/examples/bpf/](https://git.kernel.org/pub/scm/network/iproute2/iproute2-next.git/tree/examples/bpf) - Some networking programs to attach to the TC interface.
- [Netronome sample network applications](https://github.com/Netronome/bpf-samples/) - Provides basic but complete examples of eBPF applications also compatible with hardware offload.
- [bcc/examples](https://github.com/iovisor/bcc/tree/master/examples) - Examples coming along with the bcc tools, mostly about tracing.
- [bcc/tools](https://github.com/iovisor/bcc/tree/master/tools) - These tools themselves can be seen as example use cases for BPF programs, mostly for tracing and monitoring. bcc tools have been packaged for some Linux distributions.
- [MPLSinIP sample](https://github.com/fzakaria/eBPF-mpls-encap-decap) - A heavily commented sample demonstrating how to encapsulate & decapsulate MPLS within IP. The code is commented for those new to BPF development.
- [ebpf-samples](https://github.com/vbpf/ebpf-samples) - A collection of compiled (as ELF object files) samples gathered from several projects, primarily intended to serve as test cases for user space verifiers.
- [ebpf-kill-example](https://github.com/niclashedam/ebpf-kill-example) - A fully documented and tested example of an eBPF probe that logs all force-kills and prints them out in user-space.
- [redbpf examples](https://github.com/foniod/redbpf/tree/main/examples) - Example programs for using RedBPF to write eBPF programs in Rust.
- [XDP/TC-eBPF example](https://github.com/netfoundry/zfw) - Program that uses XDP/TC-eBPF to provide statefull firewalling and socket redirection.

## eBPF Workflow: Tools and Utilities

### bcc

- [bcc](https://github.com/iovisor/bcc/) - Framework and set of tools - One way to handle BPF programs, in particular for tracing and monitoring. Also includes some utilities that may help inspect maps or programs on the system.
- [Lua front-end for BCC](https://github.com/iovisor/bcc/tree/master/src/lua) - Another alternative to C, and even to most of the Python code used in bcc.

### iproute2

- [iproute2](https://git.kernel.org/pub/scm/network/iproute2/iproute2.git) - Package containing tools for network management on Linux. In particular, it contains `tc`, used to manage eBPF filters and actions, and `ip`, used to manage XDP programs. Most of the code related to BPF is in lib/bpf.c.
- [iproute2-next](https://git.kernel.org/pub/scm/network/iproute2/iproute2-next.git) - The development tree, synchronised with net-next.

### LLVM

- [LLVM](https://llvm.org/) - Contains several tools used in eBPF workflows. Snapshots of the latest versions for Ubuntu/Debian can be retrieved from [here](http://apt.llvm.org/).

  - clang is used to compile C to eBPF object file under the ELF format (clang v3.7.1+). The BPF backend was added with [this commit](https://reviews.llvm.org/D6494).
  - llvm-objdump is used to dump the content of an object file in human-readable format, possibly with the initial C source code (llvm-objdump v4.0+).
  - llvm-mc is used to compile from LLVM intermediate representation to eBPF object file, so that one can compile from C to eBPF assembly, tinker with assembly, then compile to ELF file.

### libbpf

- [libbpf](https://git.kernel.org/pub/scm/linux/kernel/git/davem/net-next.git/tree/tools/lib/bpf) - A C library used for handling BPF objects (programs and maps), and manipulating ELF object files containing them. It is shipped with the kernel and [mirrored on GitHub](https://github.com/libbpf/libbpf).
- [libbpf-bootstrap](https://github.com/libbpf/libbpf-bootstrap) - Scaffolding for BPF application development with libbpf and BPF CO-RE.

### Go libraries

- [cilium/ebpf](https://github.com/cilium/ebpf) - Pure-Go library to read, modify and load eBPF programs and attach them to various hooks in the Linux kernel.
- [libbpfgo](https://github.com/aquasecurity/libbpfgo) - eBPF library for Go, powered by libbpf.
- [gobpf](https://github.com/iovisor/gobpf) - Go bindings for BCC for creating eBPF programs.

### Aya

- [aya](https://github.com/aya-rs/aya) - A pure Rust library for writing, loading, and managing eBPF objects, with a focus on developer experience and operability. It supports writing eBPF programs in Rust and distributing library code over crates.io to share it between eBPF programs. Aya does not depend on libbpf.
- [aya-template](https://github.com/aya-rs/aya-template) - Templates for writing BPF applications in Aya that can be used with [`cargo generate`](https://github.com/cargo-generate/cargo-generate).
- [Ebpfguard](https://github.com/deepfence/ebpfguard) - Rust library for writing Linux security policies using eBPF.

### zbpf

- [zbpf](https://github.com/tw4452852/zbpf) - A pure Zig framework for writing cross platform eBPF programs, powered by libbpf and Zig toolchain.

### eunomia-bpf

- [eunomia-bpf](https://github.com/eunomia-bpf/eunomia-bpf) - A compilation framework and runtime library to build, distribute, dynamically load, and run CO-RE eBPF applications in multiple languages and WebAssembly. It supports writing eBPF kernel code only (to build simple CO-RE libbpf eBPF applications), writing the kernel part in both BCC and libbpf styles, and writing userspace in multiple languages in a WASM module and distributing it with simple JSON data or WASM OCI images. The runtime is based on libbpf only and provides CO-RE to BCC-style eBPF programs without depending on the LLVM library.

### oxidebpf

- [oxidebpf](https://github.com/redcanaryco/oxidebpf) - A pure Rust library for managing eBPF programs, designed for security use cases. The featureset is more limited than other libraries but emphasizes stability across a wide range of kernels and backwards-compatible compile-once-run-most-places.

### bpftool and Other Tools from the Kernel Tree

- [bpftool](https://git.kernel.org/pub/scm/linux/kernel/git/bpf/bpf-next.git/tree/tools/bpf/bpftool) - Also some other tools in the kernel tree, under [linux/tools/net/](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/tools/net?h=v4.14) for versions earlier than 4.15, or [linux/tools/bpf/](https://git.kernel.org/pub/scm/linux/kernel/git/davem/net-next.git/tree/tools/bpf) after that:

  - [`bpftool`](https://git.kernel.org/pub/scm/linux/kernel/git/bpf/bpf-next.git/tree/tools/bpf/bpftool) - A generic utility that can be used to interact with eBPF programs and maps from userspace, for example to show, dump, load, disassemble, pin programs, or to show, create, pin, update, delete maps, or to attach and detach programs to cgroups.
  - [`bpf_asm`](https://git.kernel.org/pub/scm/linux/kernel/git/bpf/bpf-next.git/tree/tools/bpf/bpf_asm.c) - A minimal cBPF assembler.
  - [`bpf_dbg`](https://git.kernel.org/pub/scm/linux/kernel/git/bpf/bpf-next.git/tree/tools/bpf/bpf_dbg.c) - A small debugger for cBPF programs.
  - [`bpf_jit_disasm`](https://git.kernel.org/pub/scm/linux/kernel/git/bpf/bpf-next.git/tree/tools/bpf/bpf_jit_disasm.c) - A disassembler for both BPF flavors and could be highly useful for JIT debugging.

### User Space eBPF

- [uBPF](https://github.com/iovisor/ubpf/) - Written in C. Contains an interpreter, a JIT compiler for x86_64 architecture, an assembler and a disassembler.
- [A generic implementation](https://github.com/YutaroHayakawa/generic-ebpf) - With support for FreeBSD kernel, FreeBSD user space, Linux kernel, Linux user space and macOS user space. Used for the [VALE software switch](https://www.unix.com/man-page/freebsd/4/vale/)'s [BPF extension module](https://github.com/YutaroHayakawa/vale-bpf).
- [rbpf](https://github.com/qmonnet/rbpf) - Written in Rust. Interpreter for Linux, macOS and Windows, and JIT-compiler for x86_64 under Linux.
- [PREVAIL](https://github.com/vbpf/ebpf-verifier) - A user space verifier for eBPF [using an abstract interpretation layer](https://elazarg.github.io/pldi19main-final.pdf), with support for loops.
- [oster](https://github.com/grantseltzer/oster) - Written in Go. A tool for tracing execution of Go programs by attaching eBPF to uprobes.
- [wachy](https://rubrikinc.github.io/wachy/) - A tracing profiler that aims to make eBPF uprobe-based debugging easier to use. This is done by displaying traces in a UI next to the source code and allowing interactive drilldown analysis.

### eBPF on Other Platforms

- [eBPF for Windows](https://github.com/microsoft/ebpf-for-windows) - This project is a work-in-progress that allows using existing eBPF toolchains and APIs familiar in the Linux ecosystem to be used on top of Windows.

### Testing in Virtual Environments

- [A Vagrant setup](https://github.com/iovisor/xdp-vagrant) - To easily test XDP. Less useful now that generic XDP (driver-independant, mostly for testing) exists.
- [bcc in a Docker container](https://github.com/zlim/bcc-docker)

## Projects Related to eBPF

### Networking

- P4 has some interactions with eBPF:

  - [P4 on the Edge](https://schd.ws/hosted_files/2016p4workshop/1d/Intel%20Fastabend-P4%20on%20the%20Edge.pdf) - P4 with eBPF to create high-performance programmable switches.
  - [OvS Orbit episode (#11), called P4 on the Edge](https://ovsorbit.org/#e11) - Related to the former item. Audio interview of John Fastabend by Ben Pfaff, one of the core maintainers of Open vSwitch.
  - [P4, EBPF and Linux TC Offload](https://open-nfp.org/m/documents/Open_NFP_P4_EBPF_Linux_TC_Offload_FINAL_5JHLETS.pdf) - P4 with some elements related to eBPF hardware offload on Netronome's NFP (Network Flow Processor) architecture.
  - [Old documentation for P4 usage with eBPF](https://github.com/iovisor/bcc/tree/master/src/cc/frontends/p4) - From bcc repository; deprecated by the P4_16 backend linked below.
  - [P4_16 backend for eBPF](https://github.com/p4lang/p4c/blob/master/backends/ebpf/README.md)

- [Cilium](https://cilium.io/) project ([GitHub repository](https://github.com/cilium/cilium)) is a technology relying on BPF and XDP to provide "fast in-kernel networking and security policy enforcement for containers based on eBPF programs generated on the fly". Many presentations available (with overlap):

  - [Cilium: Networking & Security for Containers with BPF & XDP](http://www.slideshare.net/ThomasGraf5/clium-container-networking-with-bpf-xdp) - Also featuring a load balancer use case
  - [Cilium: Networking & Security for Containers with BPF & XDP](http://www.slideshare.net/Docker/cilium-bpf-xdp-for-containers-66969823) - [video](https://www.youtube.com/watch?v=TnJF7ht3ZYc&list=PLkA60AVN3hh8oPas3cq2VA9xB7WazcIgs)
  - [Cilium: Fast IPv6 container Networking with BPF and XDP](http://www.slideshare.net/ThomasGraf5/cilium-fast-ipv6-container-networking-with-bpf-and-xdp)
  - [Cilium: BPF & XDP for containers](https://fosdem.org/2017/schedule/event/cilium/)
  - [OvS Orbit episode (#4)](https://ovsorbit.benpfaff.org/) - Interview of Thomas Graf by Ben Pfaff.
  - [A generic introduction to Cilium](https://opensource.googleblog.com/2016/11/cilium-networking-and-security.html)
  - [A podcast interviewing Thomas Graf](http://blog.ipspace.net/2016/10/fast-linux-packet-forwarding-with.html) - Ivan Pepelnjak interviewing Thomas, October 2016, on eBPF, P4, XDP and Cilium.

- Open vSwitch (OvS), and its related project Open Virtual Network (OVN, an open source network virtualization solution) are considering using eBPF at various level:

  - [Offloading OVS Flow Processing using eBPF](http://openvswitch.org/support/ovscon2016/7/1120-tu.pdf)
  - [Coupling the Flexibility of OVN with the Efficiency of IOVisor](http://openvswitch.org/support/ovscon2016/7/1245-bertrone.pdf)

- [Katran](https://code.fb.com/open-source/open-sourcing-katran-a-scalable-network-load-balancer/) - A layer 4 load-balancer based on XDP, open-sourced by Facebook.
- [XDP in practice: integrating XDP in our DDoS mitigation pipeline](http://netdevconf.org/2.1/session.html?bertin) - Protection against DDoS with XDP at Cloudflare.
- [Droplet: DDoS countermeasures powered by BPF + XDP](http://netdevconf.org/2.1/session.html?zhou) - Protection against DDoS with XDP at Facebook.
- [DPDK has a poll-mode driver (PMD) based on AF_XDP](https://dpdkuserspace2018.sched.com/event/G45Z/dpdk-pmd-for-afxdp)
- [CETH for XDP](http://www.slideshare.net/IOVisor/ceth-for-xdp-linux-meetup-santa-clara-july-2016) - Common Ethernet Driver Framework for faster network I/O, a technology initiated by Mellanox.
- Suricata, an open source intrusion detection system, [relies on eBPF components](https://www.stamus-networks.com/2016/09/28/suricata-bypass-feature/) for its "capture bypass" features:

  - ["eBPF and XDP" section of Suricata documentation](http://suricata.readthedocs.io/en/latest/capture-hardware/ebpf-xdp.html?highlight=XDP#ebpf-and-xdp)
  - [SEPTun-Mark-II](https://github.com/pevma/SEPTun-Mark-II) - Extreme Performance Tuning guide - Mark II.
  - [A blog post introducing the feature](https://www.stamus-networks.com/2016/09/28/suricata-bypass-feature/)
  - [The adventures of a Suricate in eBPF land](http://netdevconf.org/1.2/slides/oct6/10_suricata_ebpf.pdf)
  - [eBPF and XDP seen from the eyes of a meerkat](https://www.slideshare.net/ennael/kernel-recipes-2017-ebpf-and-xdp-eric-leblond)

- [Project Calico](https://projectcalico.docs.tigera.io/about/about-calico) - Calico is an open source networking and network security solution for containers, virtual machines, and native host-based workloads. Calico's eBPF data plane delivers a low latency, high throughput data plane with a rich network security policy model.
  - [Enabling eBPF data plane with Calico](https://projectcalico.docs.tigera.io/maintenance/ebpf/enabling-bpf)
- [merbridge](https://github.com/merbridge/merbridge/) - Use eBPF to speed up your Service Mesh. Merbridge replaces iptables rules with eBPF to intercept traffic. It also combines msg_redirect to reduce latency with a shortened datapath between sidecars and services.
- [PcapPlusPlus](https://pcapplusplus.github.io/) - An open-source C++ library for capturing, parsing and crafting network packets. It features a C++ interface for creating AF_XDP sockets, making it easy to [send and receive packets through them](https://pcapplusplus.github.io/docs/next/features#af_xdp-support-beta).

### Observability

- [InKeV: In-Kernel Distributed Network Virtualization for DCN](https://github.com/iovisor/bpf-docs/blob/master/university/sigcomm-ccr-InKev-2016.pdf)
- [DEEP-mon](https://www.slideshare.net/necstlab/deepmon-dynamic-and-energy-efficient-power-monitoring-for-containerbased-infrastructures) - Helps with measuring power consumption for servers and uses eBPF programs for in-kernel aggregation of data.
- [pixie](https://github.com/pixie-io/pixie) - Observability for Kubernetes using eBPF. Features include protocol tracing, application profiling, and support for distributed bpftrace deployments.
- [SkyWalking Rover](https://github.com/apache/skywalking-rover) - [Apache SkyWalking](https://skywalking.apache.org/) is an open-source Application Performance Monitoring (APM) platform specially designed for distributed systems with microservices, cloud-native and container-based (Kubernetes) architectures. SkyWalking Rover is an eBPF-based profiler and metrics collector for C, C++, Golang, and Rust applications.
- [parca-agent](https://github.com/parca-dev/parca-agent) - eBPF based always-on continuous profiler for analysis of CPU and memory usage, down to the line number and throughout time.
- [rbperf](https://github.com/javierhonduco/rbperf) - Sampling profiler and tracer for Ruby.
- [Hubble](https://github.com/cilium/hubble) - Network, service and security observability for Kubernetes using eBPF.
- [Caretta](https://github.com/groundcover-com/caretta) - Instant Kubernetes service dependency map generated by eBPF, right to a Grafana instance.
- [DeepFlow](https://github.com/deepflowio/deepflow) - Instant observability for cloud-native and AI applications based on eBPF.
- [Coroot](https://github.com/coroot/coroot) - Coroot is an open-source APM & Observability tool, a DataDog and NewRelic alternative.

### Security

- [Falco](https://falco.org/) - A cloud-native runtime security project used as a Kubernetes threat detection engine.
- [Sysmon for Linux](https://github.com/Sysinternals/SysmonForLinux) - A security monitoring tool. It depends on [SysinternalsEBPF](https://github.com/Sysinternals/SysinternalsEBPF).
- [Red Canary Linux Agent](https://redcanary.com/blog/ebpf-for-security) - Red Canary has started to incorporate eBPF to their Linux security sensor.
- [Tracee](https://github.com/aquasecurity/tracee) - A runtime security and forensics tool for Linux which uses eBPF technology to trace the system and applications at runtime, and analyze collected events to detect suspicious behavioral patterns.
- [redcanary-ebpf-sensor](https://github.com/redcanaryco/redcanary-ebpf-sensor) - A set of BPF programs that gather security relevant event data from the Linux kernel. The BPF programs are combined into a single ELF file from which individual probes can be selectively loaded, depending on the running operating system and kernel version.
- [bpflock - Lock Linux machines](https://github.com/linux-lock/bpflock) - An eBPF driven security tool for locking and auditing Linux machines.
- [Tetragon](https://github.com/cilium/tetragon) - Kubernetes-aware, eBPF-based security observability and runtime enforcement.
- [harpoon](https://github.com/alegrey91/harpoon) - Trace syscalls from user-space functions, by using eBPF.

### Tools

- [ply](https://wkz.github.io/ply/) - A small but flexible open source dynamic tracer for Linux, with features similar to the bcc tools, but with a simpler language inspired by awk and DTrace.
- [bpftrace](https://bpftrace.org/) - A tool for tracing with its own high-level tracing language. It is flexible enough to be envisioned as a Linux replacement for DTrace and SystemTap.
  - [bpftrace Cheat Sheet](https://www.brendangregg.com/BPF/bpftrace-cheat-sheet.html) - Summary and cheat sheet for programming in bpftrace. Contains information about syntax, probe types, variables and functions.
- [kubectl trace](https://github.com/iovisor/kubectl-trace) - A kubectl plug-in for executing bpftrace programs in a Kubernetes cluster.
- [inspektor-gadget](https://inspektor-gadget.io) - A collection tools and framework for data collection and system inspection on Kubernetes clusters and Linux hosts using eBPF.
- [bpfd](https://github.com/genuinetools/bpfd) - Framework for running BPF programs with rules on Linux as a daemon. Container aware.
- [BPFd](https://github.com/joelagnel/bpfd) - A distinct BPF daemon, trying to leverage the flexibility of the bcc tools to trace and debug remote targets, and in particular devices running with Android.
- [adeb](https://github.com/joelagnel/adeb) - A Linux shell environment for using tracing tools on Android with BPFd.
- [greggd](https://github.com/olcf/greggd) - System daemon to compile and load eBPF programs into the kernel, and forward program output to socket for metric aggregation.
- [FUSE](https://events.linuxfoundation.org/wp-content/uploads/2017/11/When-eBPF-Meets-FUSE-Improving-Performance-of-User-File-Systems-Ashish-Bijlani-Georgia-Tech.pdf) - Considers using eBPF.
- [upf-bpf](https://github.com/navarrothiago/upf-bpf) - An in-kernel solution based on XDP for 5G UPF.
- [redbpf](https://github.com/foniod/redbpf) - Tooling and framework to write eBPF code in Rust efficiently.
- [ebpf-explorer](https://github.com/ebpfdev/explorer) - A web interface to explore system's maps and programs.
- [ebpfmon](https://github.com/redcanaryco/ebpfmon) - A TUI (terminal user interface) application for real time monitoring of eBPF programs.
- [bpfman](https://github.com/bpfman/bpfman) - An eBPF Manager for Linux and Kubernetes. Includes a built-in program loader that supports program cooperation for XDP and TC programs, as well as deployment of eBPF programs from OCI images.
- [ptcpdump](https://github.com/mozillazg/ptcpdump) - A process-aware, eBPF-based tcpdump-like tool.

# eBPF in Security

- [Embrace The Red: Offensive BPF!](https://embracethered.com/blog/tags/ebpf) - A series of posts around the introduction into BPF with a focus to an offensive setting, and also how its misuse can be detected. Posts include discussions on the rootkit capabilities of eBPF, or on which tracing type is needed for different use cases.
- [eBPF: Block Linux Fileless Payload "Malware" Execution with BPF LSM](https://djalal.opendz.org/post/ebpf-block-linux-fileless-payload-execution-with-bpf-lsm/) - Blog post about how BPF can help detection and blocking fileless malware.
- [Blackhat 2021: With Friends Like eBPF, Who Needs Enemies?](https://www.blackhat.com/us-21/briefings/schedule/#with-friends-like-ebpf-who-needs-enemies-23619) - Talk about an eBPF rootkit and how the capabilities of eBPF could be abused. The rootkit was also the object of a talk at Defcon, [eBPF, I thought we were friends !](https://defcon.org/html/defcon-29/dc-29-speakers.html#fournier).
- [ebpfkit](https://github.com/Gui774ume/ebpfkit) - A rootkit that leverages multiple eBPF features to implement offensive security techniques.
- [ebpfkit-monitor](https://github.com/Gui774ume/ebpfkit-monitor) - An utility to statically analyze eBPF bytecode or monitor suspicious eBPF activity at runtime. It was specifically designed to detect ebpfkit.
- [Bad BPF](https://github.com/pathtofile/bad-bpf) - A collection of malicious eBPF programs that make use of eBPF's ability to read and write user data in between the usermode program and the kernel.
- [TripleCross](https://github.com/h3xduck/TripleCross) - A Linux eBPF rootkit with a backdoor, C2, library injection, execution hijacking, persistence and stealth capabilities.

## The Code

- [linux/include/linux/bpf.h](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/include/linux/bpf.h) - with [linux/include/uapi/bpf.h](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/include/uapi/linux/bpf.h): definitions related to eBPF, to be used respectively in the kernel and to interface with userspace programs.
- [linux/include/linux/filter.h](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/include/linux/filter.h) - with [linux/include/uapi/filter.h](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/include/uapi/linux/filter.h): information used to run the BPF programs themselves.
- [linux/kernel/bpf/](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/bpf) - This directory contains most of BPF-related code. In particular, those files are worth of interest:

  - [`syscall.c`](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/kernel/bpf/syscall.c) - Different operations permitted by the system call, such as program loading or map management.
  - [`core.c`](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/kernel/bpf/core.c) - BPF interpreter.
  - [`verifier.c`](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/kernel/bpf/verifier.c) - BPF verifier.

- [linux/net/core/filter.c](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/core/filter.c) - Functions and eBPF helpers related to networking (TC, XDP etc.); also contains the code to migrate cBPF bytecode to eBPF (all cBPF programs are translated to eBPF in recent kernels).
- [linux/kernel/trace/bpf_trace.c](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/trace/bpf_trace.c) - Functions and eBPF helpers related to tracing and monitoring (kprobes, tracepoints, etc.).
- The JIT compilers are under the directory of their respective architectures, such as file [linux/arch/x86/net/bpf_jit_comp.c](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/arch/x86/net/bpf_jit_comp.c) for x86\. Exception is made for JIT compilers used for hardware offload, sitting in their drivers, such as [linux/drivers/net/ethernet/netronome/nfp/bpf/jit.c](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/drivers/net/ethernet/netronome/nfp/bpf/jit.c) for Netronome NFP.
- [linux/net/sched/](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/sched) - and in particular in files `act_bpf.c` (action) and `cls_bpf.c` (filter): code related to BPF actions and filters with TC.
- [linux/kernel/seccomp.c](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/seccomp.c)
- [linux/net/core/dev.c](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/core/dev.c) - contains the function `dev_change_xdp_fd()` that is called through a Netlink command to hook a XDP program to a device, after is has been loaded into the kernel from user space. This function in turns uses a callback from the relevant driver.

## Development and Community

- [The bpf-next tree](https://git.kernel.org/pub/scm/linux/kernel/git/bpf/bpf-next.git/) - BPF patches land in this tree. It is regularly merged into [net-next](https://git.kernel.org/pub/scm/linux/kernel/git/davem/net-next.git), which is itself merged for each release to Linus' tree.
- [Kernel documentation](https://git.kernel.org/pub/scm/linux/kernel/git/davem/net-next.git/tree/Documentation/bpf/bpf_devel_QA.rst) - About contributions to BPF.
- [The netdev mailing list](http://lists.openwall.net/netdev/) - Mailing list for Linux kernel networking stack development. All patches are sent there for review and inclusion.
- [XDP-newbies](http://vger.kernel.org/vger-lists.html#xdp-newbies) - A mailing list specially dedicated to XDP programming (both for architecture or for asking for help).
- [IO Visor mailing list](http://lists.iovisor.org/pipermail/iovisor-dev/) - BPF is at the heart of the project, and is regularly discussed on the mailing list.
- [@IOVisor Twitter account](https://twitter.com/IOVisor)
- [The XDP Collaboration Project](https://github.com/xdp-project/xdp-project) - A GitHub repository with notes and ideas regarding the future evolutions of XDP.

## Other Lists of Resources on eBPF

- [IO Visor's bcc documentation](https://github.com/iovisor/bcc/tree/master/docs)
- [IO Visor's bpf-docs repository](https://github.com/iovisor/bpf-docs/)
- [Dive into BPF: A List of Reading Material](https://qmonnet.github.io/whirl-offload/2016/09/01/dive-into-bpf/)

## Acknowledgement

Thank you to Quentin Monnet and Daniel Borkmann for their original work on [Dive into BPF: A List of Reading Material](https://qmonnet.github.io/whirl-offload/2016/09/01/dive-into-bpf/) which became the basis for this list.

## Contributing

Contributions welcome! Read the [contribution guidelines](contributing.md) first.

## License

[![CC0](http://mirrors.creativecommons.org/presskit/buttons/88x31/svg/cc-zero.svg)](http://creativecommons.org/publicdomain/zero/1.0)

To the extent possible under law, zoidbergwill has waived all copyright and related or neighboring rights to this work.
