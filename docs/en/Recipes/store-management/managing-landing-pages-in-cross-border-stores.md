---
title: Managing landing pages in cross-border stores
description: "Create landing pages for your cross-border store."
date: "09/28/2020"
tags: ["custom", "cross-border", "landing", "page"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store-management/managing-landing-pages-in-cross-border-stores.md"
---

# Managing landing pages in cross-border stores

To meet your store's specific needs, you may want to [create custom landing pages](https://developers.vtex.com/docs/vtex-io-documentation-creating-a-new-custom-page). In a cross-border context, you may also want them to be distinct depending on the locations in which your shop operates.

In this case, after creating a custom page, you must link its path to the desired *binding* as presented in the [Linking a landing page to a binding](#linking-a-landing-page-to-a-binding) section.

Finally, you may want to remove your landing page from the *default binding*. For that, check the [Unlinking a landing page from a specific *binding*.](#unlinking-a-landing-page-from-a-binding) section.

## Before you start

Before proceeding any further with this step-by-step:
- Create your custom landing pages as presented in [this](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-creating-a-new-custom-page) guide.
- [Check your account's binding ids](https://developers.vtex.com/docs/checking-your-stores-binding-id) and keep the returned data with you.

It's also worth noting that **this technique only works if the custom pages were created via the CMS** rather than the Store Theme.

## Step by step

### Linking a landing page to a binding

After creating a new page, the page's route becomes available only in the store associated with your account's default binding. The following shows how to associate your page with the desired binding.

1. Open the terminal and install the `vtex.admin-graphql-ide@3.x` app:
  
  ```sh
  vtex install vtex.admin-graphql-ide@3.x
  ```

2. Open the Admin and go to the GraphQL IDE section.
3. From the GraphQL IDE dropdown list, choose the `vtex.rewriter` app.
4. Run the following query to get the internal data related to your custom page's path.
  - _Replace the values between the curly brackets according to your scenario._

  ```graphql
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

5. Copy and save the returned data.
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

7. Click on *Query Variables* at the bottom of the page and fill in the *Query Variables* section as in the following:

``` json
{
    "args": {
        "from": "/US/about-us",
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

- Replace the `args` values with the information obtained in Step 4.
- Update the `binding` value with the binding `id` of the store you want to have your new custom landing page live. 

Done! Now, your landing page will be accessible in the *default* binding as well as in the desired binding.

> ℹ *If you want to link the same landing page to other stores, just repeat this process considering their respective binding `id`s.*

If you don't want to have this landing page in the *default* binding, check the following section on [Unlinking a landing page from a binding.](#unlinking-a-landing-page-from-a-binding)

### Unlinking a landing page from a binding

1. Open the Admin and go to the GraphQL IDE section.
2. From the GraphQL IDE dropdown list, choose the `vtex.rewriter` app.
3. Fill in the main text box with the following mutation.
  - _Replace the values between the curly brackets according to your scenario._

  ```graphql
  mutation deleteInternal($args:RouteLocator){
    internal{
      delete(path:"/{URL}",locator:$args){
        from
      }
    }
  }
  ```

4. Click on *Query Variables* at the bottom of the page and fill in the *Query Variables* section as in the following.
  - _Replace the values between the curly brackets according to your scenario._

  ```json
  {
    "args": {
      "from": "/{URL}",
      "binding": "{bindingId}"
    }
  }
  ```
  
Once you run this mutation, you'll remove the page related to the specified `{URL}` from the `{bindingId}` provided.

## Next steps

- [Indicating alternate versions of localized pages in cross border stores](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-indicating-alternate-pages-in-cross-border-stores)

## Related resources

- [Binding](https://help.vtex.com/en/tutorial/what-is-binding--4NcN3NJd0IeYccgWCI8O2W?&utm_source=autocomplete)
- [Creating a new custom page](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-creating-a-new-custom-page)
- [Cross-border stores](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-cross-border-stores)
