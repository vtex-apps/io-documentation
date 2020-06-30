# Dependencies

The dependencies property is a JSON object field (`dependencies`) in the app's `manifest.json` file.  

This field **specifies which VTEX IO apps your app relies on to properly work**. Its semantics resembles [`package.json`'s `dependencies`](https://docs.npmjs.com/files/package.json#dependencies) property on Javascript apps. 

In practice, when an app is installed on a VTEX account, every app included in its manifest's `dependencies` field is automatically installed on the account.

Therefore, if your app needs to interact with another IO app, such as a VTEX API or a store framework block, you may declare it in the `manifest.json` file under `dependencies`, according to the following structure `"vtex.{appName}": "{majorVersion}.x"`. 

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

- Using [store component _blocks_](https://vtex.io/docs/apps/all/) _(example: [vtex.store-theme](https://github.com/vtex-apps/store-theme/blob/fee222b7d337ab35a57eeefe12c27181e9e9e257/store/blocks.jsonc#L12))_
- Importing React components from another app _(example: [vtex.order-placed](https://github.com/vtex-apps/order-placed/blob/ec6fab76f59ea4eacbea465419c3d026ae26be73/react/BankInvoiceSection.tsx#L3))_
- Importing Typescript types from a GraphQL service app _(example: [vtex.my-account](https://github.com/vtex-apps/my-account/blob/414c584e8f4acf0d9f3c5e9b37f6d946f7bfa8ac/react/typings/graphql/customerGreeting.gql.d.ts#L3))_
- Querying GraphQL or REST from another app _(example: [vtex.store-form](https://github.com/vtex-apps/store-form/blob/aca5bbde3c6b9ac311d656e6f5e9659f787ab196/react/graphql/getSchema.graphql))_
- Implementing a GraphQL schema from anoher app _(example: [vtex.search-resolver](https://github.com/vtex-apps/search-resolver/blob/49dccd1e5a952bf195aed929e8cca85a1cb29a79/node/index.ts#L4))_

<div class="alert alert-warning">When installing a VTEX IO app, its dependencies will be automatically installed on the logged account as well, but not as first-class apps (i.e.: indirect dependencies will not be able to declare routes).</div>
