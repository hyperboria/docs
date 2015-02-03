# Changelog for cjdns

crashey is for development, master is rolling release

A few words about Version.h

## v15 -- January 2015

crashey since: 74e7b71 - Configurator should attempt a ping before beginning to setup the core (might fix startup errors for some people) (Fri Jan 23 23:45:04 2015 +0100)
master since: 97161a5 - shitfuck missed a line (Thu Jan 29 19:25:39 2015 +0100)

- Changes

## v14 -- January 2015

crashey since: 670b047 - Fixed bug in getPeers which caused it to return the same peers every time (Sun Jan 18 17:13:53 2015 +0100)
master since: 601b6cd - Oops, lets bump the version while we're at it (Fri Jan 23 07:47:05 2015 +0100)

- Changes

## v13 -- January 2015

crashey since: bb06b63 - Added 2 new command line tools, traceroute and cjdnslog (Thu Jan 1 17:10:39 2015 +0100)
master since: 185fe28 - Nodes trying to ping themselves causing crashes (Fri Jan 2 09:37:32 2015 +0100)

- Changes that haven't been documented yet
- Nodes running v11 or below are not supported any longer. They can still
  establish peering to every other node (also v13), but from v13 on, their
  traffic won't be switched any longer. They also won't make it into v13 nodes'
  routing tables.
- The ETHInterface wire protocol now includes the payload length. A few ethernet
  adapters don't strip the checksum which is appended to the packet by the
  sender, and thus confuse the decrypter.
- NodeStore_getBest() no longer takes DHT k-buckets into accounts -- the
  respective code has been commented out. From the code comments:

> The network is small enough that a per-bucket lookup is inefficient
> Basically, the first bucket is likely to route through an "edge" node
> In theory, it scales better if the network is large.

- The Admin API function `InterfaceController_peerStats()` doesn't require
  authentication any longer.
