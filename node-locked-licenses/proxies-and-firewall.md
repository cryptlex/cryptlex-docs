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

## **Firewall Whitelisting**

To enable LexActivator license and trial activations through your firewall, it's essential to whitelist Cryptlex IP addresses. This ensures smooth operation even if your customer's policy restricts access from external IP addresses and websites.

### **Access Through Firewall**

If the security policy at your customer's end denies access from external IP addresses and websites, you will need to whitelist specific IP addresses. A whitelist permits access to designated IP addresses and sites that would otherwise be blocked by your security policy.

#### **For Our US Data Center:**

* IP Addresses to Whitelist:
  * `52.223.22.71`
  * `35.71.188.31`
* Web API URL to Whitelist:
  * `https://api.cryptlex.com:443`

#### **For Our EU Data Center:**

For customers utilizing our EU data center, the following IP addresses and URL should be whitelisted:

* IP Addresses to Whitelist:
  * `75.2.113.112`
  * `99.83.149.57`
* Web API URL to Whitelist:
  * `https://api.eu.cryptlex.com:443`
