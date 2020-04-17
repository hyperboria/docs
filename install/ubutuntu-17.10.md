# Installing cjdns on Ubuntu 17.10

This is a short guide how to setup an Ubuntu cjdns box.

## Install packages

    apt-get install nodejs make gcc git python 2.7

## Clone, compile, install

```
cd /opt
git clone https://github.com/cjdelisle/cjdns.git
cd cjdns
./do
ln -s /opt/cjdns/cjdroute /usr/bin
umask 077 && sudo ./cjdroute --genconf | sudo tee /etc/cdjroute.conf
sudo cp contrib/systemd/*.service /etc/systemd/system/
systemctl enable cjdns
systemctl start cjdns
```
