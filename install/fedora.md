Installing CJDNS on Fedora
==========================

Since Fedora 22, cjdns is in the Fedora repository.  To install the easy way:

```bash
sudo dnf install cjdns cjdns-tools cjdns-selinux
```
For rhel6 and rhel7 use:
```bash
yum install epel-release
yum install cjdns cjdns-tools cjdns-selinux
```

The `cjdns-tools` package has peerStats and other nodejs tools.  Python versions of the tools are in `cjdns-python` - although the ones conflicting with the nodejs tools are not symlinked to /bin.

The `cjdns-selinux` package has an selinux sandbox for cjdroute, to prevent it from doing anything wonky through accident or malice.  SELinux is enabled by default on Fedora and RHEL - so if you are running Fedora or RHEL/CentOS you'll usually want this.

Start cjdroute:

```bash
sudo systemctl enable cjdns #This sets cjdns to be started on boot. if you don't want that, feel free to leave this line out.
sudo systemctl start cjdns #This actually starts cjdroute.
```

For rhel6, use ```start cjdns``` instead of systemctl.  Add to /etc/rc.d/rc.local to enable on boot.

Checking the logs:
```bash
sudo systemctl status -l cjdns
```

Starting cjdroute for the first time will generate a new config file in ```/etc/cjdroute.conf```.  The default config will Just Work if there are any other cjdns nodes within reach of ethernet broadcast - for example on your local LAN or mesh.  Otherwise, you will need to [add some internet peers as discussed elsewhere.](../configure.md)  

After changing anything in the configuration, restart cjdns:

```bash
sudo systemctl restart cjdns
```

For rhel6, use ```restart cjdns``` instead of systemctl.

If you are on a laptop, you may find that after waking up from suspend or hibernate, cjdroute takes a minute or two to make coffee and figure out what just happened.  To speed this up, just restart cjdroute.  To always restart cjdroute upon awakening, enable the cjdns-resume service:

```bash
sudo systemctl enable cjdns-resume
```

# Installing CJDNS manually

## Prerequisites
```bash
sudo dnf install git automake nodejs libseccomp-devel gcc
```

## Getting cjdns
```bash
git clone https://github.com/hyperboria/cjdns
```

## Building cjdns
```bash
cd cjdns/
./do
```

## Generating a confighttps://github.com/hyperboria/docs
```bash
./cjdroute --genconf > cjdroute.conf
```

## Setting cjdns to autostart on boot.

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
