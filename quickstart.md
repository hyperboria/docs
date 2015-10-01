## Getting going with cjdns

### 1. what is it?

cjdns is the name of both the daemon and the network protocol that implements a secure, scalable and fast network with minimal configuration.

cjdns was born out of a need to solve inherent problems in the standard TCP/IP stack, like running out of addressable space and vulnerability to DDoS attacks.
It also implements end-to-end encryption out of the box, so any communication in a cjdns network is meddle-proof.

The cjdns project is currently in alpha, and a test network called Hyperboria with services like mail, social network and irc chat servers, exist with hundreds of nodes spread across the world.

### 2. how can you install it? 

Pick your OS and follow the instructions. Its not hard, but does involve some compiling.

* [Arch](install/arch.md)
* [Debian Jessie](install/debian-jessie.md)
* [Debian Wheezy](install/debian-wheezy.md)
* [Fedora](install/fedora.md)
* [OpenWRT](install/openwrt.md)
* [MacOSX](install/osx.md)
* [Windows(via cross-compiling)](install/windows.md)

### 3. generate a conf

Generate a configuration file with the write permissions by doing

    (umask 077 && ./cjdroute --genconf > cjdroute.conf)

**Warning:** skipping the umask part leaves your configuration file inssecure.
If someone steals your configuration, they can impersonate you.

**Note:** Backup your configuration file to somewhere safe locally to prevent
an embarassing loss of peer connectivity in case you delete the file by accident. 

### 4. Find a public peer

cjdns's network operates on a friend-of-a-friend model. This means, that to connect to 
the network you need to find nodes called peers which allow you to connect to the network.

But luckily, you don't have to go around hunting for peers just to get a taste of Hyperboria,
you can peer with public peers to get into the network right away.

To do that, first get on the [#cjdns](http://chat.efnet.org/irc.cgi?chan=%23cjdns) channel 
on the Efnet IRC Network

Once in the channel, type `? public` and you'll get links to public peers.

Follow any link and get to the peer info or "creds", which look something like this.

    "<ip-address:<port>":{
        "password":"<some-password>",
        "publicKey":"<some-key>.k",
        "user":"<username>",
        "contact":"<email>",
        "location":"<location>"
    }

Copy this info and paste it into the `cjdroute.conf` you generated. The peer info
goes into the "connectTo" section under the "UDPInterface" section.

Thats it, you're done! Fire up cjdns with

   sudo ./cjdroute < cjdroute.conf  

and its time to start testing things and getting involved

### 5. Now you should be on the net...

#### Testing whether you're connected

Open your browser and open [this link](http://h.cjdns.ca). If it works, then
congratulations! You just opened your first Hyperboria link. You can verify this
by killed the cjdns daemon and trying the link again.

If it didn't work, your problem could be one of the following

#### Troubleshooting

##### do you have a tun device?

First, check that your tunnel device exists and is working fine.

    cat /dev/net/tun

If it says: `cat: /dev/net/tun: File descriptor in bad state` Good!

If it says: `cat: /dev/net/tun: No such file or directory`, create it using:

    sudo mkdir -p /dev/net &&
    sudo mknod /dev/net/tun c 10 200 &&
    sudo chmod 0666 /dev/net/tun

Then `cat /dev/net/tun` again.

If it says: `cat: /dev/net/tun: Permission denied` and you're on MacOSX, Dont bother.

If you're probably using a VPS based on the OpenVZ virtualization platform. Ask your provider to enable the
TUN/TAP device - this is standard protocol so they should know exactly what you
need. 

##### is the network working? 

Open your terminal, go to the cjdns folder and do

    ./tools/peerStats

You should get something like

    v16.0000.0000.0000.0015.<some-key>.k ESTABLISHED in 1kb/s out 1kb/s  LOS 142

The ESTABLISHED state indicates a peer that is connected and working. If you don't get
this then the peer is probably down, and you'll need to connect to another peer.

if `peerStats` was successful, try pinging a server with

    ping6 h.cjdns.ca

If this works as well, then you probably have a browser issue.
If it doesn't, it indicates that something is wrong with the ipv6 setup of your OS.
Please check the OS docs and try to resolve the issue.

##### is your chrome/firefox working?

Browser support issues are mostly related to disabled or wrong ipv6 handling.
If Chrome doesn't work, try firefox, and vice-versa.

To get Chrome to support IPv6, you need to compile it with the --enable-ipv6 flag.

In Firefox, you'll need to make a few settings changes, navigate to [about:config](about:config)

    browser.fixup.alternate.enable to false
    network.dns.disableIPv6 to false

    * What if nothing works?

If nothing works, tell us whats wrong at [#cjdns](http://chat.efnet.org/irc.cgi?chan=%23cjdns)

Note that Hyperboria and cjdns is run by a group of volunteers so be patient with us if you don't 
get immediate responses

5. cool, now you're on
  + secure your device
  + get on hypeirc
  + find something to do
6. ???
7. Profit

:D


