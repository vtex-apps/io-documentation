---
title: Creating custom apps on VTEX IO
description: "Find now all guidelines regarding the VTEX IO Application form to make it easier for you to start developing on the platform!"
date: "2020-05-20"
tags: ["apps", "custom", "apí", "service", "react", "interface", "kickstart"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/new-docs-and-fix/docs/en/Recipes/development/creating-custom-apps-on-vtex-io.md"
---

# Creating custom apps on VTEX IO

The VTEX IO platform allows developers to create unique commerce experiences using Web technologies. It's possible to create **frontend blocks** for Store Framework, **backend services** exposing REST or GraphQL APIs and combine a series of VTEX frameworks into a complete solution, packaging it into **an app**.

This tutorial will show you how to quickly start developing a custom app on VTEX IO!

## Manifest

Every IO app must have a `manifest.json` file on its root folder. This file holds important information about the app, like it's **name**, **version**, **vendor**, **settingsSchema**, **dependencies**, etc. For guidelines about app naming, you can read [this arcticle](TODO).

Check this manifest from app **vtex.wordpress-integration**:
![Wordpress App Manifest](https://user-images.githubusercontent.com/18706156/81855711-14535680-9536-11ea-9e1c-9150d3570c97.png)

_[Original](https://github.com/vtex-apps/wordpress-integration/blob/d3ca9bd43b8d6797f162519d7b8a31ec755bd47d/manifest.json)_

Now, let's go through some of the fields you can declare on your manifest and how they interfere on the app functioning!

### Builders

These are the entrypoints of the app's functionality. In fact, all implementation must relate to the builders declared on the manifest, and live inside a folder with the corresponding name.

For example, if you want to **develop React components** on an app,  you should use the builder `react@3.x`, declaring it on the manifest:

```json
    "builders": {
        "react": "3.x"
    }
```

And create a `react` folder inside the app, placing there the component files. Each builder will have its own set of rules and validation process.

One interesting aspect of this is that **it's possible to use as many builders as you want in one app**, which allows bundling frontend and backend development, delivering you solution with just one package.

The VTEX Product Team is always improving how our builders works (and creating new ones) to ease the development of commerce solutions.

This is a *non-exaustive* list of the VTEX IO builders:

| Name | Current Version | Functionality |
|--|--| -- |
| `react` | `3.x` | Development of **React components** using Typescript |
| `node` | `6.x` | Development of **custom backend services** using Typescript |
| `graphql` | `1.x` | Exporting a **GraphQL schema** that a `node` service can implement |
| `store` | `0.x` | Exporting or using **blocks and routes** for VTEX Store Framework |
| `admin` | `0.x` | Exporting blocks and routes for **VTEX Admin** |
| `messages` | `0.x` | Exporting localized **string messages** |
| `styles` | `2.x` | Exporting **CSS configuration** for Store Framework blocks |
| `pixel` | `0.x` | Exporting **pixel apps** to be included on the Storefront |
| `docs` | `0.x` | Exporting **app's documentation** to be posted on vtex.io/docs | 

For more technical information about them, read [Builders](https://vtex.io/docs/concepts/builders/).

### Dependencies

The `dependencies` field on the manifest accepts IO Apps, with their versions, and its semantics looks like a `package.json`'s dependencies on Javascript apps. 

If your app needs to **interact with another IO app** (like a VTEX API), you need to declare it on `dependencies`. The most common cases of dependency are:

- Using _blocks_ from another app _(example: [vtex.store-theme](https://github.com/vtex-apps/store-theme/blob/fee222b7d337ab35a57eeefe12c27181e9e9e257/store/blocks.jsonc#L12))_
- Importing React components from another app _(example: [vtex.order-placed](https://github.com/vtex-apps/order-placed/blob/ec6fab76f59ea4eacbea465419c3d026ae26be73/react/BankInvoiceSection.tsx#L3))_
- Importing Typescript types from a GraphQL service app _(example: [vtex.my-account](https://github.com/vtex-apps/my-account/blob/414c584e8f4acf0d9f3c5e9b37f6d946f7bfa8ac/react/typings/graphql/customerGreeting.gql.d.ts#L3))_
- Querying GraphQL or REST from another app _(example: [vtex.store-form](https://github.com/vtex-apps/store-form/blob/aca5bbde3c6b9ac311d656e6f5e9659f787ab196/react/graphql/getSchema.graphql))_
- Implementing a GraphQL schema from anoher app _(example: [vtex.search-resolver](https://github.com/vtex-apps/search-resolver/blob/49dccd1e5a952bf195aed929e8cca85a1cb29a79/node/index.ts#L4))_

> When installing an app, its dependencies will be automatically be installed on that account as well, but not as first-class apps (i.e: indirect dependencies will not be able to declare routes).

### Peer Dependencies

It´s possible to configure app A to be **peer dependant** on an app B. VTEX IO will understand that **app B is required for app A to work**, so it enforces that app B **must already be installed in the workspace before A can be installed.**

> **Keep in mind:** Peer Dependencies will not be automatically installed!


The peer dependency concept is strongly related with the power of a directly installed app (which we call root apps, because they are the roots of the dependency tree) and with the power of a mere dependency.

**Only root apps are allowed to declare routes and only root apps are billable.** This means that if you depend on a paid app, you must use a peer dependency. 

A peer dependecy declares that the app can't be installed without that dependency being installed.

An example would be the Pages admin where the user can't install it without first installing `vtex.store` 
```javascript
{
  ...
  "peerDependencies": {
      "vtex.store": "2.x"
  },
  "dependencies": {
      "vtex.styleguide": "9.x"
  }
}
  ```

### settingsSchema

The VTEX Admin for Apps may display configuration forms for each app installed on that account, and it's using this field on `manifest.json` that an app may **declare the schema of its configuration**. Using [JSON Schema](https://json-schema.org/), it's possible to accept multiple field with multiple data types. The persistence of the information is taken care by VTEX Plaftorm, and you may fetch the current configuration on your app code.

For example, on the **vtex.wordpress-integration** app, the following `settingsSchema`: 

```json
  "settingsSchema": {
    "title": "Wordpress Integration",
    "type": "object",
    "properties": {
      "endpoint": {
        "title": "Wordpress URL",
        "description": "Enter the URL of your Wordpress installation in the form http://www.example.com/",
        "type": "string"
      },
      "titleTag": {
        "title": "Title tag for blog homepage",
        "description": "Will also be appended to inner blog pages",
        "type": "string"
      },
      "blogRoute": {
        "title": "URL path for blog homepage",
        "description": "Example: if 'foo' is entered here, blog homepage will be at http://www.yoursite.com/foo . Make sure routes in your store-theme match this setting. If left blank, default is 'blog'",
        "type": "string"
      }
    }
  }
```

will generate the following form once that app is installed:

![image](https://user-images.githubusercontent.com/18706156/82129418-fb96ab00-9798-11ea-8d22-915fb2f59f6e.png)

On your app's code, it's possible to **retrieve this configuration**, when configured by the merchant, in two ways:

- With a GraphQL query from the frontend to the `vtex.apps-graphql` (like [vtex.shopper-approved](https://github.com/vtex-apps/shopper-approved/blob/3d33e84f3b36eabcea4e3f940cd63095d48767bb/react/graphql/shopperApprovedSettings.graphql))
- On the backend, using the `getAppSettings` metod from `ctx.clients.apps` client  (like [vtex.store-indexer](https://github.com/vtex-apps/store-indexer/blob/9bff58ebcb560560ad1a598a080c93e4bde38ecb/node/middlewares/settings.ts#L18))

### credentialType

When creating Node.js services that needs to communicate with other VTEX services **on behalf of the app**, instead of the user, the `credentialType` should be `absolute`.

This will result in the contents of `ctx.vtex.authToken` being **the app's token**, what may be used to authenticate into other services.

> The credential for the user who sent the request may be still accesed in `ctx.vtex.adminUserAuthToken` or `ctx.vtex.storeUserAuthToken`. Details [here](https://github.com/vtex/node-vtex-api/blob/929b9335f9fb0fe8fca6bf705e0aee80f923443c/src/service/worker/runtime/typings.ts#L122).

### policies

If the app being built needs to **access some external services** or get some specific data from other places, it needs to declare so, even for external API's.

The `policies` field on the app's manifest is **a list of resources** representing the "permissions" required by the apps. These resources might be of two types:

- A specific resource (like `vtex.catalog-api-proxy:catalog-proxy` on [vtex.store-graphql](https://github.com/vtex-apps/store-graphql/blob/040bcc3e2a96d1537fe05647e0db677bda9fcb15/manifest.json#L140)) that was declared by [other app](https://github.com/vtex-apps/catalog-api-proxy/blob/5bb8085e5ea21c9be418b6f86c495584e3fc2c90/policies.json#L3) on `policies.json`. This file is used by apps that want to **declare policies for its resources.**

- A descrition of an `outbound-access` resource, providing information about the HTTP API that the app needs to communicate with. This was the case for all `policies` from the `vtex.wordpress-integration` app displayed above.

```json
"policies": [
    {
      "name": "outbound-access",
      "attrs": {
        "host": "{{account}}.vtexcommercestable.com.br",
        "path": "/api/dataentities/*"
      }
    },
    {
      "name": "outbound-access",
      "attrs": {
        "host": "*",
        "path": "/wp-json/wp/v2/*"
      }
    }
  ]
 ```

 ## Best Practices

- Use [Typescript](https://www.typescriptlang.org/) when developing React or Node. We provide some default environment configuration on [vtex/typescript](http://github.com/vtex/typescript).
- Use [VTEX Styleguide](https://styleguide.vtex.com/) when developing Admin Apps or extensions to My Account. 
- Use [React Hooks](https://reactjs.org/docs/hooks-intro.html) when developing custom blocks. We already expose some VTEX API's with hooks like [*useRuntime*](https://vtex.io/docs/app/vtex.render-runtime) or [*useProduct*](https://github.com/vtex-apps/product-quantity/blob/8e83b0fd64d0496d36ced2645e53961e1e37211a/react/ProductQuantity.tsx#L2).
- Always **prefer GraphQL** if you're creating a complete frontend/backend solution, since it will help us constantly improve page load time.

### React Apps
- Visit the documentation for [**render-runtime**](https://vtex.io/docs/app/vtex.render-runtime) to check available **navigation** API's. It's not necessary to inject third-party routers on your app.

 ## Courses

If you want to learn from stratch about VTEX IO and Store Framework, a great way to start is **enrolling on our courses**. As of now, we have two:

1. The [Store Framework Course](https://lab.github.com/vtex-trainings/store-framework), where you'll learn about Store Framework and how to create beautiful themes.
2. The [Store Block Course](https://lab.github.com/vtex-trainings/vtex-store-block-course/), where you'll learn how to creating custom Store Framework blocks using React.

 ## Development

- The development flow for IO apps is seamless. Just run `vtex link` and you should be good to go! More details on [Linking an app](https://vtex.io/docs/recipes/development/linking-an-app/).
- When using service builders, the _link_ process will probably **output the URL for your service**, where you may test endpoints directly. If you're building GraphQL API's, it will print the location of a **GraphiQL IDE** where you may test your queries and resolvers.

## Templates and Examples

Instead of writing the boilerplate code when creating an VTEX IO App, try using one of our **app templates**. If your solution will be composed by multiple functionalities (like frontend components and backend services), you might want to **merge the examples apps**, adding the appropriate builders on `manifest.json` and centering all folders into one app.

Here's a list of our example/template apps:

| App | Description |
|--|--|
| [react-app-template](https://github.com/vtex-apps/react-app-template) | Exports Store Blocks using React components |
| [pixel-app-template](https://github.com/vtex-apps/pixel-app-template) | Example of a [Pixel App](https://vtex.io/docs/apps/pixel/) |
| [service-example](https://github.com/vtex-apps/service-example) | Exposes a RESTful API using Node.js and Typescript |
| [graphql-example](https://github.com/vtex-apps/graphql-example) | Exposes a GraphQL API using Node.js and Typescript |
| [admin-example](https://github.com/vtex-apps/admin-example) | Creates a VTEX Admin extension app, adding items to menu and rendering React components |
| [events-example](https://github.com/vtex-apps/events-example) | Exposes a Node.js app that handles platform events 
| [search-engine-example](https://github.com/vtex-apps/search-engine-example) | Backend service that implements VTEX's Search Protocol |

Another great way of learning about VTEX IO apps is **checking the [vtex-apps](https://github.com/vtex-apps) organization on Github**, as most of the code that powers Store Framework **is open-source**. Here are some of the apps you'll find there:

| App | Description | Builders |
|--|--| -- |
| [store-theme](https://github.com/vtex-apps/store-theme) | Theme definition for [Store Theme](https://storetheme.vtex.com) | `store`, `styles` and `sitemap`
| [store](https://github.com/vtex-apps/store) | Declaration of default blocks and store routes | `react`, `store`, and `messages`
| [wordpress-integration](https://github.com/vtex-apps/wordpress-integration) | Complete solution for integrating a VTEX Store with Wordpress, fetching external data and exposing blocks | `react`, `store`, `node`, `graphql` and `messages`
| [seller-selector](https://github.com/vtex-apps/seller-selector) | Exports blocks and route to marketplaces with multiple sellers | `react`, `store`, and `messages`
| [admin-pages](https://github.com/vtex-apps/admin-pages) | VTEX Site Editor | `react`, `admin`, and `messages`
| [store-graphql](https://github.com/vtex-apps/store-graphql) | Connection to VTEX Commerce API's |  `node` and `graphql`

> All apps listed above use the `docs` builder as well.