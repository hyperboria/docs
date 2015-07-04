Installing CJDNS on Fedora
==========================
(last tested on Fedora 22, those with fedora versions older than 22 should substitue yum for dnf.)

#Prerequisites
```
sudo dnf install git automake nodejs libseccomp-devel gcc 
```

#Getting cjdns
```
git clone https://github.com/hyperboria/cjdns
```

#Building cjdns
```
cd cjdns/
./do
```

#Generating a config
```
./cjdroute --genconf > cjdroute.conf
```

#Setting cjdns to autostart on boot.

First you'll want to edit contrib/systemd/cjdns.service to properly reflect where your cjdns binary and configuration are.
Then, run these commands:
```
sudo cp cjdns.service /etc/systemd/system/cjdns.service # This gives systemd some information about cjdns.
sudo systemctl enable cjdns.service #This sets cjdns to be started on boot. if you don't want that, feel free to leave this line out.
sudo systemctl start cjdns.service #This actually starts cjdns.
```

Checking the logs:
```
sudo systemctl status -l cjdns
```
