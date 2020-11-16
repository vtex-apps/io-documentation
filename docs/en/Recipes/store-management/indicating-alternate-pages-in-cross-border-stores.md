---
title: Indicating alternate versions of localized pages in cross border stores
description: "Learn how to improve cross-border store's SEO by indicating the alternate versions of a landing page."
date: "11/16/2020"
tags: ["alternate", "cross-border", "landing", "page"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store-management/indicating-alternates-pages-in-cross-border-stores.md"
---

# Indicating alternate versions of localized pages in cross border stores

If you have different versions of a [landing page](https://developers.vtex.com/docs/vtex-io-documentation-creating-a-new-custom-page) for each region your store is present, we recommend that you save them as `alternate` versions.

This way, search engines will be aware of the different versions of your page and able to provide the right content to the right audience.

> ℹ️ *Notice that this is especially useful for improving your store's SEO.*

For implementation details, check the following step by step.

## Step by step

1. [Install](https://developers.vtex.com/docs/vtex-io-documentation-installing-an-app) the `vtex.admin-graphql-ide@3.x` app using your terminal.
2. In your browser, access your account's admin and go to the GraphQL IDE section.
3. From the GraphQL IDE dropdown list, choose the `vtex.rewriter` app.
4. Run the following query to get the internal data related to the specified page `path`.

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

```json
{
    "args": {
        "from": "/US/about-us",
        "declarer": "vtex.store@2.x",
        "type": "userRoute",
        "id": "vtex.store@2.x:store.custom::us-about-us",
        "alternates": [
            {
                "binding": "7cf37a3b-efc0-4e47-8201-d8b58kd4d3fd",
                "path": "/BR/sobre-nos"
            },
            {
                "binding": "8cf37a3b-edc0-4a47-8241-d8b58kfsd3fd",
                "path": "/UK/about-us"
            }
        ]
    }
}
```

- Replace the `from`, `declarer`, `type`, and `id` values with the information obtained in step 4.
- Regarding the `alternates` field, fill in the `binding` and `path` values according to the alternate landing page's data.

> ⚠️ *If you don't know the `binding` values of your stores, follow [this step by step on checking your account's `binding` ids](https://developers.vtex.com/docs/checking-your-stores-binding-id).*
