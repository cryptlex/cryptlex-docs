# LexFloatServer

LexFloatServer is the server software that leases floating license to your app which is installed on some computer \(which is referred to as a license server\) in your customer's local network. Normally, only one license server is required in your network.

LexFloatServer is designed to be robust, low memory and very fast. Hence, it can even be installed on any old machine connected to the local network.

{% hint style="info" %}
LexFloatServer has **libnss3** dependency on Linux. Make sure dependency is installed before running the server.
{% endhint %}

## Activating the LexFloatServer

LexFloatServer needs to be activated using a license key of type **"on-premise-floating"**, before it can be used. To activate use **"-a"** switch along with the license key and product file path:

```bash
LexFloatServer -a -licensekey=LICENSE_KEY -productfile="path/of/myproduct.dat"
```

You can also pass other options. To check all the command line options use the **"-help"** switch.

{% hint style="info" %}
You need admin rights to run the LexFloatServer. 
{% endhint %}

## Configuring the LexFloatServer

LexFloatServer uses a simple key value based text file as it's config file. It is loaded at the start of the server. Any changes to the config file will be ignored until the server is restarted. Following is a sample file which would suffice for most of the cases:

```text

# Port LexFloat Server should bind to

port=8090

# Total threads the server should use. Ideally this should be 1 thread per CPU "core".
# LexFloat server will automatically detect number of cores, if you set this value to "0"

totalthreads=0

# Determines how long a license lease should last. The time is in seconds.
# 15 minutes (900 seconds) is recommended. 30 seconds is minimum allowed time.

leaselength=60

# Path of log file to write errors, warnings, and any other information

logfilepath=float_server.log

# The amount of information to be the logged file. These are the possible levels:
# "0" - No log
# "1" - Only Errors
# "2" - Errors and Warnings
# "3" - Errors, Warnings and other info regarding when leases are created, removed, expired etc.

loglevel=2

# Blocked IP addresses

#blockedips=192.168.0.7,192.168.0.8

```

## Installing LexFloatServer on Windows

LexFloatServer runs as a service on Windows. To install it as a service after activating the license simply pass the **"-i"** switch along with product and config file paths:

```text
LexFloatServer -i -productfile="path/of/myproduct.dat" -config="path/of/config/file"
```

{% hint style="info" %}
To set a custom display name in the Windows services use the **"-displayName"** switch.
{% endhint %}

After installation it is set to start with the computer and run silently in the background.

### Stop/Start LexFloatServer on Windows

To stop or start the server from command line , you need the "service name". If product id of your product is xxx then "service name" would be "LexFloatServer-xxx":

```text
sc stop LexFloatServer-xxx
sc start LexFloatServer-xxx
```

### Uninstalling LexFloatServer on Windows

To uninstall simply pass **"-d"** switch to deactivate the license and then** "-u"** switch to remove the service:

```text
LexFloatServer -d
LexFloatServer -u
```

## Installing LexFloatServer on MacOS

LexFloatServer runs as a launchd daemon on MacOS. To install it as a launchd daemon after activation simply pass the **"-i"** switch along with product and config file paths:

```text
LexFloatServer -i -productfile="path/of/myproduct.dat" -config="path/of/config/file"
```

After installation it is set to start with the computer and run silently in the background.

### Stop/Start LexFloatServer on MacOS

To stop or start the server from command line , you need the "launchd daemon label". If product id of your product is xxx then "launchd daemon label" would be "com.lexfloatserver.xxx":

```text
sudo launchctl stop com.lexfloatserver.xxx
sudo launchctl start com.lexfloatserver.xxx
```

### Uninstalling LexFloatServer on MacOS

To uninstall simply pass **"-d"** switch to deactivate and then **"-u"** switch to remove the daemon:

```text
LexFloatServer -d
LexFloatServer -u
```

## Installing LexFloatServer on Linux

In Linux their are multiple ways of running daemons. A typical Linux distribution can use systemd or upstart or System V init etc. for running daemons. Some init methods expect your application to have daemon support built in, and others don't.

If your init method expects your process to self daemonize, then in your init script, you should execute LexFloatServer as:

```text
LexFloatServer -b -silent
```

If your init method \(e.g. systemd\) expects your process not to self daemonize, then in your init script, you should execute LexFloatServer as:

```text
LexFloatServer -s -silent
```

## Getting server stats

LexFloatServer exposes a stats API endpoint which can be used to get the current stats of the server.

{% api-method method="get" host="http://localhost:8090" path="/api/stats" %}
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
  "availableLicenseActivations": 3,
  "totalLicenseActivations": 5,
  "expiresAt": 1580732402,
  "leaselength": 60,
  "version": "3.0.0",
  "activationStatus": "ok",
  "floatingClients": [
    {
      "ip": "192.168.1.2",
      "leaseRefreshedAt": 1480702402
    },
    {
      "ip": "192.168.1.7",
      "leaseRefreshedAt": 1480702428
    }
  ]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}



