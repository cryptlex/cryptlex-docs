# Implementing License Models

You can easily implement any licensing model using license templates, or by overriding the properties of the license template when creating a license. The latter allows you to create a variant without creating a new template.

## License template configuration for different licensing models

Each licensing model you want to implement may require a different license template configuration. We will now list the license template configuration for implementing the different licensing models. You may combine different configurations to implement your licensing model.

### Perpetual

A perpetual license has lifetime validity.

| Property       | Value |
| -------------- | ----- |
| **`validity`** | `0`   |

### Subscription

A subscription expires after a specific duration of time. When a license expires, LexActivator will return `LA_EXPIRED` status code.

| Property       | Value |
| -------------- | ----- |
| **`validity`** | `>0`  |

### Node-locked

A node-locked license is bound to a machine on which the license was activated. It means that the license key cannot be re-used on any other machine (if the license allows a single activation/seat).

If the license allows multiple activations (multi-seat), then after all the activations are used, the license key cannot be used on other machines.

| Property   | Value         |
| ---------- | ------------- |
| **`type`** | `node-locked` |

### User-locked

A user-locked license is essentially a node-locked license only. It just ensures that different users (OS users) on the same machine are prevented from re-using the same license.&#x20;

| Property         | Value         |
| ---------------- | ------------- |
| **`type`**       | `node-locked` |
| **`userLocked`** | `true`        |

### Hosted-floating

A floating license is temporarily bound to a machine for a specific amount of time. When the time expires the activation (seat) is automatically freed up (if not renewed), so that any other machine can use the license.

Hosting-floating option lets you implement a floating licensing model without requiring your customer to install a floating server in its network.

| Property              | Value             |
| --------------------- | ----------------- |
| **`type`**            | `hosted-floating` |
| **`leaseDuration`**   | `>0`              |
| **`leasingStrategy`** | `per-machine`     |

### Hosted-floating (instance-locked)

Instead of temporarily locking a floating license to a machine for a specific amount of time, you can also bind it to the application instance (process).&#x20;

This is useful in case your app is running inside a VM (which can be cloned) or Docker (and you want to charge your customer for each instance).&#x20;

| Property              | Value             |
| --------------------- | ----------------- |
| **`type`**            | `hosted-floating` |
| **`leaseDuration`**   | `>0`              |
| **`leasingStrategy`** | `per-instance`    |

### On-premise-floating

A floating license is temporarily bound to a machine for a specific amount of time. When the time expires the activation (seat) is automatically freed up (if not renewed), so that any other machine can use the license.

The on-premise-floating option lets you implement a floating licensing model in environments which may or may not be connected to the internet. Your customer is required to install LexFloatServer in its network. The number of floating licenses the on-premise LexFloatServer can lease is determined by the `allowedFloatingClients` property.

| Property                     | Value                 |
| ---------------------------- | --------------------- |
| **`type`**                   | `on-premise-floating` |
| **`leaseDuration`**          | `0`, `>0`             |
| **`allowedFloatingClients`** | `>0`                  |

### Single-seat

The number of machines a license key can be used on is determined by the `allowedActivations` property.

| Property                 | Value                            |
| ------------------------ | -------------------------------- |
| **`allowedActivations`** | `1`                              |
| **`type`**               | `node-locked`, `hosted-floating` |

### Multi-seat

A single key can be used on multiple machines if the value of `allowedActivations` property is greater than one.

| Property                 | Value                            |
| ------------------------ | -------------------------------- |
| **`allowedActivations`** | `>1`                             |
| **`type`**               | `node-locked`, `hosted-floating` |

### Unlimited-seat

You can allow an unlimited number of seats for a license (site license), and restrict the site using an IP address or location.

| Property                 | Value                            |
| ------------------------ | -------------------------------- |
| **`allowedActivations`** | `0`, `-1`                        |
| **`type`**               | `node-locked`, `hosted-floating` |
| **`allowedIpAddresses`** | `[125.67.123.43]`                |

### Named-user

A license activation only requires a license key. In case you want to enforce user authentication for license activation, you can set `requireAuthentication` property to `true`.

This also requires linking the user to the license at the time of license creation.

| Property                    | Value             |
| --------------------------- | ----------------- |
| **`type`**                  | `hosted-floating` |
| **`leasingStrategy`**       | `per-instance`    |
| **`leaseDuration`**         | `>0`              |
| **`requireAuthentication`** | `true`            |
