---
description: Expose Cryptlex dashboard and Web API server endpoints via HTTPS using Nginx.
---

# SSL Termination

To make your Cryptlex services available over secured TLS/SSL connections, we recommend using Nginx to set up a reverse proxy. The following instructions are for the Cryptlex dashboard but can be applied to other endpoints.

## Installing and configuring Nginx

[Install Nginx](https://www.nginx.com/resources/wiki/start/topics/tutorials/install/) on the server where your Cryptlex On-premise installation is located.

### Locate your configuration file

Locate the `nginx.conf` for your install, typically at `/etc/nginx/nginx.conf`.

### Handle HTTPS traffic

Create a `server` block in your Nginx configuration file to handle HTTPS traffic, and configure your SSL certificate:

```text
server {
  listen 443 default_server ssl;
  ssl_certificate /path/to/your/cert.pem;
  ssl_certificate_key /path/to/your/cert.key;
  server_name cryptlex.your-domain.com;

  location / {
    proxy_pass http://127.0.0.1:5000;
    proxy_set_header HOST $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
  }
}
```

## Redirect HTTP traffic to HTTPS

Create the server block for your site to redirect HTTP traffic to HTTPS if you wish.

```text
server {
  listen 80 default_server;
  server_name cryptlex.your-domain.com;
  return 301 https://$host$request_uri;
}
```

Restart Nginx to pick up config changes, for example by running `/etc/init.d/nginx restart`.

