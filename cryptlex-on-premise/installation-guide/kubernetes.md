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

This Service is of type LoadBalancer, and because you are deploying it to a Kubernetes cluster, the cluster will automatically create a Load Balancer, through which all external traffic will flow to the appropriate backend services.

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

### Step 2 — Create custom A/CNAME records

You will need to create three A/CNAME records for the external IP address of the Nginx Ingress installed in the previous step. For this tutorial we will choose the following three sub-domains:

`license-api.mycompany.com` for the Web API Server

`license-portal.mycompany.com` for the Web Dashboard

`releases.mycompany.com` for the Release Server

In order to get the external IP address you can execute the following command:

```text
kubectl get services -o wide -w ingress-nginx-controller
```

Now to create the records:

* Go to your DNS provider’s website \(e.g. [GoDaddy](https://ie.godaddy.com/help/add-a-cname-record-19236) or [Cloudflare](https://www.cloudflare.com/dns/)\).
* Create A/CNAME records for the above custom domains.
* Point all of them to the same IP address.

### Step 3 — Securing the Nginx Ingress using Cert-Manager

To secure your Ingress Resources, you need to install the [Cert-Manager](https://cert-manager.io/docs/installation/kubernetes/). Once installed and configured, your app will be running behind HTTPS.

To install the Cert-Manager to your cluster, run the following commands:

```text
kubectl create namespace cert-manager
helm repo add jetstack https://charts.jetstack.io
helm upgrade --install cert-manager jetstack/cert-manager --version v0.16.1 --namespace cert-manager --set installCRDs=true
```

### Step 4 — Installing the Cryptlex Enterprise Kubernetes application

In this section, you will deploy the Cryptlex Enterprise Kubernetes application in your Kubernetes cluster.

#### Step 4.1 —  Choosing the database

Postgres database is required for storing all Cryptlex data. The Cryptlex Enterprise Kubernetes app will automatically spin up a Postgres database instance and will use the persistent volume claim for requesting the storage disk. This option may be good for staging/testing environments, but for the production environment, we recommend using a third party Postgres database service.

#### Step 4.2 —  Choosing the file store

The file store \(AWS S3 compatible\) is required for storing releases. In case you don't want to use the Cryptlex [release management](https://docs.cryptlex.com/release-management) API, this service is not required. 

The Cryptlex Enterprise Kubernetes app will automatically spin up a [Minio](https://min.io/) instance and will use the persistent volume claim for requesting the storage disk. This option may be good for staging/testing environments, but for the production environment, we recommend using a third-party AWS S3 compatible file store service.

#### Step 4.3 —  Download and update the Helm values file

The Cryptlex Enterprise Helm chart uses a `values.yaml` file for setting the configuration. You need to download this file to your local machine and update this file for each environment.

[https://raw.githubusercontent.com/cryptlex/helm-charts/master/cryptlex/cryptlex-enterprise/values.yaml](https://raw.githubusercontent.com/cryptlex/helm-charts/master/cryptlex/cryptlex-enterprise/values.yaml)

Download two copies of this file and rename them to `production.yaml` and `staging.yaml` \(or `testing.yaml`, `development.yaml` etc.\).

You need to update this file for each environment.

#### Step 4.4 —  Installing the Cryptlex Enterprise Helm chart

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

### Step 5 — Signup for the Cryptlex account

Next, you need to open the dashboard in the browser, and create your Cryptlex account, which can be done at following URL: 

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



