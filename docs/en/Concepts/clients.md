# Clients on VTEX IO Services

Clients, on VTEX IO, are **abstractions to other services**. We tackle complexities when setting up an HTTP client, for example, so you can focus on the real value of your software. Whenever you need to setup a connection with an **external API** or another **VTEX service**, you should create a *client*! Some standard clients are already baked into VTEX IO, check them [here](https://github.com/vtex/node-vtex-api/blob/ccf4d8f8d3208007c4bfd558baf979df8d825af8/src/clients/IOClients.ts).

> *Leave the burden with us!*

**These are some of the features built in our clients infrastructure:**

 - Cache *(you can use disk on in-memory cache easily)*
 - Native metrics support
 - Retry and timeout options
 - Billing tracking *(you can easily charge who uses your app)*

![Clients on IO Services](https://imgur.com/i45O8MN.png)

- Learn [**how to create and use Clients**](recipes/development/how-to-create-and-use-clients.md)
