# Activating the LexFloatServer

LexFloatServer needs to be activated using a license key of type **"on-premise-floating"** before it can be used. It can be activated using the dashboard, command-line options or Web API.

## Using the Dashboard

LexFloatServer provides a web-based local dashboard that can be used to activate the server license.

### Online activation

Open the dashboard using `http://localhost:8090` URL in your browser. Click the Settings page icon and put in the license key to activate the server

### Offline activation

To activate offline click on the "SWITCH TO OFFLINE ACTIVATION" option on the Settings page. Put in the license key to generate the offline activation request file.

After generating the offline response from the Cryptlex admin dashboard for this request, paste the offline response file contents in the input to activate the server:

## Using command-line options

### Online activation

To activate use **"-a"** option along with the license key and product file path (if not set in the config.yml file):

```bash
lexfloatserver -a --license-key LICENSE_KEY
```

### Offline activation

To activate offline use **"-g"** option to generate the offline activation request:

```bash
lexfloatserver -g --license-key LICENSE_KEY --offline-request FILEPATH
```

After generating the offline response from the admin dashboard, pass it along with **"-a"** option to activate the server:

```
lexfloatserver -a --license-key=LICENSE_KEY --offline-response=FILEPATH
```

## Using Web API

LexFloatServer exposes a few API endpoints which can also be used to activate the server.

### Online activation

Send a POST request to the **/api/server/activate** API endpoint with a JSON request body containing the license key and optionally the activation metadata.

## Activate server

<mark style="color:green;">`POST`</mark> `http://localhost:8090/api/server/activate`

#### Request Body

| Name       | Type   | Description                         |
| ---------- | ------ | ----------------------------------- |
| licenseKey | string | License key to activate the server. |
| metadata   | array  | Activation metadata.                |

{% tabs %}
{% tab title="200 " %}
```javascript
{
  "message": "Server license activation successful!",
  "code": "SERVER_LICENSE_ACTIVATED"
}
```
{% endtab %}

{% tab title="400 " %}
```javascript
{
  "message": "Server license activation failed!",
  "code": "SERVER_INVALID_LICENSE_KEY"
}
```
{% endtab %}
{% endtabs %}

## Offline activation

Send a POST request to the **/api/server/offline-activation-request** API endpoint with a JSON request body containing the license key and optionally the activation metadata.

### Generate offline activation request

<mark style="color:green;">`POST`</mark> `http://localhost:8090/api/server/offline-activation-request`

#### Request Body

| Name       | Type   | Description                         |
| ---------- | ------ | ----------------------------------- |
| licenseKey | string | License key to activate the server. |
| metadata   | array  | Activation metadata.                |

{% tabs %}
{% tab title="200 " %}
```javascript
{
  "offlineRequest": "U7l69tNy8..."
}
```
{% endtab %}
{% endtabs %}

After generating the offline response from the admin dashboard, send a POST request to the **/api/server/offline-activate** API endpoint with a JSON request body containing the license key and the offline response.

### Activate server offline

<mark style="color:green;">`POST`</mark> `http://localhost:8090/api/server/offline-activate`

#### Request Body

| Name            | Type   | Description                         |
| --------------- | ------ | ----------------------------------- |
| licenseKey      | string | License key to activate the server. |
| offlineResponse | string | Offline activation response.        |

{% tabs %}
{% tab title="200 " %}
```javascript
{
  "message": "Server offline license activation successful!",
  "code": "SERVER_LICENSE_ACTIVATED"
}
```
{% endtab %}

{% tab title="400 " %}
```javascript
{
  "message": "Server offline license activation failed!",
  "code": "SERVER_INVALID_LICENSE_KEY"
}
```
{% endtab %}
{% endtabs %}
