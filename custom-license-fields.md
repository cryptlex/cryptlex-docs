Using custom fields you can store additional license data alongside product keys. This can include additional information about customers \(e.g. their name, company etc.\), additional options to enable or disable specific features in your application etc. An unlimited number of custom fields can be associated with a product key.

### Adding a Custom License Field

On the "Products" page, click "Custom Fields" under your product version.

[![](https://cryptlex.com/public/img/docs/products.png "products")](https://cryptlex.com/public/img/docs/products.png)

On the "Custom Fields" page, click "Plus symbol" button and fill in all the values in the fields created in the custom fields table.

[![](https://cryptlex.com/public/img/docs/add-custom-field.png "add-custom-field")](https://cryptlex.com/public/img/docs/add-custom-field.png)

![](/assets/4.PNG)

**Name :** This is the name of the custom field.

**Required : **Choosing if the field is necessarily required to be filled or not**.**

**Accessible :** Once user activates your app the field data is accessible to you in the app. On activation, encrypted fields data is sent along with signed activation data. So, after user has activated your app, you can use LexActivator API function GetCustomLicenseField\(\) to access the field value.

### Using a Custom License Field

Once you have created a license field, it will appear in the "Add Key" dialog where it can be filled when generating a product key. Alternately, it can be passed in the Web API when generating a key.

[![](https://cryptlex.com/public/img/docs/use-custom-field.png "use-custom-field")](https://cryptlex.com/public/img/docs/use-custom-field.png)

### Updating a Custom License Field and getting changes in your application

Whenever you change the field data for a product key either within your Cryptlex dashboard or using the web API, then updated data will automatically be accessible to you in your app, when your customer re-activates or`IsProductGenuine()`function \(periodically\) checks with Cryptlex servers.

