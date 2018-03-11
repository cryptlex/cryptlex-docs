## Product

End-user organizations can control where and how  products are able to run.

### Product Versions

Each product has a product version which  constitutes of following :

![](/assets/3.PNG)

#### Name

This includes the name of your product version.

#### App Version

This includes values for the product version information.

App Version should be set to the latest version of your software. This value is accessible and can be used to detect software updates.

### Product Keys Settings

The product key consists of following settings:

![](/assets/1.PNG)

#### Validity

The number of days after which the product gets expired.

#### Type

There are two types of product key

* **Node-locked**: This is the default type which locks the product key to the machine.

* **Floating** : This type is used for LexFloatServer.

#### Allowed Activations

Total number of activations allowed per user.

#### Allowed Deactivation

Total number of deactivations allowed per user.

#### Server sync Interval

Whenever the application starts, the server sync occurs immediately. This setting determines the interval for further server syncs if the application is not closed.

#### Grace Period

It determines the number of days for which the server sync failure due to network error is acceptable.

#### Expiration Strategy

The time after which the product key starts count of expiry . Its of three types:

* **Immediate : **The product key starts expiring right after the product key is created.
* **Delayed : **The product key starts expiring after the product key is activated first time. 
  * If the product allows more than one activation then all the other activations will also start expiring right after the first activation of the product key.
* **Rolling : **The product key starts expiring after the product key is activated.
  * ** **If the product key allows more than one activation,all the other activations of the product key will start expiring right after they are activated.
  * If any of the activation of the product key is deactivated, the expiry date of that activation  will start from the day its reactivated.

#### Fingerprint Matching Strategy

This includes how the fingerprints will be compared. Its of three types:

* **Exact : **There should be an exact match of the hardwares of the machine. If their is a minor change in the hardware, fingerprints will not be accepted.
* **Fuzzy :**
* **Loose : **If any of the hardware is matched, the fingerprint is accepted.

#### Allowed Floating Clients

Total number of floating clients allowed.

#### Allowed Countries

Product allowed in the countries. If none of the country is included, the setting is ignored.

#### Disallowed Countries

Product not allowed in the countries.

#### Allow VM Activations

It prevents licenses from working on cloned virtual machines.

#### Enable User Lock

It prevents users from using the same key in a machine with the same fingerprint.

### Trial Settings

It consists of following settings:

![](/assets/Capture.PNG)

#### Trial Length

The number of days after which the trial is expired.

