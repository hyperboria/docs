A number of us have begun the task of documenting and reverse engineering the cjdns core.

To speak with those involved, join **HypeIRC/#documentation**

ansuz has re-implemented the [xor metric](https://github.com/ansuz/fc00.org/tree/master/scripts/xor) and [key generation process](https://github.com/ansuz/fc00.org/tree/master/scripts/keys), along with the support functions involved, notably the implementation of Base32 used by cjdns.

[jph](https://hackworth.be/) is experimenting with writing a minimal, linux first implementation in golang, along with deconstructing everything involved in making that happen. He is also investigating TUN support in other languages (notably Python and ocaml).
