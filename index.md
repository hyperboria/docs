# Hyperboria

## The privacy-friendly network without borders

We're a community of local Wifi initiatives, programmers, and enthusiasts.
We run a peer-to-peer IPv6 network with automatic end-to-end encryption,
distributed IP address allocation, and DHT-based Source Routing.

- Existing applications Just Work
- Low entry barriers for users and ISPs
- Runs on Linux, Android, OpenWrt, OS X, and many others

Hyperboria is based on the cjdns routing protocol.

You can contribute to its documentaion: https://github.com/hyperboria/docs


## About Hyperboria

- [Asking Questions](wtfm.html) *TODO*
- [Peering](faq/peering.html)
- [Security](faq/security.html)
- [Meshlocals](meshlocals/intro.html)
  - [Meshlocals around the world](meshlocals/existing/index.html)
  - [Starting a Meshlocal](meshlocals/diy.html)
- [FAQ](faq/general.html)
- [Achievements](achievements.html)
- [Glossary](faq/glossary.html)


## The cjdns routing protocol

- About
  - [Goals](project-goals.html) ([russian](project-goals-ru.html))
  - [Original whitepaper](Whitepaper.html)
  - [Brief intro](intro.html)
  - [Security Specification](security-specifications.html)
- Installation
  - [Most Linuxes](install/linux.html) *TODO*
  - [OpenWrt](install/openwrt.html)
  - [Android](install/android.html) *TODO*
  - [Firefox OS](install/firefoxos.html) *TODO*
  - [OS X](install/osx.html)
  - [Debian Wheezy](install/debian-wheezy.html)
  - [Debian Jessie](install/debian-jessie.html)
  - [Arch](install/arch.html)
  - [Fedora](install/fedora.html)
  - [FreeBSD](install/freebsd.html) *TODO*
  - [OpenBSD](install/openbsd.html) *TODO*
  - [Windows](install/windows.html)
    - [Building *on* Windows](install/build-on-windows.html)
    - [Securing your Windows system](config/windows-firewall.html)
- Usage
  - [Setup](config/configure.html)
  - [Operator guidelines](cjdns/operator-guidelines.html)
  - [Securing your system](config/network-services.html)
  - [Tools](tools/index.html) *TODO*
    - [Third party tools](ctrls.html)
  - [Admin API](cjdns/admin-api.html)
- Working with cjdns
  - [Anatomy of cjdroute](cjdns/anatomy.html)
  - [Peering over UDP](cjdns/peering-over-UDP-IP.html)
  - [nodeinfo.json](cjdns/nodeinfo-json.html)
  - [Changelog](cjdns/changelog.html)
- HowTo
  - [Using cjdns as a VPN](config/tunnel.html)
  - [Shorewall and VPN gateway](config/shorewall-and-vpn-gateway-howto.html)
  - [NAT gateway for non-cjdns nodes](config/nat-gateway.html)
  - [Autostart at login](config/autostart-at-login.html)
  - [Run as non-root user](config/non-root-user.html)
- Troubleshooting
  - [Read this first](bugs/policy.html)
  - [Memory leaks](bugs/debugging-memory-leaks.html)
  - [SecComp](bugs/Seccomp.html)
  - [Analyzing network IO](traffic-analysis.html)
  - Known issues
    - [Horizon](bugs/horizon.html)
    - [Black Hole](bugs/black-hole.html)
    - [Secret Santa](bugs/santa.html)
    - Configurator timeout
      - [Firewall on localhost](bugs/configurator-timeout.html)
      - [UDP overflow](bugs/connectTo-overflow.html)
    - ~~[Hidden Peers](bugs/hidden-peers.html)~~
    - [OS/distro-specific quirks](bugs/distro-quirks.html)
  - [Reporting bugs](bugs/reporting.html)


## Random notes, work-in-progress, inbox

These notes are unstructured, and most of them likely outdated.

* [Interesting links](notes/links.html)
* [ansuz' Q&A with Arceliar](notes/arc-workings.html)
* [cjdns-core](notes/cjdns-core.html)
* [cryptography](notes/cryptography.html)
* [cjdroute.conf](notes/cjdroute-conf.html)
* [./do](notes/do.html)
* [DNS ideas](notes/dns.html)
* [DJC layer model](djc-layer-model.html)
* [Benchmarks](benchmark.txt)
* [Fun with the switch](switchfun.txt)

More of this in `notes/`.
