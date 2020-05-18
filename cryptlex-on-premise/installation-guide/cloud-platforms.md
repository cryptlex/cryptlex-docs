---
description: >-
  Cryptlex can be easily hosted on cloud computing platforms like AWS, GCE,
  Azure, Heroku, DigitalOcean and others supporting Dockers.
---

# Cloud Platforms

## Hosting Cryptlex On-Premise

In order to run Cryptlex on any cloud computing platform, you would require following services:

### Database

**Postgres** database is required for storing all Cryptlex data. Following are some of the cloud computing platforms which provide Postgres database service:

* [Amazon RDS](https://aws.amazon.com/rds/postgresql/)
* [Google Cloud SQL](https://cloud.google.com/sql/docs/postgres/)
* [Azure Database](https://azure.microsoft.com/en-in/services/postgresql/)
* [Heroku Postgres](https://www.heroku.com/postgres)
* [DigitalOcean Postgres](https://www.digitalocean.com/products/managed-databases/)

### Cache \(optional\)

**Redis** is optionally required for storing IP rate limiting data. If no Redis database is provided it defaults to memory. Following are some of the cloud computing platforms which provide Redis database service:

* [Amazon ElastiCache](https://aws.amazon.com/elasticache/)
* [Google Cloud Memorystore](https://cloud.google.com/memorystore/)
* [Azure Cache](https://azure.microsoft.com/en-in/services/cache/)
* [Heroku Redis](https://www.heroku.com/redis)

### Filestore

Any AWS S3 compatible file store is required for storing releases. In case you don't want to use Cryptlex [release management](https://docs.cryptlex.com/release-management) API, this service is not required. Currently following file stores are supported:

* [Amazon S3](https://aws.amazon.com/s3/)
* [Google Cloud Storage](https://cloud.google.com/storage/)
* [Minio](https://www.minio.io/) \(self-host\)

### Cryptlex Web API Server

Cryptlex Web API server can be easily hosted on any cloud computing platform with Docker runtime. The Docker image is available on DockerHub:

* [Cryptlex Web API Server](https://hub.docker.com/r/cryptlex/cryptlex-web-api-enterprise) \(private\)

{% hint style="warning" %}
The Cryptlex Web API server must not be exposed publicly on internet. Instead, you must use an HTTPS enabled reverse proxy server \(load balancer\) to forward the traffic to the server.
{% endhint %}

Just follow the guide of your cloud computing platform to run Docker apps and ensure following environment variables are set for the Web API server:

| Environment Variables | Description |
| :--- | :--- |
| `PORT` | The server port for web API server. Set this to 5000 or some other value and use an HTTPS enabled load balancer to forward the traffic to this server. |
| `DATABASE_URL` | The database URL for Postgres database with following format:  postgres://{user}:{password}@{hostname}:{port}/{database-name} |
| `REDIS_URL` | **Redis is optional**. The database URL for Redis database with following format: redis://{user}:{password}@{hostname}:{port} |
| `GEOIPSERVER_URL` | The URL of the GeoIP server. |
| `JWT_AUDIENCE` | The public url of the web API server \(or load balancer\). For example https://cryptlex.mycompany.com |
| `RSA_PASSPHRASE` | Random secret used to encrypt the private key.  |
| `JWT_RSA_PRIVATEKEY` | Use the single line private key. **This key if compromised, can be used to** **gain access to the whole account.** |
| `JWT_RSA_PUBLICKEY` | Use the single line public key. |
| `GOOGLE_CLIENT_ID` | This is needed in case you want to enable Google SSO. |
| `EMAIL_FROMNAME` | From name which should appear for password reset email. |
| `EMAIL_FROMADDRESS` | From email for password reset email. |
| `SMTP_HOST` | SMTP host for sending password reset email. |
| `SMTP_PORT` | SMTP port. |
| `SMTP_ENABLESSL` | Set this to `true` to enable SSL. |
| `SMTP_USERNAME` | SMTP username. |
| `SMTP_PASSWORD` | SMTP password. |

Other than SMTP, Cryptlex also supports MailGun and SendGrid for sending password reset email. So instead of setting SMTP environment variables you can set `MAILGUN_APIKEY` and  `MAILGUN_DOMAIN` environment variables to enable MailGun or set `SENDGRID_APIKEY` environment variable to enable SendGrid.

### Geo IP Server

This service is used to get location information from the IP address of the user. Cryptlex GeoIP  server can be easily hosted on any cloud computing platform with Docker runtime. The docker image is available on DockerHub:

* [Cryptlex GeoIP Server](https://hub.docker.com/r/cryptlex/freegeoip)

Instead of using [cryptlex/freegeoip](https://hub.docker.com/r/cryptlex/freegeoip) server for getting location information from the IP address, you can also use [Ipstack](https://ipstack.com/) and [Ipdata](https://ipdata.co/) third-party GeoIP services. 

#### Configuring ipstack

To configure the ipstack you need to set following environment variables for the Web API server:

```text
GEOIPSERVER_URL: https://api.ipstack.com
GEOIPSERVER_APIKEY: ${IPSTACK_ACCESS_KEY}
```

#### Configuring ipdata

To configure the ipdata you need to set following environment variables for the Web API server:

```text
GEOIPSERVER_URL: https://api.ipdata.co
GEOIPSERVER_APIKEY: ${IPDATA_API_KEY}
```

### Cryptlex Release Server

Cryptlex Release server handles the upload and download of releases you create in Cryptlex. In case you don't want to use Cryptlex [release management](https://docs.cryptlex.com/release-management) API, this service is not required. It can be easily hosted on any cloud computing platform with Docker runtime. The docker image is available on DockerHub:

* [Cryptlex Release Server](https://hub.docker.com/r/cryptlex/cryptlex-release-server) \(private\)

{% hint style="warning" %}
The Cryptlex Release server must not be exposed publicly on internet. Instead, you must use an HTTPS enabled reverse proxy server \(load balancer\) to forward the traffic to the server.
{% endhint %}

Just follow the guide of your cloud computing platform to run Docker apps and ensure following environment variables are set for the Release server:

| Environment Variables | Description |
| :--- | :--- |
| `PORT` | The server port for Release server. Set this to 3000 or some other value and use an HTTPS enabled load balancer to forward the traffic to this server. |
| `RELEASE_SERVER_BASE_URL` | The  public URL of Release server e.g. https://cryptlex-releases.mycompany.com |
| `WEB_API_BASE_URL` | The  public URL of Web API server e.g. https://cryptlex-api.mycompany.com |
| `FILE_STORE_ACCESS_KEY` | The access key of the Filestore. |
| `FILE_STORE_SECRET_KEY` | The secret key of the Filestore. |
| `FILE_STORE_BUCKET` | Name of the bucket where you want to store all your files. |
| `FILE_STORE_REGION` | This is required in case you are using AWS S3, otherwise leave the default value as such. |
| `FILE_STORE_USE_SSL` | This should only be set to true in case you are using AWS S3. |
| `FILE_STORE_ENDPOINT` | The hostname of the Filestore server. In case you are using AWS S3 set this to: `s3.amazonaws.com` |
| `FILE_STORE_PORT` | The port of the Filestore server. In case you are using AWS S3 set this to:  `443` |

### Cryptlex Dashboard

The dashboard should ideally be hosted on third party services like [Netlify](https://www.netlify.com/) or [Github](https://pages.github.com/) which provide globally load balanced, static website servers free of cost.

#### Downloading dashboard

The latest or specific version of the dashboard can be downloaded from the following locations:

```bash
# download specific version
curl https://dl.cryptlex.com/downloads/dashboard/{version}/cryptlex-dashboard.zip \
     -o="cryptlex-dashboard.zip"

# download latest version
curl https://dl.cryptlex.com/downloads/dashboard/latest/cryptlex-dashboard.zip \
     -o="cryptlex-dashboard.zip"
```

#### Updating config

After unzipping the dashboard web app, open the `assets/custom/config.js` file and set the following values:

```javascript
'use strict';

window.Cryptlex = {
    title : "COMPANY_NAME",
    website: "COMPANY_WEBSITE",
    logoUrl: "COMPANY_LOGO_URL_WITH_TRANSPARENT_BACKGROUND",
    faviconUrl: "COMPANY_FAVICON_URL",
    googleAnalyticsKey : "GOOGLE_ANALYTICS_KEY",
    googleClientId : "GOOGLE_CLIENT_ID",
    apiBaseUrl : "WEB_API_BASE_URL",
    releaseServerBaseUrl : "RELEASE_SERVER_BASE_URL"
}
```

#### Deploying dashboard

Pleasing follow the static website hosting guidelines for [Netlify](https://www.netlify.com/), [Github](https://pages.github.com/), [S3](https://docs.aws.amazon.com/AmazonS3/latest/dev/WebsiteHosting.html) or other hosting providers.

#### Using Docker

You can also use the Docker, which uses Nginx to host the dashboard on port **4200**. The docker image is available on DockerHub:

* [Cryptlex Web Dashboard](https://hub.docker.com/r/cryptlex/cryptlex-web-dashboard)

Just follow the guide of your cloud computing platform to run Docker apps and ensure following environment variables are set for the Dashboard static server:

| Environment Variables | Description |
| :--- | :--- |
| `RELEASE_SERVER_BASE_URL` | The  public URL of Release server e.g. https://cryptlex-releases.mycompany.com |
| `WEB_API_BASE_URL` | The  public URL of Web API server e.g. https://cryptlex-api.mycompany.com |
| `COMPANY_NAME` | This shows up in the browser title. |
| `COMPANY_WEBSITE` | Your company website. |
| `COMPANY_LOGO_URL` | Logo to be displayed. It must have a transparent background. |
| `COMPANY_FAVICON_URL` | Favicon URL. |
| `GOOGLE_CLIENT_ID` | This is needed in case you want to enable Google SSO. |
| `GOOGLE_ANALYTICS_KEY` | Google analytics key. |



