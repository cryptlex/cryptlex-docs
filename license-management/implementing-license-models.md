# Implementing License Models

You can easily implement any licensing model using license policies, or by overriding the properties of the license policy when creating a license. The later allows you create a variant without creating a new policy.

## License policy configuration for different licensing models

Each licensing model you want to implement may require a different license policy configuration. We will now list the license policy configuration for implementing the different licensing models. You may combine different configurations to implement your licensing model.

### Perpetual

A perpetual license has lifetime validity.

| Property | Value | Comments |
| :--- | :--- | :--- |
| **`validity`** | `0` |  |

### Subscription

A subscription expires after a specific duration of time. When a license expires, LexActivator will return `LA_EXPIRED` status code.

| Property | Value | Comments |
| :--- | :--- | :--- |
| **`validity`** | `>0` |  |

### Node-locked

A node-locked license is bound to a machine on which the license was activated. It means that the license key cannot be re-used on any other machine \(if license allows a single activation/seat\).

If license allows multiple activations \(multi-seat\), then after all the activations are used, the license key cannot be used on other machines.

| Property | Value | Comments |
| :--- | :--- | :--- |
| **`type`** | `node-locked` | \`\` |

### User-locked

A user-locked license is essentially a node-locked license only. It just ensures that different users \(OS users\) on the same machine are prevented from re-using the same license. 

| Property | Value | Comments |
| :--- | :--- | :--- |
| **`type`** | `node-locked` | \`\` |
| **`userLocked`** | `true` |  |

### Hosted-floating

A floating license is temporarily bound to a machine for a specific amount of time. When the time expires the activation \(seat\) is automatically freed up \(if not renewed\), so that any other machine can use the license.

Hosting-floating option lets you implement floating licensing model without requiring your customer to install a floating server in it's network.

| Property | Value | Comments |
| :--- | :--- | :--- |
| **`type`** | `hosted-floating` | \`\` |
| **`leaseDuration`** | `>0` | \`\` |
| **`leasingStrategy`** | `per-machine` | \`\` |

### Hosted-floating \(instance-locked\)

Instead of temporarily locking a floating license to a machine for a specific amount of time, you can also bound it to the application instance \(process\). 

This is useful in case your app is running inside a VM \(which can be cloned\) or Docker \(and you want to charge your customer for each instance\). 

| Property | Value | Comments |
| :--- | :--- | :--- |
| **`type`** | `hosted-floating` | \`\` |
| **`leaseDuration`** | `>0` |  |
| **`leasingStrategy`** | `per-instance` |  |

### On-premise-floating

A floating license is temporarily bound to a machine for a specific amount of time. When the time expires the activation \(seat\) is automatically freed up \(if not renewed\), so that any other machine can use the license.

On-premise-floating option lets you implement floating licensing model in environments which may or may not be connected to internet. Your customer is required to install LexFloatServer in its own network. The number of floating licenses the on-premise LexFloatServer can lease is determined by the `allowedFloatingClients` property.

| Property | Value | Comments |
| :--- | :--- | :--- |
| **`type`** | `on-premise-floating` |  |
| **`leaseDuration`** | `0`, `>0` |  |
| **`allowedFloatingClients`** | `>0` | \`\` |

### Single-seat

The number of machines a license key can be used on is determined by the `allowedActivations` property.

| Property | Value | Comments |
| :--- | :--- | :--- |
| **`allowedActivations`** | `1` | \`\` |
| **`type`** | `node-locked`, `hosted-floating` |  |

### Multi-seat

A single key can be used on multiple machines, if the value of `allowedActivations` property is greater than one.

| Property | Value | Comments |
| :--- | :--- | :--- |
| **`allowedActivations`** | `>1` |  |
| **`type`** | `node-locked`, `hosted-floating` |  |

### Unlimited-seat

You can allow an unlimited number of seats for a license \(site license\), and restrict the site using IP address or location.

| Property | Value | Comments |
| :--- | :--- | :--- |
| **`allowedActivations`** | `0` |  |
| **`type`** | `node-locked`, `hosted-floating` |  |
| **`allowedIpAddresses`** | `[125.67.123.43]` |  |

### Named-user

A license activation only requires a license key. In case you want to enforce user authentication for license activation, you can set `requireAuthentication` property to `true`.

This also requires linking the user to the license at the time of license creation.

| Property | Value | Comments |
| :--- | :--- | :--- |
| **`type`** | `hosted-floating` | \`\` |
| **`leasingStrategy`** | `per-instance` | \`\` |
| **`leaseDuration`** | `>0` | \`\` |
| **`requireAuthentication`** | `true` |  |

