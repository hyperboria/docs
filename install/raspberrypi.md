#Raspberry Pi Cjdns Install

##Debian Based
Works on Raspbian, OSMC, Kali ARM Raspberry pi

Your gonna need these packages: `
apt-get install nodejs build-essential git`

Next, grab the repository and build.

    cd /opt
    git clone https://github.com/cjdelisle/cjdns.git
    cd cjdns
    NO_TEST=1 Seccomp_NO=1 ./do`

The last line is due to a issue with SecComp on Raspbian Kernal seen here:
https://github.com/hyperboria/bugs/issues/6#issuecomment-162244016

After a little wait, the build should finish successfully. Now we want to configure cjdns to run as a daemon, so let’s create a link to the binary, generate a configuration file, and copy over the service file.

    ln -s /opt/cjdns/cjdroute /usr/bin
    (umask 077 && ./cjdroute --genconf > /etc/cjdroute.conf)
    cp contrib/systemd/cjdns.service /etc/systemd/system/

Now that we have that, we can configure it in `nano /etc/cjdroute.conf` and enable it for automatic start on boot.

    systemctl enable cjdns
    systemctl start cjdns
    
All Done!

##Arch Based

Install the package:

pacman -S cjdns

Then configure the file `nano /etc/cjdroute.conf`

Then Start/enable the cjdns.service.


    systemctl enable cjdns
    systemctl start cjdns
    
All Done!
