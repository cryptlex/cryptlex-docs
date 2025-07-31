# Installing LexFloatServer

## Installing LexFloatServer on Windows

LexFloatServer runs as a service on Windows. To install it as a service simply pass the **"-i"** option along with the service name and optionally a service display name which is displayed in the Windows Services Manager:

```bash
lexfloatserver -i --service-name myfloatingserver --service-display-name MyFloatingServer
```

After installation, it is set to start with the computer and run silently in the background.

### Stop/Start LexFloatServer on Windows

To stop or start the server from the command line you need the "service name". If the service name was not passed during installation then it defaults to `lexfloatserver-productId` (where product id is the id of your product):

```
sc stop myfloatingserver
sc start myfloatingserver
```

### Uninstalling LexFloatServer on Windows

To uninstall simply pass **"-d"** option to deactivate the server license and then **"-u"** option to remove the service:

```
lexfloatserver -d
lexfloatserver -u --service-name myfloatingserver
```

## Installing LexFloatServer on Linux

LexFloatServer can run as a Systemd, Upstart or SysV service on Linux. To install it as a service simply pass the **"-i"** option along with the service name:

```bash
lexfloatserver -i --service-name myfloatingserver
```

After installation, it is set to start with the computer and run silently in the background.

### Stop/Start LexFloatServer on Linux

To stop or start the server from the command line, you need the service name. If the service name was not passed during installation then it defaults to `lexfloatserver.productId` (where product id is the id of your product):

```bash
sudo service myfloatingserver stop
sudo service myfloatingserver start
```

### Uninstalling LexFloatServer on Linux

To uninstall simply pass **"-d"** option to deactivate and then **"-u"** option to remove the daemon:

```bash
lexfloatserver -d
lexfloatserver -u --service-name myfloatingserver
```

## Installing LexFloatServer on macOS

LexFloatServer runs as a launchd daemon on macOS. To install it as a service simply pass the **"-i"** option along with the service name:

```bash
lexfloatserver -i --service-name com.mycompany.myfloatingserver
```

After installation, it is set to start with the computer and run silently in the background.

### Stop/Start LexFloatServer on macOS

To stop or start the server from the command line, you need the service name. If the service name was not passed during installation then it defaults to `com.lexfloatserver.productId` (where product id is the id of your product):

```bash
sudo launchctl stop com.mycompany.myfloatingserver
sudo launchctl start com.mycompany.myfloatingserver
```

### Uninstalling LexFloatServer on macOS

To uninstall simply pass **"-d"** option to deactivate and then **"-u"** option to remove the daemon:

```bash
lexfloatserver -d
lexfloatserver -u --service-name com.mycompany.myfloatingserver
```
