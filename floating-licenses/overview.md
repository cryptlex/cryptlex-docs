# Overview

Floating licenses \(also known as concurrent/network licenses\) allow limited number of licenses for your app to be shared among a larger number of users over time. When authorised users wish to run the app, they request the license from a license server.

Suppose your client has 30 employees which will be using your app. In most cases there will be less than 20 users concurrently using your app. Instead of purchasing 30 individual licenses, your client will only purchase the number of floating licenses required to support the number of concurrent users. 

Floating licenses are usually more economical than purchasing individual node-locked licenses.

## Hosted vs On-Premise floating license server

Cryptlex offers both hosted as well as on-premise floating license server. In the former case you can simply use the LexActivator library and Cryptlex Web API server will act as floating license server and in the later you will use the on-premise LexFloatServer and LexFloatClient library to implement floating license model.

## How does floating license work?

When your app starts it requests a floating license from the license server. The license server checks the number of available licenses with itself, if it finds a free license it leases it to your app for a specified amount of time.

After the leased time is over, your app automatically sends a refresh request to the license server, to extend the lease and the process repeats itself. When your user is done using the app, it sends a request to free the license, thereby making it available for other users.

## How your app obtains a floating license?

In order for your app to obtain a floating license, it has to use LexActivator/LexFloatClient library. Every time your client requests a floating license, it checks out a license from the license server and the number of available license activations on the server is decreased. If all available license activations from the server are leased, the next client who wants to obtain a license must wait until one of the other client's finishes its work and the license activation is freed on the license server.

## What are zombie licenses?

Suppose a client requests a floating license with a lease length of 1 hour. If client is done with it's work after 30 minutes, it should inform the license server, so that license is freed. If the client doesn't, the license becomes \(zombie\) useless for next 30 minutes as server assumes it is being used. After, lease time is over, server expects the client to send a refresh request, if client doesn't, license is automatically freed. Hence, zombie licenses are automatically freed up after lease time is over.

