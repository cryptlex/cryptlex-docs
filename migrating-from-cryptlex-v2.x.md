---
description: This is a migration guide for Cryptlex v2.x customers.
---

# Migrating from Cryptlex v2.x

## FAQ

### Is Cryptlex v3.x a new product?

Yes, it's a completely new product. Everything has been rewritten using the latest and some of the best technologies available.

* Completely [API](https://api.cryptlex.com/v3/docs) driven
* Brand new [dashboard](https://app.cryptlex.com)
* New beautiful [documentation](https://docs.cryptlex.com) 
* New client libraries
* New hosting provider \([Heroku](https://heroku.com)\)
* Code samples have been moved to [Github](https://github.com/cryptlex)
* Updated [pricing plans](https://cryptlex.com/pricing)

{% hint style="info" %}
Cryptlex v3.x is not backward compatible with Cryptlex v2.x.
{% endhint %}

### Can I login using my existing credentials?

No, you need to create a new account for using Cryptlex v3.x.

### How long do you plan to support Cryptlex v2.x?

We are planning to support it for one year \(upto May 2019\), after which the accounts will become read only, i.e. you won't be allowed to create more products, product versions, product keys etc.

### What about our existing customers who will still be using Cryptlex v2.x after one year?

Don't worry activation and deactivation API endpoints will still work after one year. Cryptlex v2.x won't be retired unless we reach zero traffic on Cryptlex v2.x servers.

### Do our customers need to reactivate when we integrate LexActivator v3.x or upgrade to LexFloatServer v3.x?

Yes, a reactivation will be required. You can do an auto-activation if you store the key in your application settings and after upgrade check whether key exists and do an auto-activation.

### If I subscribe to a paid plan on Cryptlex v3.x will I be charged for Cryptlex v2.x?

No, when you subscribe to any paid plan on Cryptlex v3.x your Cryptlex v2.x account subscription will get discounted by the amount you pay for your subscription. Please notify us when you do so.

## What's new in Cryptlex v3.x?

A lot has changed and many new features have been added. Most of the feature requests by our customers have made into Cryptlex v3.x, we thank you for your valuable feedback.

### REST Web API

Everything is now API driven in Cryptlex. You can even skip using LexActivator \(though not recommended\) and directly use web API to license your products.

### User identity management

We now support identity management for your customers. Along with creating licenses you can also create users and link them with the licenses. Basic features like login, password reset, profile management are supported out of the box.

{% hint style="info" %}
Customer portal where your customers can self manage their licenses is coming soon...
{% endhint %}

### License policies

A license policy helps you create different types of license profiles. It acts as a blueprint for the licenses you create for your customers and helps you implement different types of licensing models.

### Hosted floating licenses

Now you can simply use LexActivator for implementing floating licenses where Cryptlex server acts as your floating license server. So you get to see activation log in real time for your floating licenses.

### Audit log

Every action is logged and you can easily view the event log in the dashboard. Logs are retained for 30 days.

{% hint style="info" %}
Additionally, activation log of your licenses is also available which can be used to audit license usage.
{% endhint %}

### Webhooks

You can now easily integrate Cryptlex with third party apps and take actions when some event occurs in your Cryptlex account. You can even use [Zapier](https://zapier.com/) and integrate Cryptlex with thousands of cloud apps.

### Metadata

Cryptlex v2.x allowed for storing custom fields with your licenses. This has been replaced with metadata which can be stored along with your products, licenses, users, activations and trial activations.

{% hint style="info" %}
You can use product metadata to easily detect software updates in your app by storing your release version. After trial or license activation product metadata can be accessed in your app.
{% endhint %}

### Analytics

Analytics have been improved and we are adding more metrics to further give you detailed insight of your products.

### Updated LexActivator

LexActivator has gone through major upgrade and now supports a lot many new features. You can checkout the [changelog](https://docs.cryptlex.com/changelog/lexactivator).

### Other features

To keep it short we won't be discussing all the features, if you have any queries drop an [email](mailto:support@cryptlex.com) and our team will reach out to you.

## How to migrate to Cryptlex v3.x?

### Exporting license keys from Cryptlex v2.x

You can easily export the license keys in csv format from the Cryptlex v2.x dashboard. The exported csv data needs to be processed a bit before it can be imported into Cryptlex v3.x. It looks as follows:

`"Key ID", "Product Key", "Email", "Status", "Expires On", "Total Activations", "Used Activations", "Total Deactivations", "Used Deactivations", "Creation Date", "Custom Fields", "Activation Location","Activation Date","Activation Extra Data","Activation OS"`

 Remove the fields which can't be imported so it will become:

`"Product Key", "Email", "Total Activations", "Total Deactivations","Custom Fields"`

Rename the fields as per the new schema:

`"key", "email", "allowedActivations", "allowedDeactivations","Custom Fields"`

Each custom field should be added as a separate field, assuming you had stored order\_id_, _first\_name_,      _last\_name:

`"key", "email", "allowedActivations", "allowedDeactivations","order_id", "first_name", "last_name"`

### Importing CSV data into Cryptlex v3.x

We have created a sample project on [Github](https://github.com/cryptlex/csv-importer) to help you with the import. It's a Node.js script which you can modify as per your requirements.

You need to decide whether you want to store the user data as separate user resource or simply store it as part of license metadata. The script uses user data to create a new user and links the user with the license. You can modify the script as per your requirements.

The script invokes Cryptlex v3.x Web API, so you will need an access token to use the script. Go the "[Personal Access Tokens](https://app.cryptlex.com/api/personal-access-tokens)" section in dashboard and create an access token with following four permissions:

`license:read`, `license:write`, `user:read`, `user:write`

In case you need more help, we'll be glad to help you make the transition. You can either post your questions on our [support forum](https://cryptlex.com/forums) or can contact us through [email](mailto:support@cryptlex.com?Subject=Importing%20CSV).



