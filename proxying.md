Proxying
===========================

Sometimes you just can't set-up cjdns on your machine.
It might be because it is not yours machine or it is Windows (it is possible but who wants to mess with that).

The easiest way to browse Hyperboria's services then is to set-up a proxy.
This can be simply done using a SSH connection.

Creating SOCKSv5 connection
----------------------------

To create SOCKS SSH connection in Linux/OSX:
```
ssh -f -N -D 8080 [your_cjdns_capable_host]
```
This will connect to host under `[your_cjdns_capable_host]`.

This can be also achieved in PuTTY by creating a dynamic tunnel on port `8080`.

(The port `8080` can be any different port but you will have to edit PAC later to make it work)

Configuring your Web Browser
----------------------------

If you are on with porxying all of your traffic through the server then just select SOCKS5 proxy
and put `localhost` as hostname and `8080` as port.

If you want your normal traffic to travel directly and only cjdns host to connect though the proxy,
you have to use Proxy auto-config (PAC).

Following PAC file checks if host is given as IPv6 in cjdns space, if not trys to resolve it (if that fails
it usually means current DNS server is not IPv6 capable or domain is registered only in cjdns so
it redirects it into the cjdns) and last if resolve is successful (current host is IPv6 capable)
it checks whether the address is in cjdns space.
```js
function FindProxyForURL(url, host) {
    // If we can't resolve this means that this host is IPv4 only. Trying cjdns won't hurt.
    // It also make IPv4 only hosts connect ot clearnet IPv6 hosts if proxy is IPv6 capable.
    // If we can resolve check if the host is insice cjdns network space.
    if (shExpMatch(host, "fc*:*") || !dnsResolve(host) || shExpMatch(dnsResolve(host), "fc*:*")) {
        return "SOCKS5 localhost:8080";
    }
    return "DIRECT";
}
```
Also available as direct link: [cjdns.pac](https://gist.githubusercontent.com/Kubuxu/768735a1c39ce0f5ec03/raw/a8cf4baac722a45f9663a163492af6782884a155/cjsnds.pac)

This PAC file uses SOCKS5 connection with proxy server on `localhost` at port `8080`.
If you are using different port, you have to change it accordingly.

Use this PAC file for `Automatic proxy configuration` option which is available in most browsers.
