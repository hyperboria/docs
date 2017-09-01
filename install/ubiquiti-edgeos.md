# cjdns for Ubiquiti EdgeOS

The `vyatta-cjdns` package provides cjdns support on supported Ubiquiti EdgeMAX routers.  It is integrated with the command line interface (CLI) allowing cjdns to be configured through the standard EdgeOS configuration system.

It is maintained in a separate repository, please see [neilalexander/vyatta-cjdns](https://github.com/neilalexander/vyatta-cjdns) on GitHub for the source code (licenced under GPLv3), build scripts and tagged binary releases. 

Currently tested models:

|                       | Architecture | Binaries |                      Notes                           |
|-----------------------|:------------:|:--------:|:----------------------------------------------------:|
|    EdgeRouter X (ERX) |    mipsel    | [Download](https://github.com/neilalexander/vyatta-cjdns/releases/) | Builds on Debian Jessie with crossbuild-essential   |
| EdgeRouter Lite (ERL) |    mips64    | [Download](https://github.com/neilalexander/vyatta-cjdns/releases/) | Builds on Debian Jessie with Codescape SDK as mips32 |

