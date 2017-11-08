# awesome-ebpf [![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome)

> A curated list of awesome projects related to eBPF

## Contents

- [Learning Resources](#learning-resources)
- [Projects using eBPF](#projects-using-ebpf)
- [Blog Posts](#blog-posts)
- [Talks](#talks)
- [Zines](#zines)
- [Papers](#papers)

## Tools

- [bcc](https://github.com/iovisor/bcc): The BPF Compiler Collection's `/tools` directory has the most comprehensive list of scripts that use eBPF, and the repo also includes great references for learning and writing eBPF programs.
- [perf-tools](https://github.com/brendangregg/perf-tools): Most of the tools from `perf-tools`'s `/bin` directory has moved into the `bcc` repo, but there are some other useful sccripts especially for `uprobes` and `tracepoints`.
- [ply](https://github.com/iovisor/ply): The primary goal of `ply` is to simplify writing test eBPF programs before doing the scaffolding that using something like the BPF Python library requires.

## Learning Resources

- [Brendan Gregg's eBPF site](http://www.brendangregg.com/ebpf.html)
- [Cilium's eBPF and XDP Reference Guide](https://cilium.readthedocs.io/en/latest/bpf/)

## Projects using eBPF

- [Weaveworks' Scope](https://www.weave.works/oss/scope/): Tool for monitoring, visualisation & management for Docker & Kubernetes, that uses eBPF for visualising network traffic
  - [Scope's HTTP Code Statistics Plugin](https://github.com/weaveworks-plugins/scope-http-statistics)
- [Cilium](https://www.cilium.io/): Linux-native, HTTP-aware Network Security

## Blog Posts

- [How to filter packets super fast: XDP & eBPF! - Julia Evans](https://jvns.ca/blog/2017/04/07/xdp-bpf-tutorial/)
- [Notes on BPF & eBPF - Julia Evans](https://jvns.ca/blog/2017/06/28/notes-on-bpf---ebpf/)

## Talks

- [Cilium's Kernel Native Security & DDOS Mitigation for Microservices with BPF - Cynthia Thomas](https://dockercon.docker.com/watch/8RL2xBhXdhwz2NFCbVZzdF)
- [Cilium's Network and Application Security with BPF and XDP - Thomas Graf](https://www.youtube.com/watch?v=ilKlmTDdFgk)
- [Facebook's Droplet: DDoS countermeasures powered by BPF + XDP - Huapeng Zhou, Doug Porter, Ryan Tierney, Nikita Shirokov](https://netdevconf.org/2.1/session.html?zhou)
- [Give me 15 minutes and I'll change your view of Linux tracing - Brendan Gregg](https://www.youtube.com/watch?v=GsMs3n8CB6g)
- [Performance Analysis Superpowers with Linux eBPF - Brendan Gregg](https://www.youtube.com/watch?v=bj3qdEDbCD4)

## Zines

- [Linux Debugging Tools - Julia Evans](https://jvns.ca/debugging-zine.pdf)
- [Let's Learn tcpdump - Julia Evans](https://jvns.ca/tcpdump-zine.pdf)

## Papers

[The BSD Packet Filter: A New Architecture for User-level Packet Capture](http://www.vodun.org/papers/net-papers/van_jacobson_the_bpf_packet_filter.pdf)

## Contribute

Contributions welcome! Read the [contribution guidelines](contributing.md) first.


## License

[![CC0](http://mirrors.creativecommons.org/presskit/buttons/88x31/svg/cc-zero.svg)](http://creativecommons.org/publicdomain/zero/1.0)

To the extent possible under law, zoidbergwill has waived all copyright and
related or neighboring rights to this work.
