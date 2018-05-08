# Hosted Floating License Server

## Creating a floating license

At the time of license creation you should do the following to configure the floating license:

* Set the license type to **"floating".**
* Set the lease duration to the amount of time you want to lease the licenses.
* Make sure server sync interval is less than lease duration, as server sync is responsible for licence renewal.

## Adding floating licensing to your app

Hosted floating license server uses Cryptlex Web API directly to lease the floating licenses. You can simply use LexActivator to enable floating licenses:

{% page-ref page="../node-locked-licenses/using-lexactivator/" %}

When your user is done using the app, the app should send a request to free the license activation by calling `DeactivateLicense()` LexActivator API function, thereby making it available for other users. If the app doesn't, the license activation becomes \(zombie\) useless until lease time is over.

## Borrowing floating licenses

Borrowing floating licenses for offline usage is supported out of the box. You just need to increase the `leaseDuration` to the amount of time you wish to lease the license for offline usage.

