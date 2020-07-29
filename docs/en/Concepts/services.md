---
title: Services
description: "Services concept"
date: "2020-05-20"
tags: ["services"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/new-docs-1/docs/en/Concepts/services.md"
---

# Services

VTEX IO powers big e-commerce operations, and for most of that it's necessary to **run code on a server**. Services are how we run **Node.js or .NET** code on VTEX IO infrastructure, backed by API abstractions to improve developer experience.

A Service must be exported from a VTEX IO app, just like themes or store blocks, using builders `node` or `dotnet`. With these, it's able to develop a REST API that is setup out of the box, you only need to worry about code.

On the root folder of a service lives `service.json`, where it´s possible to **declare routes that the service must respond to** and other configurations like *timeout* and *memory*.

This is the `node/service.json` from [vtex.service-example](https://github.com/vtex-apps/service-example) app:
```json
{
  "memory": 256,
  "ttl": 10,
  "timeout": 2,
  "minReplicas": 2,
  "maxReplicas": 4,
  "routes": {
    "status": {
      "path": "/_v/status/:code",
      "public": true
    }
  }
}
```

After that, it´s possible to export resolver functions on `node/index.ts` file.

It´s also possible to **export GraphQL services**, using the `graphql` builder. You can check [vtex.graphql-example](https://github.com/vtex-apps/graphq-example) to see how it's done.
