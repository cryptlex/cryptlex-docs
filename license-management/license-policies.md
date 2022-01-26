# License Policies

A license policy acts as a template (blueprint) for the licenses you create for your customers. Before you start creating licenses, you need to create a license policy that would contain the default values for the fields of any license.

While creating a license from any license policy, you can override all the properties of the license policy. License policy provides you with default values for all the properties of a license, so you don't have to provide them every time you create a new license.

## Creating a license policy

You can easily create a license policy through the dashboard. Go to the [license policies](https://app.cryptlex.com/license-policies) section in the dashboard and click the add the button. A license policy form with the following fields will popup:&#x20;

### Name

The name of the license policy.

### Validity

The duration (in seconds) after which the license will expire.

{% hint style="info" %}
To create a **perpetual** license set the validity to zero and for **subscriptions** set it to any value greater than zero.
{% endhint %}

### Type

There are three types of licenses:

* **Node-locked:** This is the default type that locks the license to the machine.
* **Hosted Floating:** This type is used for creating a hosted floating license.
* **On-Premise floating:** This **** type is used for creating an on-premise floating license.

### Lease duration

This option is valid for **hosted-floating** and **on-premise-floating** license types only. It sets the duration for which you want to lease the floating license.

{% hint style="info" %}
In case of **hosted-floating** license type,  if you want the license lease to auto-renew then ensure that the **server sync interval is less than lease duration** by a difference of atleast 30 seconds.
{% endhint %}

{% hint style="info" %}
In the case of **on-premise** license type, lease duration can be set to 0 to honor the lease duration set in the **LexFloatServer** config file.
{% endhint %}

### Leasing strategy

This option is valid for **on-premise-floating** and **hosted-floating** license types only. It allows for the following strategies:

#### **Per-Machine:**&#x20;

Each machine will only consume a single floating license/activation, irrespective of the number of instances (processes) of your app being run on the machine.

#### **Per-Instance:**&#x20;

Each instance (process) of your app will consume a separate floating license/activation, irrespective of whether the instances are running on the same machine or different machines.

{% hint style="info" %}
In case of **hosted-floating** license type,  if you want to use a **per-instance** leasing strategy, ensure that the permission flag in the **LexActivator** `SetProductId()` function is set to `LA_IN_MEMORY`.
{% endhint %}

### Allowed floating clients

This option is valid for **on-premise** **floating** license type only. It sets the maximum number of concurrent clients that can lease the floating license from the server.

{% hint style="info" %}
For hosted floating licenses, the maximum number of concurrent clients that can lease the license from the server is determined by **allowedActivations** property
{% endhint %}

### Allowed activations

Allowed number of activations (seats) for the license. If you allow (say) 10 activations for a license, then the license can be used on 10 different machines.

### Allowed deactivations

Allowed number of deactivations for the license. This setting is ignored for **hosted-floating** licenses.

### Server sync interval

Whenever the application starts (and`IsLicenseGenuine()` is called the first time), the server sync occurs immediately in a separate thread. This setting determines the interval for further server syncs till the application is not closed.

{% hint style="info" %}
The minimum allowed server sync interval up to the STARTUP plan is 3600 seconds, and for higher plans, it is 180 seconds. It is highly recommended to set it to 3600 or greater unless required.
{% endhint %}

### Server sync grace period

The duration for which the server sync failure due to network error is acceptable. In order to allow an infinite grace period, this property can be set to "0".

### Allowed clock offset

The allowed difference between the network time and the system time. This can be used to allow license activations on machines where system clocks run behind the network time.

### Expiration strategy

The strategy to determine the expiration start date. It allows for the following strategies:

#### **Immediate:**&#x20;

The license starts expiring right after it is created.

#### **Delayed:**&#x20;

The license starts expiring after the license is activated the first time. If the license allows more than one activation then all the other activations will also start expiring right after the first activation of the license.

#### **Rolling:**&#x20;

The license starts expiring after the license is activated. If the license allows more than one activation even then all the activations will start expiring after they are activated.

{% hint style="info" %}
You may not allow license deactivations if a **rolling** expiration strategy is being used, as it would reset the expiry.
{% endhint %}

### Fingerprint matching strategy

LexActivator generates a structured fingerprint of the machine which allows for multiple fingerprint matching strategies. It allows for the following strategies:

#### **Exact:**&#x20;

This strategy requires an exact match of all the hardware parts which were fingerprinted. If there is a minor change in the hardware, the fingerprint will not be accepted, and the machine will be treated as a different machine.

#### **Fuzzy:** &#x20;

This strategy uses fuzzy matching by comparing different hardware fingerprints and if the comparison score is greater than a minimum threshold value, the machine is accepted. This is the **recommended** strategy.

#### **Loose:**&#x20;

This strategy is similar to fuzzy but with a much lower threshold value.

{% hint style="info" %}
Sometimes few machines misbehave by reporting major changes in hardware fingerprints due to many issues, in such cases, you should change the strategy to **"Loose"**.
{% endhint %}

### Required metadata keys

List of required metadata keys that a license inheriting the policy must-have.

### Required meter attributes

List of required meter attributes which a license inheriting the policy must-have.

### Expiring soon event offset

The number of seconds to wait before the license expiration date to trigger the `license.expiring-soon` webhook event.

### Key pattern

Regex for the license key format. The default regex is `^([A-F0-9]{6}-){5}[A-F0-9]{6}$`  which generates the license keys in the format:`XXXXXX-XXXXXX-XXXXXX-XXXXXX-XXXXXX-XXXXXX`

### Allowed countries

List of the allowed countries. The country name is resolved using the IP address. If none of the countries is selected, then all the countries are allowed.

### Disallowed countries

List of the disallowed countries. The country name is resolved using the IP address. If none of the countries is selected, this setting is ignored.

### Allowed IP range

IP address range in CIDR notation e.g. **196.210.135.105/24**. If no range is specified, then all the IP addresses are allowed.

### Allowed IP addresses

List of the allowed IP addresses. If none of the IP addresses is included, then all the IP addresses are allowed.

### Disallowed IP addresses

List of the disallowed IP addresses. If none of the IP addresses is included, this setting is ignored.

### Allow VM activations

Whether to allow an activation inside a virtual machine. Cloned virtual machines may report the same fingerprint.

### Allow Container activations

Whether to allow an activation inside a container. This must never be set to `true` for an **on-premise floating** license.&#x20;

### Allow Client Lease Duration

Whether to allow the client app to set the lease duration for the hosted-floating license activation.

### User locked

It prevents multiple users inside an OS from using the same license key. If enabled, each user will consume a license activation from the allowed number of activations for a license.

### Require authentication

In case you want to enforce user authentication for license activation in addition to the license key, you can set this property to `true`.

### Disable geolocation

In case you don't want to store the IP address and location of the license activation, you can set this property to `true`.

### Disable clock validation

In case the machine which is to be licensed doesn't have a hardware clock and can't keep the correct time you can set this property to `true`. This will only work in the case of node-locked license and validity should also be set to `0`.
