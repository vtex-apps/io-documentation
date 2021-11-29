---
title: Segmenting the search result
description: "Sometimes you want search results to be segmented by user information, like email, for example. This guide will help you with that."
date: "2021-11-29"
tags: ["segment", "search", "b2b"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store-management/segmenting-the-search-result.md"
---

# Segmenting the search result

In some situations, especially in B2B accounts, it is necessary to segment the products that will appear to the user based on information, such as email.
See the example below. For each user entered, the search result is different.

## Setup
Creating segmentation rules is easy and customizable. First of all, install the following apps in your test workspace.
```
vtex.search-session@0.x
vtex.search-segment-graphql@0.x
```
The `vtex.search-session` is responsible for managing the user session, while the `vtex.search-segment-graphql` is where the GraphQL schema is declared.

Now, clone the [`vtex.search-segment-resolver`](https://github.com/vtex-apps/search-segment-resolver) project. This project is just a boilerplate and you will edit it however you like. You just need to follow these steps:

1. Go to the `manifest.json` and change the `vendor` to your own account.

2. Change the implementation of the `searchSegment` function on `node/resolvers/segmentSearch.ts` file. The `searchSegment` receives a variable called `args`, and has the following interface:

```ts
interface SearchSegmentInput {
    // User email
    userEmail?: string
    // Whether the user is authenticated or not.
    isAuthenticated?: boolean
    // Arrrao of selected facets (optionally you can control it by the session itself)
    selectedFacets?: SelectedFacet[]
}
```

The `searchSegment` function output has the following interface:

```json
[
    {
        "key": "mykey",
        "value": "myValue"
    }
]
```

It's just an array of facets. For example, if you want to segment the search by the category "shoes", the function needs to return `[{"key": "category-1", "value": "shoes"}]`.

If you want to segment by email domain, for example, the function would be something like this:

```ts
export const queries = {
  searchSegment: async (ctx: any, args: SearchSegmentInput, __: Context) => {
    const userEmail = args.userEmail
    const domain = userEmail.split('@')[1]

    return domain === 'vtex.com.br' ? [{ key: 'productClusterIds', value: '123' }] : [{ key: 'productClusterIds', value: '456' }]
  },
}
```
In this example, if the email has the `vtex.com.br` domain it will filter by the collection `123`, otherwise, it will filter by `456`.

3. Link your app to your test workspace. Make sure everything is working fine.

4. Now you can release, deploy and install the app on your production workspace.

