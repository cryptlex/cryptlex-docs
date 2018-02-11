## Overview of Floating Licenses

Floating licenses allow limited number of product keys for your app to be shared among a larger number of users over time. When authorized users wish to run the app, they request a license from a central LexFloat license server.

Suppose your client has 30 employees which will be using your app. In most cases there will be less than 20 users concurrently using your app. Instead of purchasing 30 individual licenses, your client will only purchase the number of Floating Licenses required to support the number of concurrent users. Floating Licenses are usually more economical than purchasing individual regular licenses.



### How does Floating License Server works?

When your app starts it requests a floating license from the LexFloat server. The LexFloat server checks the number of available licenses with itself, if it finds a free license it leases it to your app for a specified amount of time.

After the leased time is over, your app automatically sends a refresh request to LexFloat server, to extend the lease and the process repeats itself. When your user is done using the app, it sends a request to free the license, thereby making it available for other users.

### How does your App obtain the Floating License?

In order for your app to obtain a floating license, it has to use LexFloatClient library. Every time your client requests a floating license, it checks out a license from that LexFloat server and the number of available licenses on this server is decreased. If all available licenses from the server are leased, the next client who wants to obtain a license must wait until one of the other client's finishes its work and the license is returned back to the LexFloat server.

### What are Zombie Licenses?

Suppose a client requests a floating license with a lease length of 1 hour. If client is done with it's work after 30 minutes, it should inform the license server, so that license is freed. If the client doesn't, the license becomes \(zombie\) useless for next 30 minutes as server assumes it is being used. After, lease time is over, server expects the client to send a refresh request, if client doesn't, license is automatically freed. Hence, zombie licenses are automatically freed up after lease time is over.

