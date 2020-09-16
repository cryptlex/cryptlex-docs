# Meter Attributes

Sometimes you want your customers to pay for what is actively used regardless of how long they possess your product. The usage can be defined as number of specific operations in your app, number of times it is run, number of times any feature is used etc.

## Meter attribute properties

The meter attributes can be added to licenses and have the following properties:

#### Name

Name of the meter attribute.

#### Allowed Uses

The maximum allowed uses for the attribute.

#### Total Uses

The current uses for the attribute. Its value can be incremented, decremented, or reset in your app using LexActivator functions.

#### Gross Uses

This property keeps track of lifetime usage of the meter attribute. When a license activation is deleted, the uses consumed by the activation are automatically decremented from the license total uses. So, this property can be used to keep track of gross uses even if activations are deleted.

## Enforcing meter attributes schema

You can easily make some meter attributes required for your licenses by adding them to the **requiredMeterAttributes** property of the license policy. This also automatically creates the meter attributes in the license form.

## Using meter attributes

After you have created meter attributes for the license, you can easily get, increment, decrement and reset the usage count of the meter attributes in your app using following LexActivator functions:

**`GetActivationMeterAttributeUses()`**, **`IncrementActivationMeterAttributeUses()`**, **`DecrementActivationMeterAttributeUses()`**, **`ResetActivationMeterAttributeUses()`**

When the usage count reaches the **allowedUses** limit, further incrementing the usage count will return **`LA_E_METER_ATTRIBUTE_USES_LIMIT_REACHED`** error code.

