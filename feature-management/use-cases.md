# Use Cases

Some of the numerous cases in which our feature management suite can be used are:

* Entitlements within Software
* Testing
* Changes without Deployment
* Value-based changes

## **Entitlements within software**

Creating `Feature Flags` for functionality you want to control among product flavours allows for hassle-free management. Example: When shipping your software, you want to have three variants: Lite, Pro, and Max with different features. For each variant, you can easily create a `Product Version` and within the `Product Version`, features defined by the `Feature Flags` can be enabled or disabled.

SaaS plans like `Basic`, `Pro`, `Enterprise` etc. can also be maintained using Product Versions.

## **Testing**

The creation of different `Product Versions` allows you to test new functionality, turn off malfunctioning code, present different variations to different users(A/B Test) and much more. Example: You decide to test new functionality within your application with a select few users. To do this you can easily create a new `Product Version` in which the Feature Flag related to the new functionality is enabled and then link the user licenses to the newly created Product Version.

## **Changes without deployment**

You can easily change the values of a Feature Flag using our dashboard and, our API. This is essentially useful when you want to change values that are causing errors in your application. Example: Your analytics plugin was updated with the new release of your application, however, this new plugin seems to be causing unexpected issues on your user's devices. If you have associated the usage of analytics with a Feature Flag, simply disabling the flag will stop your application from malfunctioning.

## **Value-based changes**

`Feature Flags` in Cryptlex have an optional 'Data' field. This allows you to associate a String value with your Feature Flag. This is especially useful when you need to debug your application on the go. Example: Your application has set a certain data entry to be invalidated in 20ms, however, this has caused various errors after the recent Android update. Setting the value in a Feature Flag allows you to change the value from Cryptlex and have it reflected in your application.

##

\
