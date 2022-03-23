# Service

A service is a piece of code used to run .NET and Node.js on VTEX servers. This way, services allow VTEX IO apps to export HTTP routes, GraphQL resolvers, and event handlers to the server.

By setting the `node` or `dotnet` [builders](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-builders) in your app's [`manifest.json`](https://developers.vtex.com/vtex-developer-docs/docs/manifest) file, VTEX IO apps can export services just like themes and store blocks.

>ℹ️ It´s also possible to export GraphQL services, using the `graphql` builder. Check the [vtex.graphql-example](https://github.com/vtex-apps/graphql-example) app to see how it's done.

Considering the builder in use (`node` or `dotnet`), services must be configured in the `service.json` file inside the `/node` or `/dotnet` folder. This file is responsible for declaring routes and events that the service must respond to. It also configures parameters such as `timeout` and `memory`.

Take the following example of a `service.json` file:

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

As a reference, consider the following parameters for the `services.json` file:

|Name  |Type  |Description  |
|--|--| -- |
|`events` | `object` |Map from a event handler to an object that describes sender or keys.|
|`maxReplicas` | `number` |Maximum number of replicas available.|
|`minReplicas` | `number` |Minimum number of replicas available when the service is running. |
|`memory` |`number`  |Memory size **in MB** allocated to the service.|
|`routes` | `object` |Map from a route handler to an object that contains `path`, `public` or other information about ReBAC.|
|`timeout` | `number` |Time **in seconds** to abort connection if the request time is taking too long.|
|`ttl` | `number` | Time-to-live or the amount of time **in minutes** that the platform will keep the service running without receiving any new requests. Default: 10. Min: 10. Max: 60.|
|`workers` | `number` |Numbers of workers to spawn for the service on production. (Max: 4). |

Keep in mind that most of these fields are optional and default values from the platform are commonly used.

>ℹ️ For more information, check our [Node.js](https://github.com/vtex-apps/service-example), [.NET](https://github.com/vtex-apps/service-example-dotnet), and [GraphQL](https://github.com/vtex-apps/graphql-example) service example apps.
