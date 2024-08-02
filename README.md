# Welcome to Cryptlex!

Cryptlex lets you license your software apps effortlessly. You can easily generate license keys using our [REST API](https://api.cryptlex.com/v3/docs) or through the [admin portal](https://app.cryptlex.com) and validate the license keys in your software apps using [LexActivator](https://docs.cryptlex.com/node-locked-licenses/overview) (Cryptlex client library).&#x20;

The license keys can't be shared by your customers because they are node-locked (locked to the machine where they are activated), hence preventing casual piracy.

## Quick start

The complete process of adding licensing to your software app has three steps:

### Step 1. Add a product in Cryptlex

Log in to the Cryptlex [admin portal](https://app.cryptlex.com). Click the `Home -> Products` link in the sidebar and add your first product. You will need to create a default [license template](license-management/license-templates.md) too for the product. After creating the product click the `Licenses` link in the sidebar and create your first license.

### Step 2. Adding LexActivator to your software app

LexActivator is the Cryptlex client library which you will use to add licensing to your product. Using this library you can easily validate the license key in your software app. It is a shared library available for all the major platforms - Windows, macOS and Linux. The library can be used with almost all programming languages. To learn more refer to:

{% content-ref url="node-locked-licenses/using-lexactivator/" %}
[using-lexactivator](node-locked-licenses/using-lexactivator/)
{% endcontent-ref %}

### Step 3. Using Cryptlex Web API to automate the order process

You can use the [web API](https://api.cryptlex.com/v3/docs) to automate your order processes by generating new licenses when an order is processed through your payment processor. The web API can be used with any payment processor to generate licenses when an order is processed. To learn more refer to:

{% content-ref url="web-integration/" %}
[web-integration](web-integration/)
{% endcontent-ref %}

