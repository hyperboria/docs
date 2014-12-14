# What does everything in your configuration file do?

If you've never worked with [JSON](http://en.wikipedia.org/wiki/JSON) before, you might feel a little overwhelmed editing your  **cjdroute.conf** for the first time.

One thing that makes matters more difficult is that your cjdroute.conf is **not** actually valid JSON.

This document will:

1. Indicate the exact purpose of each attribute of your configuration file.
2. Document the permitted and recommended syntax you can use, and the difference between the two.
3. Indicate which attributes are required, and which are optional.
4. Refer to related documentation about specific attributes, and the surrounding recomended practices.

## Structure

* privateKey
* publicKey
* ipv6
* authorizedPasswords
* admin
  + bind
  + password
* interfaces
  + UDPInterface
    + bind
    + connectTo
  + ETHInterface
    + bind
    + beacon
    + connectTo
* router
  + interface
    * type
  + ipTunnel
    * allowedConnections
      + publicKey
      + ip4Address
      + ip6Address
    * outgoingConnections
* resetAfterInactivitySeconds
* security
  + setuser
  + exemptAngel
* logging
  + logTo
* noBackground
* dns
  + keys
  + servers
  + minSignatures

## Functionality

### privateKey, publicKey, ipv6

As indicated in [this article on cjdns' cryptographic functions](cryptography.md), your ipv6 is derived from your publicKey, which is in turn derived from your privateKey.

**cjdroute --genconf** produces a sample configuration file which includes all three, but they are not all actually required to launch your router.

Instead, cjdns only uses your privateKey, then derives the rest. As such, the publicKey and ipv6 are only there for your benefit.
