# Clients 

On VTEX IO, Clients are **abstractions to other services**. 

Whenever you need to set up a connection with an external API or another VTEX service, you should create a Client to **focus on the real value of your software instead of worrying about those platform complexities**. Some standard clients are already into the VTEX IO. Check them [here](https://github.com/vtex/node-vtex-api/blob/ccf4d8f8d3208007c4bfd558baf979df8d825af8/src/clients/IOClients.ts).

These are some of the features built-in our clients infrastructure:

 - Cache;
 - Native metrics support;
 - Retry and timeout options;
 - Billing tracking.

![Clients on IO Services](https://imgur.com/i45O8MN.png)

Learn how to create Clients of your own by accessing [Managing Clients]() documentation. 


