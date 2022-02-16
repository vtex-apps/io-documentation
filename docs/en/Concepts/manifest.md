# Manifest

The `manifest.json` file is the first communication point with VTEX IO, holding important metadata about an app, such as its **name**, **version**, **vendor**, **description**, **dependencies**, etc.

Hence, keep in mind that every IO app must have a `manifest.json` file on its root folder.

# Manifest fields summary

Check the following snippet, which shows a manifest example and its supported fields. 

Click on each field to learn more about it.

<pre>
{
  "<a href="#name">name</a>": "app-name",
  "<a href="#vendor">vendor</a>": "vtex",
  "<a href="#version">version</a>": "1.0.0",
  "<a href="#title">title</a>": "App Name",
  "<a href="#description">description</a>": "Brief description of your app.",
  "<a href="#builders">builders</a>": {
      "react": "3.x"
  },
  "<a href="#scripts">scripts</a>": {
      "postreleasy": "vtex publish --verbose"
  },
  "<a href="#dependencies">dependencies</a>": {
      "vtex.styleguide": "9.x"
  },
  "<a href="#peerdependencies">peerDependencies</a>": {
      "vtex.store": "2.x"
  },
  "<a href="#policies">policies</a>": [...],
  "<a href="#settingsschema">settingsSchema</a>": {...},
  "<a href="#credentialtype">credentialType</a>": {...}
}
</pre>

For a real example of a `manifest.json` file, check [this file](https://github.com/vtex-apps/wordpress-integration/blob/d3ca9bd43b8d6797f162519d7b8a31ec755bd47d/manifest.json).

## name

The app name. It should concisely express the app's purpose. 

On the VTEX IO platform, apps' names are [kebab case](https://en.wiktionary.org/wiki/kebab_case). Basically, they must be comprised of lowercase letters separated by hyphens. Special characters, such as `*` and `@`, and numbers at the beginning of the name are not recommended.

<div style="text-align: right"><a href="#manifest-fields-summary">Manifest fields summary</a> 🔼</div>

## vendor

The app owner. That is, the VTEX account responsible for the app development, maintenance, and distribution.

If the app is to-be sold on VTEX App Store, the vendor is the one to profit from its installations. Therefore, remember the following: an app must have only one vendor. Even is the app is installed on multiple accounts, you shouldn't change the app's `vendor` value for each one of them. 

<div style="text-align: right"><a href="#manifest-fields-summary">Manifest fields summary</a> 🔼</div>

## version

The app version, according to the [Semantic Versioning 2.0.0](https://semver.org/).

<div style="text-align: right"><a href="#manifest-fields-summary">Manifest fields summary</a> 🔼</div>

## title

The app distribution name. This name is the one used in the Apps section from the Administrative Panel and in the VTEX App Store.

<div style="text-align: right"><a href="#manifest-fields-summary">Manifest fields summary</a> 🔼</div>

## description

A brief description explaining the app's purpose.

<div style="text-align: right"><a href="#manifest-fields-summary">Manifest fields summary</a> 🔼</div>

## builders

The list of builders used by the app. A builder is an abstraction to configure other IO services, such as `node`, `dotnet`, `react`, etc. It acts as an API service, responsible for processing and interpreting a directory from the app. Hence, it’s possible to use as many builders as you want in one single app.

For example, if you want to **develop React components** on an app, you should use the builder `react@3.x`, declaring it on the manifest:

```
"builders": {
    "react": "3.x"    
}
```

And create a `react` folder inside the app, placing there the component files. Each builder has its own set of rules and validation process.

>ℹ️ Follow this [link](https://developers.vtex.com/docs/vtex-io-documentation-builders) to learn more about Builders.

<div style="text-align: right"><a href="#manifest-fields-summary">Manifest fields summary</a> 🔼</div>

## scripts

The list of scripts the app runs.

<div style="text-align: right"><a href="#manifest-fields-summary">Manifest fields summary</a> 🔼</div>

## dependencies

The list of other VTEX IO apps that the app relies on to properly work.

The most recurrent use of VTEX IO apps as dependencies are for:

- Using VTEX Store Framework blocks.
- Importing React components from another app.
- Importing Typescript types from a GraphQL service app.
- Using GraphQL or REST definitions declared in another app.
- Implementing a GraphQL schema from another app.

>ℹ️ Follow this [link](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-dependencies/) to learn more about Dependencies.

<div style="text-align: right"><a href="#manifest-fields-summary">Manifest fields summary</a> 🔼</div>

## peerDependencies

The list of other apps that the app relies on to properly work. However, unlike regular dependencies, peer dependencies are not automatically installed in an account. Hence, these are mostly used in cases an app relies on paid apps or a specific version of an app.

>ℹ️ Follow this [link](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-peerdependencies/) to learn more about Peer Dependencies.

<div style="text-align: right"><a href="#manifest-fields-summary">Manifest fields summary</a> 🔼</div>

## policies

The list of policies, responsible for granting permissions to the app in case it needs access to external services or specific data from other sources, such as external APIs.

>ℹ️ Follow this [link](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-policies/) to learn more about Policies.

<div style="text-align: right"><a href="#manifest-fields-summary">Manifest fields summary</a> 🔼</div>

## settingsSchema

The layout settings of the app, displayed in the VTEX Admin. 

Using [JSON Schema](https://json-schema.org/), it’s possible to accept multiple fields with multiple data types. The persistence of the information is taken care by the VTEX Platform, and you may fetch the current configuration on your app code.

For example, on the `vtex.wordpress-integration` app, the following `settingsSchema`:

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

![settingsschema](https://user-images.githubusercontent.com/60782333/92953164-a5c8cb80-f437-11ea-87ba-0458b68ed0c9.png)

<div style="text-align: right"><a href="#manifest-fields-summary">Manifest fields summary</a> 🔼</div>

## [DEPRECATED] credentialType

**Deprecated field.**

The credential type. When set as `relative`, a request from the app can only be performed if the app and the role who called it have the required permissions. When set as `absolute`, if the app has the necessary permission, a request from the app can be performed.

<div style="text-align: right"><a href="#manifest-fields-summary">Manifest fields summary</a> 🔼</div>
