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

All of the Cryptlex Docker images may be found on [Docker Hub](https://hub.docker.com/u/cryptlex). If you’re looking for a complete configuration to get up and running quickly, use our Docker Compose example.

```bash
git clone https://github.com/cryptlex/cryptlex-on-premise
# update the .env, webapi.env and dashboard.env files
# on first run server may take upto 2 minutes to generate certificates
docker-compose up
```

The following is an example and it may not be the most recent version. Refer to the following link in [GitHub](https://github.com/cryptlex/cryptlex-on-premise) to find the latest version. The stock `.env` file contains the following values, you will want to modify the `POSTGRES_DB` and ensure the `POSTGRES_USER` , `POSTGRES_PASSWORD`, `EMAIL` and `WEB_DOMAIN` values are correct. You may also override any of these values using environment variables.

```text
# postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
POSTGRES_DB=cryptlex

# LetsEncrypt SSL certificate
EMAIL=joe.doe@mycompany.com
WEB_DOMAIN=cryptlex.mycompany.com
```

{% hint style="warning" %}
Ensure that the server has a public IP address and a web domain, as running `docker-compose` command will automatically try to generate an SSL certificate through LetsEncrypt to enable HTTPS.
{% endhint %}

```yaml
version: '3'

services:
  db:
    image: postgres:10
    environment:
      PGDATA: /var/lib/postgresql/data/pgdata
      POSTGRES_USER: ${POSTGRES_USER}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
      POSTGRES_DB: ${POSTGRES_DB}
    ports:
      - 5432
    networks:
      - backend
    restart: unless-stopped
    volumes:
      - db_data:/var/lib/postgresql/data

  cache:
    image: redis:alpine
    ports:
      - 6379
    networks:
      - backend
    restart: unless-stopped

  geoip:
    image: cryptlex/freegeoip:3.6.0
    ports:
      - 8080
    networks:
      - backend
    restart: unless-stopped
  
  loadbalancer: 
    image: linuxserver/letsencrypt:0.31.0-ls4
    volumes:
      - ./config:/config
    environment:
      - EMAIL=${EMAIL}
      - URL=${WEB_DOMAIN}
    depends_on:
      - webapi
    ports:
      - 80:80
      - 443:443
    networks:
      - backend
    restart: unless-stopped

  webapi:
    image: cryptlex/cryptlex-web-api-enterprise:3.10.1
    depends_on:
      - db
      - geoip
    env_file: webapi.env
    environment:
      JWT_AUDIENCE: https://${WEB_DOMAIN}
      DATABASE_URL: postgres://${POSTGRES_USER}:${POSTGRES_PASSWORD}@db:5432/${POSTGRES_DB}
      REDIS_URL: redis://:@cache:6379
      GEOIPSERVER_URL: http://geoip:8080/json
    networks:
      - backend
    restart: unless-stopped
    ports:
      - 5000

  dashboard:
    image: cryptlex/cryptlex-web-dashboard:3.0.6
    depends_on:
      - webapi
    env_file: dashboard.env
    environment:
      WEB_API_BASE_URL: https://${WEB_DOMAIN}
    networks:
      - frontend
    restart: unless-stopped
    ports:
      - 4200:80

networks:
  backend:
    driver: bridge
  frontend:
    driver: bridge

volumes:
  db_data:
```

### Docker services <a id="docker-services"></a>

In the above example configuration you will find a db, cache, geoip,  webapi, dashboard and load balancer services. Read below to better understand how each service is configured.

#### Database service <a id="database-service"></a>

At a minimum, you will need to either set the `POSTGRES_PASSWORD` environment variable in the `db` service section, or more ideally set the value in the host environment `.env` file. Ensure the other properties fit your requirements.

#### Cache service \(optional\) <a id="search-service"></a>

It uses Redis for storing IP rate limiting data. If no Redis database is provided it defaults to memory. No configuration is needed.

#### GeoIP service <a id="search-service"></a>

This service is used to get location information from the IP address of the user. No configuration is needed.

#### Web API service

At a minimum, you must set the following environment variables present in the `webapi.env` file:

* `RSA_PASSPHRASE`: Use 16 characters long random secret. This is used to encrypt the RSA private key generated for each product you create in the dashboard.
* `JWT_SECRETKEY`: Use at least 32 ASCII characters long random secret. This secret if compromised can be used to compromise the whole account.
* `APPLICATION_LICENSE_KEY`: The license key which you get after you purchase the license for the Cryptlex On-Premise server.

Other than the above three you need to set environment variables for the email provider \(MailGun, SendGrid or SMTP\) and additionally you can configure other monitoring and error reporting services.

The web API can be accessed at following URL: https://${WEB\_DOMAIN}/v3/status

#### Dashboard service

It hosts the Cryptlex web dashboard at port 4200. It is a single page application and should ideally be hosted on Github, Netlify or S3.

To configure the dashboard you need to set following environment variables in the `dashboard.env` file:

* `COMPANY_NAME`: This shows up in the browser title.
* `COMPANY_WEBSITE`: Your company website.
* `COMPANY_LOGO_URL`: Logo to be displayed in the dashboard.
* `COMPANY_WHITE_LOGO_URL`: White coloured version of your company logo.
* `GOOGLE_ANALYTICS_KEY`: Google analytics key.

The dashboard can be accessed at following URL: http://${WEB\_DOMAIN}:4200

#### Load balancer service

It's an Nginx and LetsEncrypt docker image which acts as a reverse proxy and automatically generates and renews the SSL certificate for the `WEB_DOMAIN`.

To configure the load balancer service, set the `EMAIL` and `WEB_DOMAIN` environment variables in the `.env` file.

{% hint style="warning" %}
`WEB_DOMAIN` environment variable must be set to a valid domain which can be accessed over the internet.
{% endhint %}

