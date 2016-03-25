Installing CJDNS on Fedora
==========================

Cjdns was added to the Fedora repository beginning with Fedora 23.  It is in the testing repository until it gains sufficient positive karma.  To install:

```bash
sudo dnf install cjdns cjdns-tools cjdns-selinux --enablerepo=updates-testing
```

The cjdns-tools package has peerStats and other nodejs tools.  Python versions of the tools are in cjdns-python - although the ones conflicting with the nodejs tools are not symlinked to /bin.

The cjdns-selinux package has an selinux sandbox for cjdroute, to prevent it from doing anything wonky through accident or malice.  Some don't trust selinux (because of NSA origins), but it is installed by default on Fedora - so if you are running Fedora you want this.

Start cjdroute:

```bash
sudo systemctl enable cjdns #This sets cjdns to be started on boot. if you don't want that, feel free to leave this line out.
sudo systemctl start cjdns #This actually starts cjdroute.
````

Checking the logs:
```bash
sudo systemctl status -l cjdns
```

Starting cjdroute for the first time will generate a new config file in ```/etc/cjdroute.conf```.  The default config will Just Work if there are any other cjdns nodes within reach of ethernet broadcast - for example on your local LAN or mesh.  Otherwise, you will need to add some internet peers as discussed elsewhere.  

After changing anything in the configuration, restart cjdns:

```bash
sudo systemctl restart cjdns
```

If you are on a laptop, you may find that after waking up from suspend or hibernate, cjdroute takes a minute or two to make coffee and figure out what just happened.  To speed this up, just restart cjdroute.  To always restart cjdroute upon awakening, enable the cjdns-resume service:

```bash
sudo systemctl enable cjdns-resume
```

Advanced config
---------------
You may install a network service that depends on cjdns, for instance you might install thttpd to serve up 
[nodeinfo.json](https://docs.meshwith.me/en/cjdns/nodeinfo.json.html).  If thttpd is configured to listen only on your cjdns IP, then it will not start until cjdns is up and running.  Add ```After=cjdns-wait-online.service``` to ```thttpd.service``` to hold off starting the service until cjdns has the tunnel up and ready.

Feedback During Testing
-----------------------
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
