---
title: Builders
description: "Builders concept"
date: "2020-04-09"
tags: ["builders"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/new-docs-1/docs/en/Concepts/builders.md"
---

# Builders

A *Builder* is responsible for processing, validating, and forwarding a given block of code to a runtime or a framework capable of executing it.

In practice, a builder works as an API responsible for configuring other IO services.

As you'll see in the following, builders can also be understood as the entry points to the functionalities of an IO app.

In fact, the whole app implementation must relate to the builders declared in the app's `manifest.json` file and live inside the folders named over the app's builders.

When running an IO app, each builder converts the files included in its corresponding folder into configurations to the competent services. Check our [implementation example](#implementation-example).

>ℹ️ Notice that each builder has its own set of rules and validation process.

One important aspect is that an app can have as many builders as you want. That allows bundling front and backend development and delivering your solution with just one package.

Notice that by dividing responsibilities into smaller builders, we are able to evolve them separately - quickly and with fewer stop-the-world breaking changes. Thus, it's expected from a builder to:

- Have very *well-defined* and *minimal responsibilities*.
- Be *abstract* and *opinionated* according to its goals.
- Allow *fine-grained permission control*.

We currently work with several builders that simplify app development by making each part of an app's responsibilities clear and well separated. Check our [list of builders](#list-of-builders).

## Implementation example

Pretend you want to develop a *React* component in your IO app.

For that, you'll need to use a builder that offers a way to configure a *React renderer*, namely, the `react@3.x` builder.

To do that, you must declare the `react@3.x` builder in the app's `manifest.json` file, as in the following:

```json
"builders": {
    "react": "3.x"
}
```

Then, in your app's root directory, you must create a folder named over the builder (e.g., `/react`) and place there the files you want its respective builder to compile (e.g., React component files).

When running your app, the `react@3.x` builder will transform the source code of TypeScript React components, placed inside the `/react` folder, into compiled bundles, ready to be imported into render apps.

## List of builders

The VTEX Product Team is always improving how our builders work and *creating new ones* to ease the development of commerce solutions. Notice that some of these are builders are not open beta. 

>⚠️ If you need to use a builder that is not open beta, you must [fill in the application form for development](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-filling-the-application-form-for-development).

This is a *non-exhaustive* list of VTEX IO builders:

Name | Functionality | Open Beta |
---- | ------------- | --------- |
 `admin` | Exports blocks and routes to the VTEX Admin.| ❌ |
 `assets` | Handles assets used by store theme blocks. It gets all asset paths used and uploads them to the VTEX IO database. *You can learn how to use it by accessing the recipe on [Using the Assets Builder](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-using-the-assets-builder/).*| ❌ |
 `configuration` | Allows you to allocate code pertaining to service configurations to an app that's independent of the platform. *You can learn how to use it by accessing the recipe on [Developing service configuration apps](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-developing-service-configuration-apps/).*| ❌ |
 `dotnet` | Interprets the `/dotnet` directory, empowering the development of custom backend services.| ❌ |
 `graphql` | Processes GraphQL API's and schemas by interpreting `.graphql` and `.gql` files contained in the app's `/graphql` directory.| ❌ |
 `services` | Fetches service workers exported by the account's installed apps and bundles them in a single file, enabling the store to work with several service workers simultaneously. You can learn how to use it by accessing the recipe on [Using several service workers in your store](https://developers.vtex.com/vtex-developer-docs/docs/using-several-service-workers-in-your-store).| ❌ |
 `styles` | Exports CSS configurations for Store Framework blocks. When building your app, the Styles builder reads the `styles/styles.json` file and uses a [Tachyons](https://tachyons.io/) generator to properly produce your store's CSS.| ✅ |
 `store` | Interprets and validates the blocks, interfaces and routes contained in the theme app's `/store` directory, powering Store Framework store's components and building the storefront.| ✅ |
 `messages` | Exports localized string messages, empowering *VTEX IO internationalization*. It reads `.json` files associated with different locales within the app's `/messages` directory and makes them available for front-end applications to use via `react-intl`.| ✅ |
 `node` | Interprets the `/node` directory, empowering the development of custom backend services using Typescript.| ❌ |
 `pixel` | Processes the source-code and configuration of [Pixel Apps](https://developers.vtex.com/vtex-developer-docs/docs/pixel-apps) in VTEX IO. The files picked up by this builder are located in the app's `/pixel` directory.| ❌ |
 `react` | Interprets the `/react` directory, empowering the development of React components using Typescript| ✅ |
