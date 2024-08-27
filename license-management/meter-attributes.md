# Meter Attributes

Sometimes you want your customers to pay for what is actively used regardless of how long they possess your product. The usage can be defined as the number of specific operations in your app, the number of times it is run, the number of times any feature is used, etc.

## Meter attribute properties

The meter attributes can be added to the licenses and have the following properties:

#### Name

Name of the meter attribute.

#### Allowed Uses

The maximum allowed uses for the attribute.

#### Total Uses

The current uses for the attribute. Its value can be incremented, decremented, or reset in your app using LexActivator functions.

#### Gross Uses

This property keeps track of the lifetime usage of the meter attribute.

#### Floating

If set to true then the uses consumed by the activation will auto-reset if the activation is deleted.

#### View Permissions

Admins can control the visibility of meter attributes for different users by configuring the meter attribute permissions as follows:

• **Activation**: Meter attributes will be accessible to developers in the LexActivator SDK (and via Web API through the `POST v3/activations` endpoint).

• **User**: Meter attributes will be visible to users within the customer portal (and via Web API through the `v3/me/licenses` endpoint).

• **Organization**: Meter attributes will be visible to the organization-admins in the customer portal (and via Web API through the `v3/organizations/:id/licenses` endpoint).

• **Reseller**: Meter attributes will be visible to reseller-admins in the reseller portal (and via Web API through the `v3/resellers/:id/licenses` endpoint).

## Enforcing meter attributes schema

You can easily make some meter attributes required for your licenses by adding them to the **requiredMeterAttributes** property of the license template. This also automatically creates the meter attributes in the license form.

## Using meter attributes

After you have created meter attributes for the license, you can easily get, increment, decrement, and reset the usage count of the meter attributes in your app using the following LexActivator functions:

**`GetActivationMeterAttributeUses()`**, **`IncrementActivationMeterAttributeUses()`**, **`DecrementActivationMeterAttributeUses()`**, **`ResetActivationMeterAttributeUses()`**

When the usage count reaches the `allowedUses` limit, further incrementing the usage count will return **`LA_E_METER_ATTRIBUTE_USES_LIMIT_REACHED`** error code.
