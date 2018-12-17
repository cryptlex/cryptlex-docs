# LexFloatServer

LexFloatServer is the server software that leases floating license to your app which is installed on some computer \(which is referred to as a license server\) in your customer's local network. Normally, only one license server is required in your network.

LexFloatServer is designed to be robust, low memory and very fast. Hence, it can even be installed on any old machine connected to the local network.

{% hint style="info" %}
LexFloatServer has **libnss3** dependency on Linux. Make sure dependency is installed before running the server.
{% endhint %}

## Activating the LexFloatServer

LexFloatServer needs to be activated using a license key of type **"on-premise-floating"**, before it can be used. To activate use **"-a"** switch along with the license key and product file path:

```bash
LexFloatServer -a -licensekey=LICENSE_KEY -config="path/of/config" -productfile="path/of/myproduct.dat"
```

You can also pass other options. To check all the command line options use the **"-help"** switch.

{% hint style="info" %}
You need admin rights to run the LexFloatServer. 
{% endhint %}

## Configuring the LexFloatServer

LexFloatServer uses a simple key value based text file as it's config file. It is loaded at the start of the server. Any changes to the config file will be ignored until the server is restarted. Following is a sample file which would suffice for most of the cases:

```text
# Port LexFloatServer should bind to

port=8090

# Determines how long a license lease should last. The time is in seconds. 
# 15 minutes (900 seconds) is recommended. 30 seconds is minimum allowed time.

leaseduration=900

# Path of log file to write errors, warnings, and any other information

logfilepath=float_server.log

# The amount of information to be logged in the file. These are the possible levels:
# "0" - No log
# "1" - Only Errors
# "2" - Errors and Warnings
# "3" - Errors, Warnings and other info regarding when leases are created, removed, expired etc.

loglevel=3

# Blocked IP addresses
#blockedips=192.168.0.7,192.168.0.8

```

## Starting LexFloatServer in terminal

For testing purpose you can easily run the LexFloatServer in terminal \(command prompt\). To start the server simply pass the **"-s"** switch along with product and config file paths:

```bash
LexFloatServer -s -productfile="path/of/myproduct.dat" -config="path/of/config"
```

## Installing LexFloatServer on Windows

LexFloatServer runs as a service on Windows. To install it as a service after activating the license simply pass the **"-i"** switch along with product and config file paths:

```bash
LexFloatServer -i -productfile="path/of/myproduct.dat" -config="path/of/config"
```

{% hint style="info" %}
To set a custom display name in the Windows services use the **"-displayname"** switch.
{% endhint %}

After installation it is set to start with the computer and run silently in the background.

### Stop/Start LexFloatServer on Windows

To stop or start the server from command line , you need the "service name". If product id of your product is xxx then "service name" would be "LexFloatServer-xxx":

```text
sc stop LexFloatServer-xxx
sc start LexFloatServer-xxx
```

### Uninstalling LexFloatServer on Windows

To uninstall simply pass **"-d"** switch to deactivate the license and then **"-u"** switch to remove the service:

```text
LexFloatServer -d
LexFloatServer -u
```

## Installing LexFloatServer on MacOS

LexFloatServer runs as a launchd daemon on MacOS. To install it as a launchd daemon after activation simply pass the **"-i"** switch along with product and config file paths:

```bash
LexFloatServer -i -productfile="path/of/myproduct.dat" -config="path/of/config"
```

After installation it is set to start with the computer and run silently in the background.

### Stop/Start LexFloatServer on MacOS

To stop or start the server from command line , you need the "launchd daemon label". If product id of your product is xxx then "launchd daemon label" would be "com.lexfloatserver.xxx":

```bash
sudo launchctl stop com.lexfloatserver.xxx
sudo launchctl start com.lexfloatserver.xxx
```

### Uninstalling LexFloatServer on MacOS

To uninstall simply pass **"-d"** switch to deactivate and then **"-u"** switch to remove the daemon:

```bash
LexFloatServer -d
LexFloatServer -u
```

## Installing LexFloatServer on Linux

In Linux their are multiple ways of running daemons. A typical Linux distribution can use systemd or upstart or System V init etc. for running daemons. Some init methods expect your application to have daemon support built in, and others don't.

If your init method expects your process to self daemonize, then in your init script, you should execute LexFloatServer as:

```bash
LexFloatServer -b -silent
```

If your init method \(e.g. systemd\) expects your process not to self daemonize, then in your init script, you should execute LexFloatServer as:

```bash
LexFloatServer -s -silent
```

## Getting server stats

LexFloatServer exposes a stats API endpoint which can be used to get the current stats of the server.

{% api-method method="get" host="http://localhost:8090" path="/api/server/stats" %}
{% api-method-summary %}
Server stats
{% endapi-method-summary %}

{% api-method-description %}
Gets the current server stats
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "leaseDuration": 1800,
  "totalLicenses": 10,
  "availableLicenses": 5,
  "leasingStrategy": "per-machine",
  "version": "4.0.0",
  "status": "ok",
  "expiresAt": 1580732402
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

## Getting list of floating licenses

LexFloatServer exposes a floating-licenses API endpoint which can be used to get the leased floating licenses.

{% api-method method="get" host="http://localhost:8090" path="/api/floating-licenses" %}
{% api-method-summary %}
List of floating licenses
{% endapi-method-summary %}

{% api-method-description %}
Gets the current server stats
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
[
  {
    "id": "3a13465d984ef1f4b21b2117e0b3f591116f6b027fa8a19f332fbc43651f3d2c",
    "ip": "127.0.0.1",
    "os": "macos",
    "osVersion": "10.14",
    "hostname": "MB-Pro.local",
    "clientVersion": "4.0.0",
    "expiresAt": 1545019266,
    "updatedAt": 1545019236,
    "createdAt": 1545019236,
    "metadata": [
      {
        "key": "name",
        "value": "John Doe"
      }
    ]
  }
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

## 

