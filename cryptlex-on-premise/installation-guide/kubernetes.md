---
description: Easily install Cryptlex on any cloud hosting provider using Kubernetes.
---

# Kubernetes

## Introduction

In this guide, you’ll install the Cryptlex Enterprise Kubernetes application using [Helm](https://helm.sh/). You’ll then create an Ingress Resource to route traffic from your domains to the Cryptlex Enterprise back-end services. Once you’ve set up the Ingress, you’ll install [Cert Manager](https://github.com/jetstack/cert-manager) to your cluster to be able to automatically provision Let’s Encrypt TLS certificates to secure your Ingresses.

[Helm](https://helm.sh/) is a package manager for managing Kubernetes. Using Helm Charts with your Kubernetes provides configurability and lifecycle management to update, rollback, and delete a Kubernetes application.

## Prerequisites

* A Kubernetes 1.15+ cluster with your connection configuration configured as the `kubectl` default.
* The Helm 3 package manager installed on your local machine.
* A fully registered domain name with three available A records. This tutorial will use `license-api.mycompany.com`, `license-portal.mycompany.com` and  `releases.mycompany.com`throughout.

## Installation

### Step 1 — Installing the Kubernetes Nginx Ingress Controller

You will first need to install the Kubernetes-maintained [Nginx Ingress Controller](https://github.com/kubernetes/ingress-nginx) using Helm. 

This Service is of type LoadBalancer, and because you are deploying it to a Kubernetes cluster, the cluster will automatically create a Load Balancer, through which all external traffic will flow to the appropriate back-end services.

The Nginx Ingress Helm chart uses an `ingress.yaml` file for setting the configuration. You need to download this file to your local machine.

{% code title="ingress.yaml" %}
```yaml
# nginx configuration

controller:
  publishService:
    enabled: true
  service:
    enabled: true
    externalTrafficPolicy: "Local"
  config:
    ssl-ciphers: "ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384:DHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-RSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES256-SHA256:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:DES-CBC3-SHA"
    ssl-protocols: "TLSv1 TLSv1.1 TLSv1.2 TLSv1.3"
```
{% endcode %}

To install the Nginx Ingress Controller to your cluster, run the following commands:

```text
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm upgrade --install ingress-nginx ingress-nginx/ingress-nginx --values ingress.yaml
```

You can watch the Load Balancer become available by running:

```text
kubectl get services -o wide -w ingress-nginx-controller
```

You’ve installed the Nginx Ingress maintained by the Kubernetes community. It will route HTTP and HTTPS traffic from the Load Balancer to appropriate back-end Services, configured in Ingress Resources.

### Step 2 — Create custom A records

You will need to create three A records for the external IP address of the Nginx Ingress installed in the previous step. For this tutorial we will choose following three sub-domains:

`license-api.mycompany.com` for the Web API Server

`license-portal.mycompany.com` for the Web Dashboard

`releases.mycompany.com` for the Release Server

In order to get the external IP address you can execute the following command:

```text
kubectl get services -o wide -w ingress-nginx-controller
```

Now to create the records:

* Go to your DNS provider’s website \(e.g. [GoDaddy](https://ie.godaddy.com/help/add-a-cname-record-19236) or [Cloudflare](https://www.cloudflare.com/dns/)\).
* Create A records for the above custom domains.
* Point all of them to the same IP address.

### Step 3 — Installing the Cryptlex Enterprise Kubernetes application

In this section you will deploy the Cryptlex Enterprise Kubernetes application in your Kubernetes cluster.

#### Step 3.1 —  Generate a 2048 bit RSA key pair

The RSA key pair is required to sign and verify the JWT access tokens used for authentication purpose. To generate the RSA key pair execute the following commands in the terminal:

```bash
# Execute the following command and type the passphrase
openssl genrsa -aes128 -passout stdin -out private.pem 2048

# Extract the public key
openssl rsa -in private.pem -outform PEM -pubout -out public.pem
```

The above commands will generate the multi-line keys in the `private.pem` and `public.pem` files. In order to pass them as environment variables they need to be converted to the single line string. To get the single line strings from the above the files, execute following commands:

```bash
awk 'NF {sub(/\r/, ""); printf "%s\\n",$0;}' private.pem
awk 'NF {sub(/\r/, ""); printf "%s\\n",$0;}' public.pem
```

The above generated keys would be used in the next steps.

#### Step 3.2 —  Choosing database

Postgres database is required for storing all Cryptlex data. The Cryptlex Enterprise Kubernetes app will automatically spin up a Postgres database instance and will use the persistent volume claim for requesting the storage disk. This option may be good for staging/testing environments, but for production environment we recommend using a third party Postgres database service.

#### Step 3.3 —  Choosing file store

Any AWS S3 compatible file store is required for storing releases. In case you don't want to use Cryptlex [release management](https://docs.cryptlex.com/release-management) API, this service is not required. 

The Cryptlex Enterprise Kubernetes app will automatically spin up a [Minio](https://min.io/) instance and will use the persistent volume claim for requesting the storage disk. This option may be good for staging/testing environments, but for production environment we recommend using a third party AWS S3 compatible file store service.

#### Step 3.4 —  Download and update the Helm values file

The Cryptlex Enterprise Helm chart uses a `values.yaml` file for setting the configuration. You need to download this file to your local machine and update this file for each environment.

[https://raw.githubusercontent.com/cryptlex/helm-charts/master/cryptlex/cryptlex-enterprise/values.yaml](https://raw.githubusercontent.com/cryptlex/helm-charts/master/cryptlex/cryptlex-enterprise/values.yaml)

Download two copies of this file and rename them to `production.yaml` and `staging.yaml` \(or `testing.yaml`, `development.yaml` etc.\) Here is the sample:

```yaml
# Default values for cryptlex-enterprise.

# Certmanager letsencrypt config
certmanager:
  issuer:
    # Set this to your company email.
    email: support@mycompany.com
    # Set this to true once staging certificates are issued successfully.
    # Otherwise you may run into rate-limiting issues.
    production: false

# Docker registry credentials
imageCredentials:
  registry: https://index.docker.io/v1/
  username: 
  password: 

# Ingress config
ingress:
  enabled: true
  hosts:
    # Hostname of the Cryptlex Web API server.
    webApiHost: license-api.mycompany.com
    # Hostname of the Cryptlex Web Dashboard server.
    dashboardHost: license-portal.mycompany.com
    # Hostname of the Cryptlex Release server.
    releaseServerHost: releases.mycompany.com

# Configure Cryptlex services
services:
  database:
    # Set this to true in case you are using an external database.
    external: false
    storage: 5Gi
  geoip:
    # Set this to true in case you are using an external geoip service.
    external: false
  filestore:
    # Set this to false in case you are not using Cryptlex release management feature.
    enabled: true
    # Set this to true in case you are using an external filestore like AWS S3, Azure Minio etc.
    external: false
    storage: 5Gi

# Database config (ignored in case you are using an external database)
database:
  name: cryptlex
  user: postgres
  password: postgres

# Filestore config
filestore:
  accessKey: minio
  secretKey: minio_secret
  # Set this to 443 in case you are using an external filestore like AWS S3, Azure Minio etc.
  port: 9000
  # Name of the bucket where you want to store all your files.
  bucket: releases.mycompany.com
  # This is required in case you are using AWS S3, otherwise leave the default value as such.
  region: us-east-1
  # Set this to true in case you are using an external filestore like AWS S3, Azure Minio etc.
  useSsl: false

# Dashboard config
dashboard:
  # Your company name. This shows up in the browser title.
  companyName: My Company
  # Your company website.
  companyWebsite: https://mycompany.com
  # Logo to be displayed. It must have a transparent background.
  companyLogoUrl: https://mycompany.com/logo.png
  # Favicon URL.
  companyFaviconUrl: https://mycompany.com/favicon.ico
  # Google analytics key.
  googleAnalyticsKey: UA-XXXXXXXX-X

# Geo IP config (only required in case you are using an external service like ipstack.com or ipdata.co)
geoip:
  # The geo ip server url.
  serverUrl:
  # The ipstack access key or ipdata API key.
  apiKey:

# Web API config
webApi:
  # Set this to 3 for production environment.
  replicaCount: 1
  # This name appears in email body and 2FA secret url.
  applicationName: MyCompany
  # The license key which you get after you purchase the license for the Cryptlex Enterprise (on-premise).
  serverLicenseKey: PASTE_LICENSE_KEY
  # The database connection string, only required in case you are using an external database.
  databaseUrl: postgres://{user}:{password}@{hostname}:{port}/{database-name}
  # Single line RSA private key.
  jwtRsaPrivateKey: "PASTE_SINGLE_LINE_RSA_PRIVATE_KEY"
  # Single line RSA public key.
  jwtRsaPublicKey: "PASTE_SINGLE_LINE_RSA_PUBLIC_KEY"
  # The passphrase which was used to encrypt the JWT RSA private key.
  rsaPassphrase: PASTE_RSA_SECRET
  # IP rate limiting options.
  ipRateLimitOptions:
    rateLimit: 50
    ipWhitelist: []

  # Mail settings
  email:  
    # From email for password reset email.
    fromAddress: support@mycompany.com
    # From name for password reset email.
    fromName: MyCompany Support
    # Email signature for password reset email.
    signature: <p>Thanks,<br>The MyCompany Team</p>
    # SMTP config for sending emails.
    smtp:
      host: ""
      port: 587
      enableSsl: true
      username: ""
      password: ""
    # Mailgun config, in case you are using Mailgun for sending emails.
    mailgun:
      apiKey: ""
      domain: ""
    # Sendgrid config, in case you are using Sendgrid for sending emails.
    sendgrid:
      apiKey: ""

  # Error monitoring
  bugsnag:
    apiKey: ""

  # App metrics
  newRelic:
    licenseKey: ""

# SSO config
sso:
  google:
    # Refer to following for enabling Google SSO: https://docs.cryptlex.com/user-management/google-sso
    clientId: ""
```

You need to update this file for each environment. You should also generate separate RSA keys for each environment.

#### Step 3.5 —  Installing the Cryptlex Enterprise Helm chart

After you have updated the `values.yaml` \(in this case `production.yaml` and `staging.yaml`\) file for each environment, execute following commands to install the Cryptlex Enterprise Helm chart for each environment:

```bash
helm repo add cryptlex https://cryptlex.github.io/helm-charts

# Staging environment
kubectl create namespace cryptlex-stg
helm upgrade --install cryptlex-enterprise-stg --values staging.yaml --namespace cryptlex-stg cryptlex/cryptlex-enterprise

# Production environment
kubectl create namespace cryptlex
helm upgrade --install cryptlex-enterprise --values production.yaml --namespace cryptlex cryptlex/cryptlex-enterprise

```

### Step 4 — Securing the Nginx Ingress using Cert-Manager

To secure your Ingress Resources, you need to install the [Cert-Manager](https://cert-manager.io/docs/installation/kubernetes/). Once installed and configured, your app will be running behind HTTPS.

To install the Cert-Manager to your cluster, run the following commands:

```text
kubectl create namespace cert-manager
helm repo add jetstack https://charts.jetstack.io
helm upgrade --install cert-manager jetstack/cert-manager --version v0.15.0 --namespace cert-manager --set installCRDs=true
```

You’ll need to wait a few minutes for the Let’s Encrypt servers to issue a certificate for your domains. In the meantime, you can track its progress by inspecting the output of the following command:

```text
kubectl describe certificate -n cert-manager
```

The end of the output will look similar to this:

```text
OutputEvents:
  Type    Reason        Age   From          Message
  ----    ------        ----  ----          -------
  Normal  GeneratedKey  48s   cert-manager  Generated a new private key
  Normal  Requested     48s   cert-manager  Created new CertificateRequest resource "hello-kubernetes-tls-4208342520"
  Normal  Issued        21s   cert-manager  Certificate issued successfully
```

Navigate to one of your domains in your browser to test. You’ll see the padlock to the left of the address bar in your browser, signifying that your connection is secure.

### Step 5 — Signup for the Cryptlex account

Next you need to open the dashboard in the browser, and create your Cryptlex account, which can be done at following url: 

**https://license-portal.mycompany.com/auth/signup**

{% hint style="info" %}
Please note that you can only create one Cryptlex account.
{% endhint %}

## Upgrading

It's important that you regularly upgrade the apps installed in your Kubernetes cluster to ensure you get new security updates and bug fixes.

In order to upgrade the apps just execute the following commands:

```bash
# Get the latest versions
helm repo update

# Upgrade the Nginx Ingress
helm upgrade --install ingress-nginx ingress-nginx/ingress-nginx --values ingress.yaml

# Upgrade the staging Cryptlex Enterprise app
helm upgrade --install cryptlex-enterprise-stg --values staging.yaml --namespace cryptlex-stg cryptlex/cryptlex-enterprise

# Upgrade the production Cryptlex Enterprise app
helm upgrade --install cryptlex-enterprise --values production.yaml --namespace cryptlex cryptlex/cryptlex-enterprise
```

For upgrading Cert-Manager please refer to there upgrading guide:

[https://cert-manager.io/docs/installation/upgrading/](https://cert-manager.io/docs/installation/upgrading/)



