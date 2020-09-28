---
title: Managing landing pages in cross-border stores
description: "Create landing pages for your cross-border store."
date: "09/28/2020"
tags: ["custom", "cross-border", "landing", "page"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store-management/managing-landing-pages-in-cross-border-stores.md"
---

# Managing landing pages in cross-border stores

You may want to [create custom landing pages](https://developers.vtex.com/docs/vtex-io-documentation-creating-a-new-custom-page) to attend your store's specific needs. In this case, you must create a template and a URL to go with it.

In a **cross border** environment, we suggest that you include the country code of its related *[binding](https://help.vtex.com/en/tutorial/what-is-binding--4NcN3NJd0IeYccgWCI8O2W?&utm_source=autocomplete)* in the path of your new landing page (e.g., `/UK/about-us`).

:warning: *Before creating a custom landing page, keep in mind that, in VTEX IO, some default pages with predefined URLs are already available to you, such as:*

- *`store.home` - Home page*
- *`store.product`- Product page*
- *`store.search` - Search Results page*
- *`store.account` - Client Account page*
- *`store.login` - Login page*
- *`store.orderplaced` - Order Placed page*

Once you create a new custom landing page, its path is directly related to your store's *default binding*. 

However, if your store is part of a **cross border** environment, you might want to have specific landing pages for each one of your *bindings*. 

If that's the case, after creating your custom page, you must link it to the desired *binding* as in the following [step by step](#linking-a-landing-page-to-a-binding).

Finally, you may want to remove it from the *default binding*. For that, check the following step by step on how to [unlink a landing page from a specific *binding*.](#unlinking-a-landing-page-from-a-binding)

## Step by step

### Linking a landing page to a binding

1. [Install](https://developers.vtex.com/docs/vtex-io-documentation-installing-an-app) the `vtex.admin-graphql-ide@3.x` app using your terminal.
2. In your browser, access your store's admin and go to the GraphQL IDE section.
3. [Check your store's binding id](https://developers.vtex.com/docs/checking-your-stores-binding-id) and save the `id` value of the binding you want to have your new custom landing page live.
4. Now, from the GraphQL IDE dropdown list, choose the `vtex.rewriter` app.
5. Run the following query to get the internal data related to your custom path:

```
{
  internal {
    get(path: "/{URL}") {
      from
      declarer
      type
      id
      query
      binding
      endDate
      imagePath
      imageTitle
      resolveAs
      origin
      disableSitemapEntry
    }
  }
}
```

:warning: *Remember to replace the values between the curly brackets according to your scenario.*

6. Save the returned information.
7. Erase the previous query and fill in the main text box with the following mutation command:

```
mutation saveInternal($args: InternalInput!){
  internal {
    save(route: $args) {
      id
    }
  }
}
```

8. Click on Query Variables at the bottom of the page and, according to the following example and the following explanations, fill in the Query Variables section.

```json
{
  "args": {
        "from": "/{URL}",
        "declarer": "vtex.store@2.x",
        "type": "userRoute",
        "id": "vtex.store@2.x:store.custom::{URL}",
        "query": null,
        "binding": "7cf37a3b-efc0-4e47-8201-d8b58kd4d3fd",
        "endDate": null,
        "imagePath": null,
        "imageTitle": null,
        "resolveAs": null,
        "origin": "vtex.pages-graphql@2.99.1",
        "disableSitemapEntry": null
	}
}
```

Replace the values inside `args` with the information obtained in step 5. Finally, replace the `binding` value with the `id` obtained in step 3.

Done! Now, your landing page will be accessible in the default and in the desired binding. 

If you want to link the same landing page to other bindings, just repeat this process.

Also, if you don't want to have this landing page in the default binding, check the following section on how to [unlink a landing page from a binding.](#unlinking-a-landing-page-from-a-binding)

### Unlinking a landing page from a binding

1. In your browser, access your store's admin and go to the GraphQL IDE section.
2. [Check your store's binding id](https://developers.vtex.com/docs/checking-your-stores-binding-id) and save the `id` value of the binding you want to delete a custom landing page.
3. Now, from the GraphQL IDE dropdown list, choose the `vtex.rewriter` app.
4. Fill in the main text box with the following mutation command:

```
mutation deleteInternal($args:RouteLocator){
  internal{
    delete(path:"/{URL}",locator:$args){
      from
    }
  }
}
```

:warning: *Remember to replace the values between the curly brackets according to your scenario.*

5. Click on Query Variables at the bottom of the page and fill in the Query Variables section as in the example below, adapting it to your scenario. 
 
```
{
  "args": {
    "from": "/{URL}",
    "binding": "{bindingId}"
  }
}
```

Once you run this mutation, you'll delete the custom landing page, related to the specified `{URL}`, from the binding related to the specified `{bindingId}`.
