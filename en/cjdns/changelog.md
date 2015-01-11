# Changelog for cjdns

## v13 -- January 2015

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
