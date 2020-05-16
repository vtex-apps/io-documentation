---
title: Creating custom apps on VTEX IO
description: "Find now all guidelines regarding the VTEX IO Application form to make it easier for you to start developing on the platform!"
date: "2020-05-20"
tags: ["apps", "custom", "apí", "service", "react", "interface", "kickstart"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/new-docs-and-fix/docs/en/Recipes/development/creating-custom-apps-on-vtex-io.md"
---

# Creating custom apps on VTEX IO

The VTEX IO platform allows developers to create unique commerce experiences using Web technologies. It's possible to create **frontend blocks** for Store Framework, **backend services** exposing REST or GraphQL APIs and combine a series of VTEX frameworks into a complete solution, packaging it in **an app**.

This tutorial will show you how to quickly start developing a custom app on VTEX IO!

## Manifest

Every IO app must have a `manifest.json` file on its root folder. This file holds important information about the app, like it's **name**, **version**, **vendor**, **settingsSchema**, **dependencies**, etc. For guidelines about app naming, you can read [this arcticle](TODO).

![Wordpress App Manifest](https://user-images.githubusercontent.com/18706156/81855711-14535680-9536-11ea-9e1c-9150d3570c97.png)

_[Original](https://github.com/vtex-apps/wordpress-integration/blob/d3ca9bd43b8d6797f162519d7b8a31ec755bd47d/manifest.json)_

Now, let's go through some of the fields you can declare on your manifest and how they interfere on the app functioning!

### Builders

These are the entrypoints of the app's functionality. In fact, all implementation must relate to the builders declared on the manifest, and live inside a folder with the corresponding name. For example, if I want to **develop React components** on an app, I should use the builder `react@3.x`, declaring it on the manifest:

```json
    "builders": {
        "react": "3.x"
    }
```

And create a `react` folder inside the app, placing there the component files. Each builder will have its own set of rules and validation process.

One interesting aspect of this is that **it's possible to use as many builders as you want in one app**, which allows bundling frontend and backend development, delivering just one package with your solution.

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

The `dependencies` field on the manifest accepts IO Apps, with their versions, and its meaning doesn't differ from a `package.json`'s dependencies on a Javascript apps. 

If you app needs to interact with another IO app (like a VTEX API), you need to declare it on `dependencies`. There's also some other cases like:

- Using _blocks_ from another app _(example: [vtex.store-theme](https://github.com/vtex-apps/store-theme/blob/fee222b7d337ab35a57eeefe12c27181e9e9e257/store/blocks.jsonc#L12))_
- Importing React components from another app _(example: [vtex.order-placed](https://github.com/vtex-apps/order-placed/blob/ec6fab76f59ea4eacbea465419c3d026ae26be73/react/BankInvoiceSection.tsx#L3))_
- Importing Typescript types from a GraphQL service app _(example: [vtex.my-account](https://github.com/vtex-apps/my-account/blob/414c584e8f4acf0d9f3c5e9b37f6d946f7bfa8ac/react/typings/graphql/customerGreeting.gql.d.ts#L3))_
- Querying GraphQL or REST from another app _(example: [vtex.store-form](https://github.com/vtex-apps/store-form/blob/aca5bbde3c6b9ac311d656e6f5e9659f787ab196/react/graphql/getSchema.graphql))_
- Implementing a GraphQL schema from anoher app _(example: [vtex.search-resolver](https://github.com/vtex-apps/search-resolver/blob/49dccd1e5a952bf195aed929e8cca85a1cb29a79/node/index.ts#L4))_

> When installing an app, its dependencies will be automatically be installed on that account as well, but not as first-class apps (i.e: indirect dependencies will not be able to declare routes).

### Peer Dependencies

It´s possible to configure app A to be **peer dependant** on on app B. VTEX IO will understand that **app B is required for app A to work**, so it enforces that app B **must already be installed in the workspace before A can be installed.**

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

### credentialType

### policies

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

Another great way of learning about VTEX IO apps is **checking our [vtex-apps](https://github.com/vtex-app) organization on Github**, as most of the code that powers Store Framework **is open-source**. Here are some of the apps you'll find there:

| App | Description | Builders |
|--|--| -- |
| [store-theme](https://github.com/vtex-apps/store-theme) | Theme definition for [Store Theme](https://storetheme.vtex.com) | `store`, `styles` and `sitemap`
| [wordpress-integration](https://github.com/vtex-apps/wordpress-integration) | Complete solution for integrating a VTEX Store with Wordpress, fetching external data and exposing blocks | `react`, `store`, `node`, `graphql` and `messages`
| [seller-selector](https://github.com/vtex-apps/seller-selector) | Exports blocks and route to marketplaces with multiple sellers | `react`, `store`, and `messages`
| [admin-pages](https://github.com/vtex-apps/admin-pages) | VTEX Site Editor | `react`, `admin`, and `messages`
| [store-graphql](https://github.com/vtex-apps/store-graphql) | Connection to VTEX Commerce API's |  `node` and `graphql`

> All apps listed above use the `docs` builder as well.