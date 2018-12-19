# Welcome to Cryptlex!

Cryptlex lets you license your software apps effortlessly. You can easily generate license keys using our [REST API](https://api.cryptlex.com/v3/docs) or through [dashboard](https://app.cryptlex.com/) and validate the license keys in your software apps using [LexActivator](https://docs.cryptlex.com/node-locked-licenses/overview) \(Cryptlex client library\).

## Quick start

The complete process of adding licensing to your software app has three steps:

### Step 1. Add a product in Cryptlex

Log in to the Cryptlex [dashboard](https://app.cryptlex.com/). Click the "Products" link in the sidebar and add your first product. You will need to create a default [license policy](https://docs.cryptlex.com/license-management/license-policies) too for the product. After creating the product select the "Licenses" link in the the products table and create your first license key.

### Step 2. Adding LexActivator to your Product

LexActivator is the Cryptlex client library which you will use to add licensing to your product. Using this library you can easily validate the license key in your software app. It is a shared library available for all the major platforms - Windows, Mac OS X and Linux. The library can be used with almost all the programming languages. To learn more refer to:

{% page-ref page="node-locked-licenses/using-lexactivator/" %}

### Step 3. Using Cryptlex Web API to automate order process

You can use the [web API](https://api.cryptlex.com/v3/docs) to automate your order processes by generating new license keys when an order is processed through your payment processor. The web API can be used with any payment processor to generate license keys when an order is processed. To learn more refer to:

{% page-ref page="web-integration/" %}



