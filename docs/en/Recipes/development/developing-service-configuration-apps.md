---
title: Developing service configuration apps
description: "Improve your VTEX IO app development by developing another app which is solely dedicated to services configuration."
date: "2020-04-09"
tags: ["develop", "development", "service", "configurations", "settings", "apps"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/development/developing-service-configuration-apps.md"
---

# Developing service configuration apps

## Introduction

**A service is basically what an app configures**. At the end of the day, services are responsible for delivering a given functionality to the app's users.

Previously, the code of any service that was configured by an app developed on the VTEX IO platform was part of that app's code package. This mean that each VTEX IO app needed to carry the services configuration required for its proper functioning.

Thanks to a new Builder called **Configurations**, you can now allocate code pertaining to service configurations to an app that's independent of the platform.

By becoming apps that are **independent**, service configurations gain the following advantages:

- Leveraging **workspace functionality**;
- **Versioning**, which makes it easier to rollback or deprecate;
- Can be **altered according to requests sent by other platform apps**, allowing a single service to be individually configured by one or more apps. 

Read the instructions below to better understand how you can improve your VTEX IO app development by developing another app which is solely dedicated to services configuration.

## Step by step

### Step 1 - Creating your service app

In this initial stage, we will create an app to house the services configuration of the other VTEX IO app.

1. Using your terminal and the [VTEX IO CLI](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installation-and-command-reference/), log in to the VTEX Account in which you are currently working in.
2. Using the command below, clone the `service-example` repository:

```
git clone https://github.com/vtex-apps/service-example.git
```

3. Once successfully cloned, go to the local app directory. Use the `cd service-example` command;
4. Open the app using your code editor;
5. Now, to declare that your app can receive configurations through requests, check the sections "If your app has a node service" or "If you are developing a GraphQL app", according to your scenario.
6. In your app's root directory, edit the `manifest.json` file by adding the `configuration` Builder to the `builders` list and update the app's `name` to one of your choosing. For example:

``` diff
 {
   "name": "vtex.most-amazing-service-ever",
   "version": "0.0.0",
   "builders": {
     "node": "4.x",
+    "configuration": "0.x"
   }
 }
```

7. Create a `configuration` folder in your app's root directory, and, then, a `schema.json` file inside it. This file will hold information about the settings structure that the service app is going to accept from other apps on the platform.
8.  In the `configuration/schema.json` file, create a JSON Schema, according to your scenario. For example:

```json
{
  "type": "object",
  "properties": {
    "id": { "type": "number" },
    "name": { "type": "string" }
  }
}
```

The JSON Schema will be used to identify new configurations coming from apps. It will also define the expected format of a new configuration. 

In the example above, the accepted configuration is an object with two keys: `id` and `name`, where the first is a number, and the second, a string.

9. Save your changes and then [publish your new service app](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-publishing-an-app/).


#### If your app has a Node Service

In the `node/service.json` file, add `"settingsType": "workspace"` to the app's path to define which routes will be able to receive configurations through requests. You should end up with something similar to the example below:

``` json
"routes": {
  "status": {
    "path": "/_v/status/:code",
    "public": true,
    "settingsType": "workspace"
  },
  ...
}
```

It is also possible to **define your configurations through event listening**. For this scenario, you should add in the  `node/service.json` file something similar to the example below, replacing the values according to your needs: 

``` json
"events": {
  "eventHandler": {
    "sender": "appEmittingTheEvent",
    "keys": ["topic"],
    "settingsType": "workspace"
  },
  ...
}
```

#### If you are developing a GraphQL app

If you are developing a GraphQL app, you may need to add a directive to all of the queries that can receive configurations.

A [GraphQL Directive](https://graphql.org/learn/queries/#directives) is a way of changing how the query will be performed. When you add the `settings` directive, the system knows it must search for configurations for that service. Under the hood, this directive is including one extra step to the query, which is responsible for finding all the configurations and adding them to the context.

Take our [graphql-example](https://github.com/vtex-apps/graphql-example) app as an example. In this app's root directory, you'll see the following file `grapqhl/schema.graphql`. Now, if you open it and add the `@settings` directive to the query `book`, you'll have something like:

``` diff
type Query {
-  book(id: ID!): Book
+  book(id: ID!): Book @settings(settingsType: "workspace")
}

+@settings(settingsType: "workspace")
```

### Step 2 - Linking your app configurations to the service app

Once your service app is deployed, it is ready to receive configurations from others. 

1. In your VTEX IO configuration app, add the recently created service app as a new builder. For example:

```diff
 {
   "name": "vtex.amazing-configuration",
   "version": "0.0.0",
   "builders": {
+    "vtex.most-amazing-service-ever": "0.x",
   }
 }
```

Notice that the name of the builder is exactly the same as that of the service you want your app to configure. The version also needs to match the desired service app version.

2.  In your app code, create a new file called `configuration.json` inside the folder named after the desired Service App. Following our example, we would have something similar to: `vtex.most-amazing-service-ever/configuration.json`.
3. In the file you've just created, define which service configurations are expected according to the JSON schema structure previously defined in the Service App. For example:

```json
{
  "name": "little foot",
  "id": 19
}
```

4. Save your changes and then [publish your new app version](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-publishing-an-app/).
  
### Step 3 - Reading the service app configurations

Lastly, we must know how to access configurations received by the service app.

As previously mentioned, the service configurations originate from other platform apps through the context of their given request. 

To access all configurations sent to the service app, use the following command:

```js
const settings = ctx.vtex.settings
```

The `ctx` can be either a `EventContext` or a `ServiceContext`.

The structure of the received configurations list is similar to the example below: 

```json
[
  {
    "vtex.amazing-configuration": {
      "name":"little foot",
      "id":1
    },
    "declarer": "vtex.amazing-configuration@0.0.0+build1580823094"
  }
]
```

We're looking at an array where each object is a configuration originating from a different app - since you can have multiple apps configuring the same service.

In each array element, you have an object with two keys: the name of the app that is configuring the service (`vtex.amazing-configuration`, in the example above) and the `declarer`. The first contains the settings itself, according to the structure defined in the service app's JSON Schema. The second corresponds to the full name of the app that carries such configurations.

## Troubleshooting

If you are developing a configuration app and the service that your app is configuring is not installed or linked in the same workspace you're working at, you may run into some errors.

That happens because, when creating a new configuration app, the configuration builder first looks for the schema of that configuration in all the apps installed in your current workspace. Consequently, if the configuration builder cannot find this specific configuration, linking your app may fail.

Hence, to avoid errors, remember to always have the service you're configuring linked or installed in the same workspace you're developing your configuration app.

Also, if you want to publish your configuration app, but doesn't want to have your service installed in the `master` workspace, you can link or install the service in an alternative branch and, then, when you're ready to publish it, you can use the `-w` flag, as in:

```
vtex publish -w <alternative-branch-name>
```
