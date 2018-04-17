# LexFloatServer

LexFloat Server is the server software that leases floating license to your app which is installed on some computer \(which is referred to as a license server\) in your customer's local network. Normally, only one license server is required in your network.

LexFloat Server is designed to be robust, low memory and very fast. Hence, it can even be installed on any old machine connected to the local network.

## Activating the LexFloat Server

LexFloat Server needs to be activated using a Float Server Key before it can be used. To activate use "-a" switch along with the product key:

```c
LexFloatServer -a -pkey=AAAAA-BBBBB-CCCCC-DDDDD-EEEEE
```

In case Product.dat is not present in the same directory as LexFloatServer, you can pass its location while activation. You can also pass extra activation data, proxy and other options:

```c
LexFloatServer -a -pkey=AAAAA-BBBBB-CCCCC-DDDDD-EEEEE -pfile="path/of/myproduct.dat" -extradata="Sample data"
```

**Note:**You need admin rights to run the LexFloat Server. To check all the command line options use the "-help" switch.

## Configuring the LexFloat Server

LexFloat Server uses a simple key value based text file as it's config file. It is loaded at the start of the server. Any changes to the config file will be ignored untill the server is restarted. Following is a sample file which would suffice for most of the cases:

```c
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

LexFloat Server runs as a launched daemon on Mac OS X. To install it as a launched daemon after activation simply pass the "-i" switch:

```c
LexFloatServer -i
```

In case Product.dat and LexFloat.config are not in the same directory as LexFloatServer, you can pass locations of both while installation:

```c
LexFloatServer -i -pfile="path/of/myproduct.dat" -config="path/of/config/file"
```

**Note:**To set a custom display name in the Windows services use the "-displayName" switch.

After installation it is set to start with the computer and run silently in the background.

### Stop/Start LexFloat Server on Windows

To stop or start the server from command line , you need the "service name". If version id of your product version is 1100 then "service name" would be "LexFloatServer-1100":

```c
sc stop LexFloatServer-1100
sc start LexFloatServer-1100
```

### Uninstalling LexFloat Server on Windows

To uninstall simply pass "-d" switch to deactivate and then "-u" switch to remove the service:

```c
LexFloatServer -d
LexFloatServer -u
```

### Installing LexFloat Server on Mac OS X

LexFloat Server runs as a launchd daemon on Mac OS X. To install it as a launchd daemon after activation simply pass the "-i" switch:

```text
LexFloatServer -i
```

After installation it is set to start with the computer and run silently in the background.

### Stop/Start LexFloat Server on Mac OS X

To stop or start the server from command line , you need the "launchd daemon label". If version id of your product version is 1100 then "launchd daemon label" would be "com.lexfloatserver.1100":

```c
sudo launchctl stop com.lexfloatserver.1100
sudo launchctl start com.lexfloatserver.1100
```

### Uninstalling LexFloat Server on Mac OS X

To uninstall simply pass "-d" switch to deactivate and then "-u" switch to remove the daemon:

```c
LexFloatServer -d
LexFloatServer -u
```

## Installing LexFloat Server on Linux

In Linux their are multiple ways of running daemons. A typical Linux distribution can use systemd or upstart or System V init etc. for running daemons. Some init methods expect your application to have daemon support built in, and others don't.

If your init method expects your process to self daemonize, then in your init script, you should execute LexFloatServer as:

```c
LexFloatServer -b -silent
```

If your init method \(e.g. systemd\) expects your process not to self daemonize, then in your init script, you should execute LexFloatServer as:

```c
LexFloatServer -s -silent
```

## Getting Server Stats

LexFloat Server exposes a stats API endpoint which can be used to get the current stats of the server.

```c
GET /services/api/stats

HTTP/1.1  200
Content-Type: application/json

{
  "availableLicenses": 8,
  "totalLicenses": 10,
  "daysLeftToExpiration": 243,
  "leaselength": 60,
  "version": "2.6.0",
  "status" : "ok",
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

