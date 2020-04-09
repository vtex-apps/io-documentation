---
title: Builders
description: "Builders concept"
date: "2020-04-09"
tags: ["builders"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/new-docs-1/docs/en/Concepts/builders.md"
---

# Builders

A builder is an app (basically a `.json` file) responsible for interpreting the code of other apps and transforming it. It works as an API service that will process and interpret a directory in your app.

For example: the **React** builder transforms the source code of TypeScript React components into compiled bundles, ready to be imported into Render apps.

As a result, It's important for builders to:

- Have very **well-defined** and **minimal responsibilities**;
- Be **abstract** and **opinionated**;
- Allow for **fine-grained permission control**.

We currently work with several builders that **simplify app development by making each part of an app's responsibilities clear and well separated**.

By dividing responsibilities into smaller builders, we will be able to evolve them separately - faster and with fewer stop-the-world breaking changes. They are:

## Styles Builder

Styles Builder takes your `styles.json` file when building and uses a [Tachyons](https://tachyons.io/) generator to properly produce your store's CSS.

## Store Builder

This is the builder responsible for powering Store Framework stores. It interprets everything that is inside an app's  `/store` directory following 4 steps with different complexity levels:

- `createParseFiles` - Where the parsing of `.json` files in `/store` takes place;
- `resolve` - Responsible for validating the blocks, interfaces and routes defined by those files;
- `maybeAppendDependency` - Adds new dependencies to the app (if needed);
- `writeAssets` - Writes the build result that will be sent to the IO registry.

## Docs Builder

Builder that processes an app's documentation and make it available on VTEX IO Docs. Each app is responsible for containing its own documentation, written in Markdown (`.md`) format in a `/docs` directory, where Docs Builder can find it and work on it.

## GraphQL Builder

GraphQL Builder is responsible for processing GraphQL files (`.graphql` or `.gql`) in an IO app. These files are used to define a GraphQL's API and Schema. As expected, these files are found in the `/graphql` directory.

## Messages Builder

Messages Builder empowers VTEX IO internationalization. It reads `json` files associated with different locales within `/messages` and makes them available for front-end applications to use via `react-intl`.

## Pixel Builder

This is the builder responsible for processing the source-code and configuration of [Pixel Apps](https://vtex.io/docs/apps/pixel/) in VTEX IO. The files picked up by this builder are located in `/pixel`.

## Assets Builder

The VTEX Assets Builder is responsible for handling assets within store theme blocks by getting all asset paths used and uploading them in the File Manager service. You can learn how to use it by accessing the recipe on [Using the Assets Builder](https://vtex.io/docs/recipes/development/using-the-assets-builder/).

## Configurations Builder

The Configurations Builder allows you to allocate code pertaining to service configurations to an app that's independent on the platform. You can learn how to use it by accessing the recipe on [Creating service configuration apps](https://vtex.io/docs/recipes/development/creating-service-configuration-apps/).


## TypedQL [Deprecated]
![https://img.shields.io/badge/-Deprecated-red](https://img.shields.io/badge/-Deprecated-red)
TypedQL Builder is a VTEX IO feature for developing back-end projects. Similar to the GraphQL Builder, it comes as an alternative for back-end apps written in GraphQL + TypeScript. It proposes to be more modern and generic, using only TypeScript Type Declaration files to create the GraphQL interface automatically.
TypeScript-based projects are greatly benefited by the use of this Builder, since developers only need to write TypeScript types. GraphQL Schema is automatically generated
