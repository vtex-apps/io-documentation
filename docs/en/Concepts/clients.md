# Clients 

Systems are meant to solve real problems by communicating to the needed services. A delivery app, for example, solves the issue of the desire to eat by communicating with a local restaurant service. 

On VTEX IO architecture, the communication made by a system to request a service is so crucial that a whole concept was built for it: **Clients**.

In other words, Clients are configurations to be set up in a given system to **abstract its communications to the needed services**. 

When building software, you can tackle complexities by setting up clients and then optimizing your code. Some standard clients are already into the VTEX IO. Check them [here](https://github.com/vtex/node-vtex-api/blob/ccf4d8f8d3208007c4bfd558baf979df8d825af8/src/clients/IOClients.ts).

These are some of the features built-in our clients infrastructure:

 - Cache;
 - Native metrics support;
 - Retry and timeout options;
 - Billing tracking.

![Clients on IO Services](https://imgur.com/i45O8MN.png)

Learn how to create Clients of your own by accessing [Managing Clients](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-how-to-create-and-use-clients) documentation. 


