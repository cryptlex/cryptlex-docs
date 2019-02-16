---
description: >-
  Cryptlex can be easily hosted on cloud computing platforms like AWS, GCE,
  Azure, Heroku, DigitalOcean and others supporting Dockers.
---

# Cloud Platforms

## Hosting Cryptlex Web API

Cryptlex web API and GeoIP servers can be easily hosted on any cloud computing platforms with Docker runtimes. The docker images are available on DockerHub:

* [Cryptlex Web API Server](https://hub.docker.com/r/cryptlex/cryptlex-web-api-enterprise) \(private\)
* [Cryptlex GeoIP Server](https://hub.docker.com/r/cryptlex/freegeoip)

{% hint style="warning" %}
The Cryptlex Web API Server must not be exposed publicly on internet. Instead, you must use an HTTPS enabled reverse proxy server \(load balancer\) to forward the traffic to the web API server.
{% endhint %}

Just follow the guide of your cloud computing platform to run Docker apps and ensure following environment variables are set for the web API server:

| Environment Variables | Description |
| :--- | :--- |
| `PORT` | The server port for web API server. Set this to 5000 or some other value and use an HTTPS enabled load balancer to forward the traffic to this server. |
| `DATABASE_URL` | The database URL for Postgres database with following format:  postgres://{user}:{password}@{hostname}:{port}/{database-name} |
| `REDIS_URL` | **Redis is optional**. The database URL for Redis database with following format: redis://{user}:{password}@{hostname}:{port} |
| `GEOIPSERVER_URL` | The URL of the GeoIP server. |
| `RSA_PASSPHRASE` | Use 16 characters long random secret. This is used to encrypt the RSA private key generated for each product you create in the dashboard. |
| `JWT_AUDIENCE` | The public url of the web API server \(or load balancer\). For example https://cryptlex.mycompany.com |
| `JWT_SECRETKEY` | Use at least 32 ASCII characters long random secret. This secret if compromised can be used to compromise the whole account. |
| `APPLICATION_LICENSE_KEY` | The license key which you get after you purchase the license for the Cryptlex On-Premise server. |
| `FORCEHTTPS` | You must set this to `true` to prevent response for non-https requests, if load balancer is listening on port 80 too. |
| `EMAIL_FROMNAME` | From name which should appear for password reset email. |
| `EMAIL_FROMADDRESS` | From email for password reset email. |
| `SMTP_HOST` | SMTP host for sending password reset email. |
| `SMTP_PORT` | SMTP port. |
| `SMTP_ENABLESSL` | Set this to `true` to enable SSL. |
| `SMTP_USERNAME` | SMTP username. |
| `SMTP_PASSWORD` | SMTP password. |



Other than SMTP, Cryptlex also supports MailGun and SendGrid for sending password reset email. So instead of setting SMTP environment variables you can set `MAILGUN_APIKEY` and  `MAILGUN_DOMAIN` environment variables to enable MailGun or set `SENDGRID_APIKEY` environment variable to enable SendGrid.

## Hosting Cryptlex dashboard

The dashboard should ideally be hosted on third party services like [Netlify](https://www.netlify.com/) or [Github](https://pages.github.com/)  which provide globally load balanced, static website servers free of cost.

### Downloading dashboard

The latest or specific version of the dashboard can be downloaded from the following locations:

```bash
# download specific version
curl https://dl.cryptlex.com/downloads/dashboard/{version}/cryptlex-dashboard.zip \
     -o="cryptlex-dashboard.zip"

# download latest version
curl https://dl.cryptlex.com/downloads/dashboard/latest/cryptlex-dashboard.zip \
     -o="cryptlex-dashboard.zip"
```

### Updating config

After unzipping the dashboard web app, open the `config.js` file and set the following values:

```javascript
'use strict';

window.Cryptlex = {
    title : "COMPANY_NAME",
    website: "COMPANY_WEBSITE",
    companyLogoUrl: "COMPANY_LOGO_URL_WITH_TRANSPARENT_BACKGROUND",
    googleAnalyticsKey : "GOOGLE_ANALYTICS_KEY",
    apiBaseUrl : "WEB_API_BASE_URL"
}
```

### Deploying dashboard

Pleasing follow the static website hosting guidelines for [Netlify](https://www.netlify.com/), [Github](https://pages.github.com/), [S3](https://docs.aws.amazon.com/AmazonS3/latest/dev/WebsiteHosting.html) or other hosting providers.

## Using third-party GeoIP service

Instead of using [cryptlex/freegeoip](https://hub.docker.com/r/cryptlex/freegeoip) server for getting location information from the IP address, Cryptlex also supports [ipstack](https://ipstack.com/) and [ipdata](https://ipdata.co/) third-party GeoIP services. 

### Configuring ipstack

To configure the ipstack you need to set following environment variables:

```text
GEOIPSERVER_URL: https://api.ipstack.com
GEOIPSERVER_APIKEY: ${IPSTACK_ACCESS_KEY}
```

### Configuring ipdata

To configure the ipdata you need to set following environment variables:

```text
GEOIPSERVER_URL: https://api.ipdata.co
GEOIPSERVER_APIKEY: ${IPDATA_API_KEY}
```

