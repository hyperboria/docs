Why?
====
If you're here from the hyperboria docs, you're already sold - proceed to Installing.  But why should a Fedora user install cjdns?  I'll mention just two contrasting use cases, one mundane and the other paranoid.

VPN Mesh
--------
Configuring a point to point VPN connection with openvpn is fairly straightforward, as
is configuring a centralized VPN server and clients.  However, when every
node in the VPN network needs to talk securely with many other nodes,
relaying every packet through the central server becomes a drag
on performance, and a single point of failure.  Mesh VPNs, like tinc and
cjdns automatically create point to point connections based on a shared
overall configuration.  Each node only needs a connection to one or more
peers (that can be reused) to get things started.  

With cjdns, however, things are
much better than with tinc.  On a local LAN or mesh with broadcast, it is zero
configuration.  Peers are automatically discovered via the 0xFC00 layer 2
protocol.  There is no shared configuration - the only thing required is adding
one or more (for redundancy) internet peers when no peers on the local LAN or mesh are available. 
Even better, when your node is mobile, and you have geographically separated peers configured,
cjdns automatically switches to a faster peer as the relative performance changes.

Darknet
-------
In a widespread VPN, address assignment must be coordinated by a central
authority.  The internet also uses centralized IP assignment, which
means a government can take away your IP at any time.  Cjdns uses
CryptoGraphic Addressing (CGA).  Your IP6 is the double SHA-512 of your public
key truncated to 128 bits.  Your IP is as safe as the private key pair
which produced it, and cannot [insert standard cryptography disclaimer] be
spoofed.  Most mesh VPNs decrypt packets before routing to a new node.  This means that if
a relay node is compromised in a conventional VPN, it can see and even alter packets.
All cjdns packets are end to end encrypted - relay nodes are untrusted.
There is no centralized routing.  If a node is "blackholing" packets
for some reason - a sender simply doesn't route through that node anymore.  (But see Security below.)

Installing CJDNS on Fedora and EPEL
===================================

Since Fedora 23, cjdns is in the Fedora repository.  It is in the testing repository until it gains sufficient positive karma.  To install:

```bash
sudo dnf install cjdns cjdns-tools cjdns-selinux --enablerepo=updates-testing
```

The cjdns-tools package has peerStats and other nodejs tools.  Python versions of the tools are in cjdns-python - although the ones conflicting with the nodejs tools are not symlinked to /bin.

The cjdns-selinux package has an selinux sandbox for cjdroute, to prevent it from doing anything wonky through accident or malice.  Some don't trust selinux (because of NSA origins), but it is installed by default on Fedora - so if you are running Fedora you want this.

For rhel6 and rhel7 with the EPEL repo, use the epel-testing repo instead of updates-testing.

Start cjdroute:

```bash
sudo systemctl enable cjdns #This sets cjdns to be started on boot. if you don't want that, feel free to leave this line out.
sudo systemctl start cjdns #This actually starts cjdroute.
````

For rhel6, use ```start cjdns``` instead of systemctl.  Add to /etc/rc.d/rc.local to enable on boot.

Checking the logs:
```bash
sudo systemctl status -l cjdns
```

Starting cjdroute for the first time will generate a new config file in ```/etc/cjdroute.conf```.  The default config will Just Work if there are any other cjdns nodes within reach of ethernet broadcast - for example on your local LAN or mesh.  Otherwise, you will need to add some internet peers as discussed elsewhere.  

After changing anything in the configuration, restart cjdns:

```bash
sudo systemctl restart cjdns
```

For rhel6, use ```restart cjdns``` instead of systemctl.

If you are on a laptop, you may find that after waking up from suspend or hibernate, cjdroute takes a minute or two to make coffee and figure out what just happened.  To speed this up, just restart cjdroute.  To always restart cjdroute upon awakening, enable the cjdns-resume service:

```bash
sudo systemctl enable cjdns-resume
```

For rhel6, ... wait, why would you run rhel6 on a laptop?

Security
--------
By default, Fedora Workstation will treat the tun device created by cjdroute as "public", with SSH being the only incoming port allowed.  There is no additional exposure with cjdns and the default Fedora firewall.  If you have modified the firewall config beyond opening additional incoming ports, be sure that the cjdns tun is treated as public - because anyone in the world can attempt to connect to you through it.  Sometimes, people configure their firewall to treat all tun devices as "VPN", and therefore somewhat more trusted.  This would be a mistake with cjdns.  It is a VPN, for sure, but one anyone in the world can join.

Public keys for cjdns are based on Elliptic Curves.  There is a known quantum algorithm that could be used to crack them if quantum computers with sufficient qubits are ever built.  The solution when that happens is larger keys - which are more cumbersome.

The Distributed Hash Table algorithm is a core component of cjdns - which is vulnerable to a Denial of Service attack known as "Sybil".  This attack can block specific updates to the DHT - to prevent your node from joining a mesh, for instance.

On the positive side, you can safely use telnet to cjdns IPs and the http protocol is automatically encrypted (but you need a secure DNS or raw ip to be sure you are talking to the right node).  Many other protocols are automatically encrypted while using cjdns.  In general, connecting to a raw cjdns IP is functionally equivalent to SSL/TLS with both client and server authentication.

Since the cjdroute core routing code parses network packets from untrusted sources, it is a security risk and is heavily sandboxed.  It runs as the cjdns user in a chroot jail in an empty directory, with RLIMIT_NPROC set to 1 to disable forking.  Seccomp is used to limit available system calls to only those actually needed.  Installing the cjdns-selinux package installs a targeted selinux policy that also restricts what the privileged process can access.

Advanced config
---------------
You may install a network service that depends on cjdns, for instance you might install thttpd to serve up 
[nodeinfo.json](https://docs.meshwith.me/en/cjdns/nodeinfo.json.html).  If thttpd is configured to listen only on your cjdns IP, then it will not start until cjdns is up and running.  Add ```After=cjdns-wait-online.service``` to ```thttpd.service``` to hold off starting the service until cjdns has the tunnel up and ready.

Feedback
--------
If you succeed, leave karma and feedback on https://bodhi.fedoraproject.org/updates/FEDORA-2016-8fb1a8db25 so that the package can move from testing to production.

Installing CJDNS on Fedora 22
=============================
(last tested on Fedora 22, those with fedora versions older than 22 should substitute yum for dnf.)

#Prerequisites
```bash
sudo dnf install git automake nodejs libseccomp-devel gcc 
```

#Getting cjdns
```bash
git clone https://github.com/hyperboria/cjdns
```

#Building cjdns
```bash
cd cjdns/
./do
```

#Generating a config
```bash
./cjdroute --genconf > cjdroute.conf
```

#Setting cjdns to autostart on boot.

First you'll want to edit contrib/systemd/cjdns.service to properly reflect where your cjdns binary and configuration are.
Then, run these commands:

```bash
sudo cp cjdns.service /etc/systemd/system/cjdns.service # This gives systemd some information about cjdns.
sudo systemctl enable cjdns.service #This sets cjdns to be started on boot. if you don't want that, feel free to leave this line out.
sudo systemctl start cjdns.service #This actually starts cjdns.
```

Checking the logs:
```bash
sudo systemctl status -l cjdns
```
