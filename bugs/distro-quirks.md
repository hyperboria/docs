# OS/distribution-specific quirks

## OSX

### Failure to autopeer

```IRC
16:46 < ansuz> sounds like you guys are in srs mode, but that mac no-auto-peering thing only really has one line of documentation
16:46 < ansuz> at some point if someone could fill me in on the why, it would get more
16:47 <@cjd> ahh, it's because generating ethernet frames is different per operating system
16:47 <@cjd> there's no standardized socket(SO_LINK_LAYER, "eth0")
16:48 <@cjd> so ETHInterface_darwin.c just isn't written
16:49 <@cjd> now you can copy/paste that into a little txt file and when some poor bastard asks why, tell him and then shout at him to update the documentation
16:49 <@cjd> and if he doesn't, shitlist him so no more questions \:D/
16:49 <@Arceliar> or bug people who own a mac to write ETHInterface_darwin.c
```

There you have it, Macs don't autopeer via ethernet frames.

This is also probably why it doesn't work on windows, either.

## Raspbian

### Failure to start Cjdns
When running Cjdns on Raspberry Pi with Raspbian you can run in to problems because IPv6 is not enabled by default. This causes Cjdns to fail on startup with the following error message:

```
CRITICAL Configurator.c:107 Got error [UDPAddrIface.c:273 call to uv_udp_bind() failed [bad file descriptor]] calling [UDPInterface_new]
```

Enable IPv6 with

```bash
$ sudo modprobe ipv6
```

and Cjdns should start correctly. To keep IPv6 on after reboot add `ipv6` to the end of the file `/etc/modules`

```bash
$ sudo sh -c 'echo ipv6 >> /etc/modules'
```

## Windows

### Not resolving DNS correctly

Windows is having problems with resolving CNAME records referencing AAAA only records.

The fix is easy, you have to lie to windows saying that you have an existing IPv6 connection under your main network card.

To do so enter your main network card contex menu, select `Properties` and enter IPv6 configuration.
Select manual configuration and type `::1` as your IPv6 address, DNS fields can be empty as you don't have a IPv6 communication after all.
Click OK and after that CNAME records will be resolved correctly.

