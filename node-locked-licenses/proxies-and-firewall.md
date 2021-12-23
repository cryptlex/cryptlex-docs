# Proxies and Firewall

## Proxies

LexActivator automatically detects the proxy settings of the machine. So, in most cases, you don't need to care whether your user is behind a proxy server or not.

To detect proxy settings, it uses standard methods available for each operating system. On Windows, it checks the system proxy settings, on macOS, it reads proxy settings from the system internet settings, and on Linux, it reads proxy settings from the environment variable `http_proxy`.

### Custom proxy settings

You can allow the user to set the proxy settings to be used by LexActivator. Simply use the following LexActivator API function:

```cpp
SetNetworkProxy("http://username:password@host:port/");
```

The proxy format should be:&#x20;

`[protocol://][username:password@]machine[:port]`

Following are some examples of the valid proxy strings:

* `http://127.0.0.1:8000/`
* `http://user:pass@127.0.0.1:8000/`
* `socks5://127.0.0.1:8000/`

## Firewall whitelisting

Whitelist Cryptlex IP addresses to enable LexActivator license and trial activations through the firewall.

### Access through firewall <a href="#access-through-firewall" id="access-through-firewall"></a>

If your customer's policy denies access from external IP addresses and websites, you will need to whitelist the IP addresses below. A whitelist provides access to designated IP addresses and sites that would otherwise be prevented by your security policy.

* `52.223.22.71`
* `35.71.188.31`

Alternatively, you can also whitelist Cryptlex Web API URL:

`https://api.cryptlex.com:443`
