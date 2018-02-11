## Switching your Licensing to Cryptlex

You can easily switch from your current licensing solution to Cryptlex. The method is pretty simple and mainly involves importing of your old licensing data into Cryptlex.



### Step 1. Importing your old licensing data into Cryptlex

The first step in the transition is to export your old licensing data to a CSV file, which will be imported into cryptlex to generate new product keys with associated data for your existing customers.

#### Create Custom License Fields

Your old licensing data might contain some additional info associated with each key. Suppose, for each key you store "Order Id","First Name" and "Last Name". So, before importing your license data you need to make sure you have created a custom license field for each of the above fields.[Know more about custom fields here.](https://cryptlex.com/help/custom-fields)

[![](https://cryptlex.com/public/img/docs/create-custom-fields.png "create-custom-fields")](https://cryptlex.com/public/img/docs/create-custom-fields.png)

Ideally, for each column in your CSV file, you will create a custom license field except for the following five fields which are present by default:

Email, License Validity, Product Key Type, Allow VM Activation, Total Activations per Key



#### Importing old licensing data

After you are done with creating the custom license fields, click the "Import Keys" button on the product version page.

[![](https://cryptlex.com/public/img/docs/import-pkeys.png "import-pkeys")](https://cryptlex.com/public/img/docs/import-pkeys.png)

Open your CSV file in any text editor and paste the header into the "License Schema" text area on the import keys page.

[![](https://cryptlex.com/public/img/docs/add-schema.png "add-schema")](https://cryptlex.com/public/img/docs/add-schema.png)

Now, match your CSV column fields with the fields provided in the "Match the fields" section. You can also set a default value for any field in case it is not present in your old licensing data.

[![](https://cryptlex.com/public/img/docs/match-fields.png "match-fields")](https://cryptlex.com/public/img/docs/match-fields.png)

Now, upload your CSV file and click the "Import Product Keys" button

### Step 2. Activating next version of your app

Your next version will be using LexActivator for online activation. So, you need to provide the new license keys to your existing customers. You can email the new keys to your existing customers \(can be automated using Lex Web API\) or write logic for fetching the new key on detection of some info \( like an old key or customer email\) in your app itself so that your users don't even know about the switch.

In case you want to write logic for fetching the new key on detection of some info in your app, you can use Lex Web API. For that you need to make sure that info was imported into cryptlex. Suppose, that info is customer email stored in your app. You can use web API to get the new license key associated with the email and automatically activate the app.

### Need more help?

In case you need more help for transitioning from your current licensing solution to Cryptlex we'll be glad to help you make the transition. You can either post your questions on our [support forum](https://cryptlex.com/forums)or can contact us through[email](mailto:support@cryptlex.com?Subject=Switching%20to%20Cryptlex).

