# LexFloatServer

LexFloatServer is the licensing server software that leases floating licenses to your app. It is usually installed on any computer in your customer's local network. In case you have multiple products, each product will require its own instance of LexFloatServer.

LexFloatServer is designed to be robust, low memory and very fast. Hence, it can even be installed on any old machine connected to the local network.

{% hint style="info" %}
LexFloatServer has [`VS2015 runtime`](https://www.microsoft.com/en-in/download/details.aspx?id=48145) dependency on Windows. Make sure dependency is installed before running the server.
{% endhint %}

## Downloading the LexFloatServer

LexFloatServer can be downloaded from the downloads page in the dashboard. Simply login to your Cryptlex account and download LexFloatServer binary for Windows, macOS or Linux:

* ​[Download LexFloatServer for Windows](https://app.cryptlex.com/downloads)​
* [​Download LexFloatServer for macOS](https://app.cryptlex.com/downloads)
* ​[Download LexFloatServer for Linux](https://app.cryptlex.com/downloads)​

## Configuring the LexFloatServer

LexFloatServer uses a simple YAML-based text file as its config file. It expects a `config.yml` file to be in the same directory as LexFloatServer. If the config file is in some other directory it can be passed using the **"-c"** option.

The config is loaded at the start of the server. Any changes to the config file will be ignored until the server is restarted.

## Starting LexFloatServer in terminal

For testing purposes, you can easily run the LexFloatServer in the terminal (command prompt). To start the server simply pass the **"-s"** option:

```bash
lexfloatserver -s
```

{% hint style="info" %}
You need admin rights to run the LexFloatServer.&#x20;
{% endhint %}

## Activating the LexFloatServer

LexFloatServer needs to be activated using a license key of type **"on-premise-floating"** before it can be used. It can be activated using the dashboard, command-line options or Web API.

### Using the Dashboard

LexFloatServer provides a web-based local dashboard that can be used to activate the server license.

#### Online activation

Open the dashboard using `http://localhost:8090` URL in your browser. Click the Settings page icon and put in the license key to activate the server

#### Offline activation

To activate offline click on the "SWITCH TO OFFLINE ACTIVATION" option on the Settings page. Put in the license key to generate the offline activation request file.

After generating the offline response from the Cryptlex admin dashboard for this request, paste the offline response file contents in the input to activate the server:

### Using command-line options

#### Online activation

To activate use **"-a"** option along with the license key and product file path (if not set in the config.yml file):

```bash
lexfloatserver -a --license-key LICENSE_KEY
```

#### Offline activation

To activate offline use **"-g"** option to generate the offline activation request:

```bash
lexfloatserver -g --license-key LICENSE_KEY --offline-request FILEPATH
```

After generating the offline response from the admin dashboard, pass it along with **"-a"** option to activate the server:

```
lexfloatserver -a --license-key=LICENSE_KEY --offline-response=FILEPATH
```

### Using Web API

LexFloatServer exposes a few API endpoints which can also be used to activate the server.

#### Online activation

Send a POST request to the **/api/server/activate** API endpoint with a JSON request body containing the license key and optionally the activation metadata.

{% swagger baseUrl="http://localhost:8090" path="/api/server/activate" method="post" summary="Activate server" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="licenseKey" type="string" %}
License key to activate the server.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="metadata" type="array" %}
Activation metadata.
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```javascript
{
  "message": "Server license activation successful!",
  "code": "SERVER_LICENSE_ACTIVATED"
}
```
{% endswagger-response %}

{% swagger-response status="400" description="" %}
```javascript
{
  "message": "Server license activation failed!",
  "code": "SERVER_INVALID_LICENSE_KEY"
}
```
{% endswagger-response %}
{% endswagger %}

#### Offline activation

Send a POST request to the **/api/server/offline-activation-request** API endpoint with a JSON request body containing the license key and optionally the activation metadata.

{% swagger baseUrl="http://localhost:8090" path="/api/server/offline-activation-request" method="post" summary="Generate offline activation request" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="licenseKey" type="string" %}
License key to activate the server.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="metadata" type="array" %}
Activation metadata.
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```javascript
{
  "offlineRequest": "U7l69tNy8..."
}
```
{% endswagger-response %}
{% endswagger %}

After generating the offline response from the admin dashboard, send a POST request to the **/api/server/offline-activate** API endpoint with a JSON request body containing the license key and the offline response.

{% swagger baseUrl="http://localhost:8090" path="/api/server/offline-activate" method="post" summary="Activate server offline" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="licenseKey" type="string" %}
License key to activate the server.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="offlineResponse" type="string" %}
Offline activation response.
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```javascript
{
  "message": "Server offline license activation successful!",
  "code": "SERVER_LICENSE_ACTIVATED"
}
```
{% endswagger-response %}

{% swagger-response status="400" description="" %}
```javascript
{
  "message": "Server offline license activation failed!",
  "code": "SERVER_INVALID_LICENSE_KEY"

```
{% endswagger-response %}
{% endswagger %}

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

## Getting server stats

LexFloatServer exposes a stats API endpoint that can be used to get the current stats of the server.

{% swagger baseUrl="http://localhost:8090" path="/api/server/stats" method="get" summary="Gets the server stats" %}
{% swagger-description %}
Gets the current server stats
{% endswagger-description %}

{% swagger-response status="200" description="" %}
```javascript
{
  "leaseDuration": 1800,
  "totalLicenses": 10,
  "availableLicenses": 5,
  "leasingStrategy": "per-machine",
  "version": "4.0.0",
  "status": "ok",
  "expiresAt": 1580732402,
  "serverSyncGracePeriodExpiryDate": 1580739313
}
```
{% endswagger-response %}
{% endswagger %}

## Getting server license info

LexFloatServer exposes a license info API endpoint that can be used to get the information related to the license used to activate the LexFloatServer.

{% swagger method="get" path="/api/server/license-info" baseUrl="http://localhost:8090" summary="Gets the license info" %}
{% swagger-description %}
Gets the license info of the license used to activate the LexFloatServer
{% endswagger-description %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
  "key": "280D2B-B48A03-406BBC-2EEE4A-C20FB3-749630",
  "allowedFloatingClients": 10,
  "createdAt": 1680518500,
  "activatedAt": 1680518506,
  "expiresAt": 1681814506,
  "serverSyncGracePeriodExpiresAt": 1680775357,
  "activationMode": {
    "initial": "online",
    "current": "online"
  },
  "user": {
    "name": "John Doe",
    "email": "johndoe@example.com",
    "company": "My Example Company"
  },
  "organization": null
}
```
{% endswagger-response %}
{% endswagger %}

## Getting the list of floating licenses

LexFloatServer exposes a floating-licenses API endpoint that can be used to get the leased floating licenses.

{% swagger baseUrl="http://localhost:8090" path="/api/floating-licenses" method="get" summary="Gets the list of floating licenses" %}
{% swagger-description %}
Gets the current server stats
{% endswagger-description %}

{% swagger-response status="200" description="" %}
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
{% endswagger-response %}
{% endswagger %}

## Getting server license meter attributes

LexFloatServer exposes a license meter attributes API endpoint that can be used to get the list of all the meter attributes of the license used to activate the LexFloatServer.

{% swagger method="get" path="/api/server/license-meter-attributes" baseUrl="http://localhost:8090" summary="Gets the list of license meter attributes" %}
{% swagger-description %}
Gets the list of meter attributes of the license used to activate the LexFloatServer
{% endswagger-description %}

{% swagger-response status="200: OK" description="" %}
<pre class="language-javascript"><code class="lang-javascript">[
  {
    "id": "string",
    "name": "string",
<strong>    "allowedUses": 0,
</strong>    "totalUses": 0,
    "grossUses": 0,  
  }
]
</code></pre>
{% endswagger-response %}
{% endswagger %}
