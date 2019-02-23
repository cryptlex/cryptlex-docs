# Upgrade Guide

## Using Docker Compose

First login to your Linux server machine where Cryptlex is deployed and go to the directory where the `cryptlex-on-premise` repository was initially cloned. Then execute the following commands:

```bash
# get the latest changes
git pull
# execute the upgrade script
./upgrade.sh
# execute the following command to check the logs for any error
docker-compose logs -t -f
```

{% hint style="info" %}
**Note:** The average downtime during upgrade is less than 2 minutes.
{% endhint %}

## Third-party cloud platforms

In case you have hosted Cryptlex on cloud computing platforms like AWS, GCE, Azure etc. you need to setup your own CD \(continuous deployment\) process to automate the deployment of the new versions. That would depend on the CD tools your company is already using.

In case you need help for setting up the CD process for deploying upgrades we'll be glad to help you. You can contact us through email at: [support@cryptlex.com](mailto:support@cryptlex.com).

