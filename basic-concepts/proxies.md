## Proxies

LexActivator automatically detects the proxy settings of the machine. So, in most of the cases you don't need to care whether your user is behind a proxy server or not.

To detect proxy settings, it uses standard methods available for each operating system. On Windows it checks the proxy settings of Internet Explorer, on Mac OS X it reads proxy settings from the system internet settings and on Linux it reads proxy settings from the environment variable http\_proxy.



### Custom Proxy Settings

You can allow the user to set the proxy settings to be used by LexActivator. Simply use the following LexActivator API function:

```
SetNetworkProxy
(
"http://username:password@host:port/"
)
;
```

The proxy format should be:

```
[
protocol
:
/
/
]
[
username
:
password@
]
machine
[
:
port
]
```

Following are some examples of the valid proxy strings:

* http://127.0.0.1:8000/
* http://user:pass@127.0.0.1:8000/
* socks5://127.0.0.1:8000/



