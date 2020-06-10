---
title: Builders
description: "Builders concept"
date: "2020-04-09"
tags: ["builders"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/new-docs-1/docs/en/Concepts/builders.md"
---

# Builders

In the VTEX IO platform, a builder basically is an **abstraction to configure other IO services**. It is responsible for **interpreting the code of other apps and transforming it** to a given goal, working as an API service that processes and interprets a directory in your app.

For example: the **React** builder offers a way to configure our react renderer, transforming the source code of TypeScript React components into compiled bundles, ready to be imported into Render apps.

As a result, it's important for builders to:

- Have very **well-defined** and **minimal responsibilities**;
- Be **abstract** and **opinionated** according to their goals;
- Allow for **fine-grained permission control**.

We currently work with several builders that **simplify app development by making each part of an app's responsibilities clear and well separated**.

By dividing responsibilities into smaller builders, we are able to evolve them separately - faster and with fewer stop-the-world breaking changes. They are:

- **Styles Builder** - Takes your `styles.json` file when building and uses a [Tachyons](https://tachyons.io/) generator to properly produce your store's CSS.

- **Store Builder** - Responsible for powering Store Framework store's components. It interprets everything that is inside the theme app's  `/store` directory, validating the blocks, interfaces and routes in order to build the store's front. 

- **GraphQL Builder** - Processes GraphQL files (`.graphql` or `.gql`) from an IO app. These files are used to define a GraphQL's API and Schema. As expected, these files are found in the app's `/graphql` directory.

- **Messages Builder** - Empowers VTEX IO internationalization. It reads `json` files associated with different locales within the app's `/messages` directory and makes them available for front-end applications to use via `react-intl`.

- **Pixel Builder** - Processes the source-code and configuration of [Pixel Apps](https://vtex.io/docs/apps/pixel/) in VTEX IO. The files picked up by this builder are located in the app's `/pixel` directory.

- **Assets Builder** - Handles assets used by store theme blocks. It gets all asset paths used and uploads them in the File Manager service, the VTEX IO database. You can learn how to use it by accessing the recipe on [Using the Assets Builder](https://vtex.io/docs/recipes/development/using-the-assets-builder/).

- **Configurations Builder** - Allows you to allocate code pertaining to service configurations to an app that's independent on the platform. You can learn how to use it by accessing the recipe on [Creating service configuration apps](https://vtex.io/docs/recipes/development/creating-service-configuration-apps/).

 - **Docs Builder** - Processes app's documentations and make it available on VTEX IO Docs. Each app is responsible for containing its own documentation, written in Markdown (`.md`) format and uploaded in a a `/docs` directory - where Docs Builder can interpret it.

