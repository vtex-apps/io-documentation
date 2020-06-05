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

1. Using your terminal and the [VTEX IO Toolbelt](https://vtex.io/docs/recipes/development/vtex-io-cli-installation-and-command-reference/), log in to the VTEX Account in which you are currently working in.
2. Using the command below, clone the `service-example` repository:

```
git clone https://github.com/vtex-apps/service-example.git
```

3. Once successfully cloned, go to the local app directory. Use the `cd service-example` command;
4. Open the app using your code editor;
5. In the `node/service.json` file, add `"settingsType": "workspace"` to the app's path to define which routes will be able to receive configurations through requests. You should end up with something similar to the example below:

```diff
 {
   "routes": {
     "status": {
       "path": "/_v/status/:code",
       "public": true,
+      "settingsType": "workspace"
     }
   }
 }
```

It is also possible to **define your configurations through event listening**. For this scenario, you should add in the  `node/service.json` file something similar to the example below, replacing the values according to your needs: 

```diff
 {
   "events": {
     "eventHandler": {
       "sender": "appEmittingTheEvent",
       "keys": ["topic"],
+      "settingsType": "workspace"
     }
   }
 }
```

6. In the `manifest.json` file, add the `configuration` Builder to the `builders` list and update the app's name to one of your choosing. For example:

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

7. Create a `schema.json` file in the `configuration` folder. You will need this `configuration/schema.json` file to define the settings structure that the service app is going to accept from other apps on the platform.
8. Once the file is created, create a JSON Schema in that file, according to your scenario. For example:

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

9. Save your changes and then [publish your new service app](https://vtex.io/docs/recipes/development/publishing-an-app/).

### Step 2 - Linking your app configurations to the service app

Once your service app is deployed, it is ready to receive configurations from others. 

1. In your VTEX IO app, add the recently created service app as a new builder. For example:

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

2. In your app code, create a new file in the `configuration.json` folder named after the desired Service App name. Following our example, we would have something similar to: `vtex.most-amazing-service-ever/configuration.json`.
3. In the file you've just created, define which service configurations are expected according to the JSON schema structure previously defined in the Service App. For example:

```json
{
  "name": "little foot",
  "id": 19
}
```

4. Save your changes and then [publish your new app version](https://vtex.io/docs/recipes/development/publishing-an-app/).
  
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
