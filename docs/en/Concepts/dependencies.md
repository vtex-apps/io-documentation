# Dependencies

The dependencies property is a JSON object field (`dependencies`) in the app's `manifest.json` file.  

This field **specifies which VTEX IO apps your app relies on to properly work**. Its semantics resembles [`package.json`'s `dependencies`](https://docs.npmjs.com/files/package.json#dependencies) property on Javascript apps. 

In practice, when an app is installed on a VTEX account, every app included in its manifest's `dependencies` field is automatically installed on the account.

Therefore, if your app needs to interact with another IO app, such as a VTEX API or a store framework block, you may declare it in the `manifest.json` file under `dependencies`, according to the following structure `"{account}.{appName}": "{majorVersion}.x"`. 

The `dependencies` object of your app's `manifest.json` file may look something like this:

```json
  "dependencies": {
    "vtex.blog-interfaces": "0.x",
    "vtex.store": "2.x",
    "vtex.styleguide": "9.x",
    "vtex.store-components": "3.x",
    "vtex.shelf": "1.x",
    "vtex.product-summary": "2.x",
    "vtex.search-graphql": "0.x",
    "vtex.search-page-context": "0.x",
    "vtex.css-handles": "0.x"
  }
```

The most recurrent use of VTEX IO apps as dependencies are for:

- Using [VTEX Store Framework blocks](https://developers.vtex.com/vtex-developer-docs/docs/overview-5).
- Importing React components from another app.
- Importing Typescript types from a GraphQL service app.
- Using GraphQL or REST definitions declared in another app.
- Implementing a GraphQL schema from another app.

>⚠️ When installing a VTEX IO app, its dependencies will be automatically installed on the logged account as well, but not as first-class apps. That means that indirect dependencies won't be able to declare routes.
