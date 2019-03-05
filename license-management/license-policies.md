# License Policies

A license policy acts as a template \(blueprint\) for the licenses you create for your customers. Before you start creating licenses, you need to create a license policy which would contain the default values for the fields of any license.

While creating a license from any license policy, you can override all the properties of the license policy. License policy provides you with defaults values for all the properties of a license, so you don't have to provide them every time you create a new license.

## Creating a license policy

You can easily create a license policy through dashboard. Go to the [license policies](https://app.cryptlex.com/license-policies) section in the dashboard and click the add the button. A license policy form with following fields will popup: 

#### Name

The name of the license policy.

#### Validity

The duration \(in seconds\) after which the license will expire.

{% hint style="info" %}
To create a **perpetual** license set the validity to zero and for **subscriptions** set it to any value greater than zero.
{% endhint %}

#### Type

There are three types of licenses:

* **Node locked:** This is the default type which locks the license to the machine.
* **Hosted Floating:** This type is used for creating a hosted floating license.
* **On-Premise floating:** This ****type is used for creating an on-premise floating license.

#### Lease duration

This option is valid for **hosted-floating** and **on-premise-floating** license types only. It sets the duration for which you want to lease the floating license.

{% hint style="info" %}
In case of **hosted-floating** license type,  if you want license lease to auto renew then ensure that the **server sync interval is less than lease duration** by a difference of around 30 seconds.
{% endhint %}

{% hint style="info" %}
In case of **on-premise** license type, lease duration can be set to 0 to honour the lease duration set in LexFloatServer config file.
{% endhint %}

#### Leasing Strategy

This option is valid for **on-premise-floating** license type only. It allows for following strategies:

**Per-Machine:** Each machine will only lease a single floating license, irrespective of the number of floating client instances being run on the machine.

**Per-Instance:** Each instance of the floating client will lease a separate floating license, irrespective of whether the instances are running on a single machine or different machines.

#### Allowed floating clients

This option is valid for **on-premise** **floating** license type only. It sets the maximum number of concurrent clients which can lease the floating license from the server.

{% hint style="info" %}
For hosted floating licenses, the maximum number of concurrent clients which can lease the license from the server is determined by **allowedActivations** property
{% endhint %}

#### Allowed activations

Allowed number of activations \(seats\) for the license. If you allow \(say\) 10 activations for a license, then the license can be used on 10 different machines.

#### Allowed deactivations

Allowed number of deactivations for the license. This setting is ignored for **hosted-floating** licenses.

#### Server sync interval

Whenever the application starts \(and `IsProductGenuine()` is called first time\), the server sync occurs immediately in a separate thread. This setting determines the interval for further server syncs till the application is not closed.

{% hint style="info" %}
The minimum allowed server sync interval upto STARTUP plan is 3600 seconds, and for higher plans it is 180 seconds. It is highly recommended to set it to 3600 or greater unless required.
{% endhint %}

#### Server sync grace period

The duration for which the server sync failure due to network error is acceptable.

#### Allowed clock offset

The allowed difference between the network time and the system time. This can be used to allow license activations on machines where system clocks run behind the network time.

#### Expiration strategy

The strategy to determine the expiration start date. It allows for following strategies:

**Immediate:** The license starts expiring right after the it is created.

**Delayed:** The license starts expiring after the license is activated first time. If the license allows more than one activation then all the other activations will also start expiring right after the first activation of the license.

**Rolling:** The license starts expiring after the license is activated. If the license allows more than one activation even then all the activations will start expiring after they are activated.

{% hint style="info" %}
You may not allow license deactivations if **rolling** expiration strategy is being used, as it would reset the expiry.
{% endhint %}

#### Fingerprint matching strategy

LexActivator generates a structured fingerprint of the machine which allows for multiple fingerprint matching strategies. It allows for following strategies:

**Exact:** This strategy requires an exact match of all the hardware parts which were fingerprinted. If their is a minor change in the hardware, fingerprint will not be accepted, and machine will be treated as a different machine.

**Fuzzy:**  This strategy uses fuzzy matching by comparing different hardware fingerprints and if the comparison score is greater than a minimum threshold value, the machine is accepted. This is the **recommended** strategy.

**Loose:** This strategy is similar to fuzzy but with a much lower threshold value.

{% hint style="info" %}
Sometimes few machines misbehave by reporting major changes in hardware fingerprints due to many issues, in such cases you should change the strategy to **"Loose"**.
{% endhint %}

#### Required Metadata Keys

List of required metadata keys which a license inheriting the policy must have.

#### Allowed countries

List of the allowed countries. The country name is resolved using the IP address. If none of the countries is included, this setting is ignored.

#### Disallowed countries

List of the disallowed countries. The country name is resolved using the IP address. If none of the countries is included, this setting is ignored.

#### Allowed IP addresses

List of the allowed IP addresses. If none of the IP addresses is included, this setting is ignored.

#### Disallowed IP addresses

List of the disallowed IP addresses. If none of the IP addresses is included, this setting is ignored.

#### Allow VM activations

Whether to allow an activation inside a virtual machine. Cloned virtual machines may report a same fingerprint.

#### User locked

It prevents users from using the same license key in a machine for different user accounts.

