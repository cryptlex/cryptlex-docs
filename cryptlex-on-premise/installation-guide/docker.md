---
description: Easily install Cryptlex on any machine using Docker Compose.
---

# Docker

## Before installation

To get started with your Cryptlex On-premise installation, you’ll need the following things prepared in advance:

* If this is your first time installing Cryptlex On-premise, you’ll need to [contact us](mailto:support@cryptlex.com) to schedule a guided installation. We’ll get you set up with a license key, and walk you through the installation process.
* A server meeting the [minimum system requirements](https://docs.cryptlex.com/cryptlex-on-premise/system-requirements).

## Installation

Cryptlex On-premise uses [Docker Compose](https://docs.docker.com/compose/) to perform and manage installations. To install Cryptlex On-premise we first need to install and configure Docker Compose.

### Install Docker Compose

Please refer to following installation guide: [https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/)

### Using Docker Compose

All of the Cryptlex Docker images may be found on [Docker Hub](https://hub.docker.com/u/cryptlex). If you’re looking for a complete configuration to get up and running quickly, use our [Docker Compose](https://github.com/cryptlex/cryptlex-on-premise) example and follow the steps below.

#### Step 1: Create custom A or CNAME records

You will need to create two A or CNAME records for the server machine where you will be deploying Cryptlex, one for the Cryptlex Web API Server and other for the dashboard.. For this tutorial we will choose following two sub-domains:

`cryptlex-api.mycompany.com` for the web API server

`cryptlex-app.mycompany.com` for the web dashboard

Now to create the records:

* Go to your DNS provider’s website \(e.g. [GoDaddy](https://ie.godaddy.com/help/add-a-cname-record-19236) or [Cloudflare](https://www.cloudflare.com/dns/)\).
* Create A or CNAME records for the above custom domains.
* Point both of them at the same IP address or hostname of your server respectively.

#### Step 2: Clone the [cryptlex-on-premise](https://github.com/cryptlex/cryptlex-on-premise) respository

Next you need to login to your Linux server machine and clone the `cryptlex-on-premise` repository inside any folder and execute following commands:

```bash
git clone https://github.com/cryptlex/cryptlex-on-premise
cd cryptlex-on-premise
chmod 0600 acme.json
```

The `acme.json` will store the SSL certificates , which will be generated for the above two sub-domains.

#### Step 3: Update the environment variables

The `cryptlex-on-premise` folder contains the following three files with environment variables which need to be updated with the correct values. 

**Update `.env` file**

The `.env` file contains the following environment variables which you may need to update:

| Environment Variables | Description |
| :--- | :--- |
| `POSTGRES_DB` | Name of the database. |
| `POSTGRES_USER` | Username of the database user. |
| `POSTGRES_PASSWORD` | Password of the database user. |
| `EMAIL` | Email required for SSL certificate notifications. |
| `WEB_API_DOMAIN` | The domain of the the web API server. In this case: `cryptlex-api.mycompany.com` |
| `DASHBOARD_DOMAIN` | The domain of the the web dashboard. In this case: `cryptlex-app.mycompany.com` |
| `TRAEFIK_BASIC_AUTH` | [Traefik](https://traefik.io/) is the reverse proxy. You can set the basic auth credentials for the Traefik dashboard. |

**Update `webapi.env` file**

The `webapi.env` file contains the following environment variables which you **must** update:

| Environment Variables | Description |
| :--- | :--- |
| `RSA_PASSPHRASE` | Use 16 characters long random secret. This is used to encrypt the RSA private key generated for each product you create in the dashboard. |
| `JWT_SECRETKEY` | Use at least 32 ASCII characters long random secret. **This secret if compromised, can be used to** **gain access to the whole account.** |
| `APPLICATION_LICENSE_KEY` | The license key which you get after you purchase the license for the Cryptlex On-Premise server. |

Other than the above three you need to set environment variables for the email provider \(MailGun, SendGrid or SMTP\) and additionally you can configure other monitoring and error reporting services.

**Update `dashboard.env` file**

The `dashboard.env` file contains the following environment variables which you may need to update:

| Environment Variables | Description |
| :--- | :--- |
| `COMPANY_NAME` | This shows up in the browser title. |
| `COMPANY_WEBSITE` | Your company website. |
| `COMPANY_LOGO_URL` | Logo to be displayed. It must have a transparent background. |
| `COMPANY_FAVICON_URL` | Favicon URL. |
| `GOOGLE_ANALYTICS_KEY` | Google analytics key. |

#### Step 4: Run Docker Compose

Execute the following commands to start the server:

```bash
# ensure you have access to Cryptlex Docker images
docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD
# execute docker-compose command without -d option to check the logs
docker-compose up
```

If everything goes fine, as will be evident from the console logs, you should stop the server and run the server again with `-d` option so that it runs in the background.

```bash
docker-compose stop
docker-compose up -d
```

The [Traefik](https://traefik.io/) reverse proxy server configured in the `docker-compose.yml` file will automatically generate SSL certificates for the above two domains and store them in `acme.json`. Additionally, it will route the traffic to respective containers.

#### Step 5: Signup for the Cryptlex account

Next you need to open the dashboard in the browser, which can be accessed at following url: [**https://cryptlex-app.mycompany.com**](https://cryptlex-app.mycompany.com)\*\*\*\*

You ****will be redirected to the login page. Click the signup link at the bottom of the login page and create your account.

{% hint style="info" %}
Only one Cryptlex account can be created in the on-premise version.
{% endhint %}

### Docker Compose file details

In the [docker-compose.yml](https://github.com/cryptlex/cryptlex-on-premise/blob/master/docker-compose.yml) file you will find the `db`, `cache`, `geoip`, `webapi`, `dashboard` and `reverseproxy` services. Read below to better understand how each service is configured.

#### Database \(db\) service <a id="database-service"></a>

It contains Postgres database server, which is used to store all the Cryptlex data.

#### Cache service \(optional\) <a id="search-service"></a>

It uses Redis for storing IP rate limiting data. If no Redis database is provided it defaults to memory.

#### GeoIP service <a id="search-service"></a>

This service is used to get location information from the IP address of the user.

#### Web API service

It is the core service which runs the Cryptlex web API server.

#### Dashboard service

It hosts the Cryptlex web dashboard. It is a single page progressive web application.

#### Reverse proxy service

It's uses Traefik reverse proxy server to route the traffic and automatically generates and renews the SSL certificates for the `WEB_API_DOMAIN` and `DASHBOARD_DOMAIN`.

### Traefik admin dashboard

Traefik provides a dashboard which can be used to monitor the health and status of the Cryptlex on-Premise instance. You can access the Traefik dashboard at the following url: [**https://cryptlex-app.mycompany.com/traefik**](https://cryptlex-app.mycompany.com/traefik)\*\*\*\*

You will need to put in the credentials set in the `.env` file to access the dashboard.

### Checking logs

Docker compose writes the **stdout** and **stderr** logs of each container in a JSON file located in `/var/lib/docker/containers/[container-id]/[container-id]-json.log.`

To prevent logs from taking up the whole disk space, `10MB` limit has been applied to all the containers in the `docker-compose.yml` file. You can change that as per your requirements.

To view the logs in realtime you can execute the following command:

```bash
docker-compose logs -t -f
```



