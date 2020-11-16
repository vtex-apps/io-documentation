---
title: Managing landing pages in cross-border stores
description: "Create landing pages for your cross-border store."
date: "09/28/2020"
tags: ["custom", "cross-border", "landing", "page"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store-management/managing-landing-pages-in-cross-border-stores.md"
---

# Managing landing pages in cross-border stores

You may want to [create custom landing pages](https://developers.vtex.com/docs/vtex-io-documentation-creating-a-new-custom-page) to attend your store's specific needs. In this case, you must create a template and a URL path to go with it.

> ℹ *In a **cross border** environment, we suggest that you include the *country code* of its related *[binding](https://help.vtex.com/en/tutorial/what-is-binding--4NcN3NJd0IeYccgWCI8O2W?&utm_source=autocomplete)* in the path of your new landing page (e.g., `/UK/about-us` ).*

Once you create your new custom landing page, its path will be solely available in the store related to your account's *default binding*.

However, in a **cross border** context, you may want to have specific landing pages for each region your store is present.

In this case, after creating your custom page, you must link its path to the desired *binding* as in the following step by step on how to [link a landing page to a binding](#linking-a-landing-page-to-a-binding).

Finally, you may want to remove your landing page from the *default binding*. For that, check the following step by step on how to [unlink a landing page from a specific *binding*.](#unlinking-a-landing-page-from-a-binding)

## Step by step

> ⚠️ *Before proceeding any further with this step by step, [check your account's `binding` ids](https://developers.vtex.com/docs/checking-your-stores-binding-id) and keep the returned data with you. This information will be crucial for successfully performing the following steps.*

### Linking a landing page to a binding

1. [Install](https://developers.vtex.com/docs/vtex-io-documentation-installing-an-app) the `vtex.admin-graphql-ide@3.x` app using your terminal.
2. In your browser, access your account's admin and go to the GraphQL IDE section.
3. From the GraphQL IDE dropdown list, choose the `vtex.rewriter` app.
4. Run the following query, adapting it to your scenario, to get the internal data related to your custom page path.

```graphql
{
  internal {
    get(path: "/{URL}") {
      from
      declarer
      type
      id
    }
  }
}
```

> ⚠️ *Remember to replace the values between the curly brackets according to your scenario.*

5. Save the returned data.
6. Erase the previous query and fill in the main text box with the following mutation command.

``` graphql
mutation saveInternal($args: InternalInput!) {
  internal {
    save(route: $args) {
      id
    }
  }
}
```

7. Click on *Query Variables* at the bottom of the page and, according to the following example and the following explanations, fill in the *Query Variables* section.

``` json
{
    "args": {
        "from": "/US/about-us",
        "declarer": "vtex.store@2.x",
        "type": "userRoute",
        "id": "vtex.store@2.x:store.custom::us-about-us",
        "binding": "7cf37a3b-efc0-4e47-8201-d8b58kd4d3fd"
    }
}
```

- Replace the values inside `args` with the information obtained in step 4.
- For the `binding` property, fill in its value with the binding `id` of the store you want to have your new custom landing page live. 

Done! Now, your landing page will be accessible either in the *default* binding as in the desired binding.

> ℹ *If you want to link the same landing page to other stores, just repeat this process considering their respective binding `id`s.*

If you don't want to have this landing page in the *default* binding, check the following section on how to [unlink a landing page from a binding.](#unlinking-a-landing-page-from-a-binding)

### Unlinking a landing page from a binding

1. In your browser, access your account's admin and go to the GraphQL IDE section.
2. From the GraphQL IDE dropdown list, choose the `vtex.rewriter` app.
3. Adapting it to your scenario, fill in the main text box with the following mutation command:

```graphql
mutation deleteInternal($args:RouteLocator){
  internal{
    delete(path:"/{URL}",locator:$args){
      from
    }
  }
}
```

> ⚠️ *Remember to replace the values between the curly brackets according to your scenario.*

4. Click on *Query Variables* at the bottom of the page and, according to your scenario, fill in the *Query Variables* section as in the following:

```graphql
{
  "args": {
    "from": "/{URL}",
    "binding": "{bindingId}"
  }
}
```

Once you run this mutation, you'll delete the custom landing page, related to the specified `{URL}` , from the binding related to the specified `{bindingId}`.
