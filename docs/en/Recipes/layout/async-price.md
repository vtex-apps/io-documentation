---
title: Adding asynchronous price to the product-summary
description: "Get the most up-to-date prices without dealing with a increase in the page response time"
date: "10/21/2020"
tags: ["price", "simulation"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/edit/master/docs/en/Recipes/layout/async-price.md"
---

# Adding asynchronous price to the product-summary

## Introduction

For some stores, it is essential to have the most up to date price. But, since this price is built on the server-side, the page response time is increased.

This recipe shows you how to keep the response time by requesting the most up-to-date price on the client-side instead of the server-side.

![priceasync](https://user-images.githubusercontent.com/40380674/96735041-85265680-1391-11eb-80e9-2eb35607fd72.gif)

## Step by step

1. Make sure your store is not requesting the price on the server-side by setting the `simulationBehavior` prop to `skip`.

```diff
"store.search": {
  "blocks": [
    "search-result-layout"
  ],
  "props": {
    "context": {
+     "simulationBehavior": "skip"
    }
  }
},
```

2. Add the following **dependencies** to your theme's `manifest.json` file:

```json
"vtex.product-summary": "2.x",
"vtex.product-price": "1.x"
```

3. Add the `isPriceAsync` prop to your `product-summary.shelf` block. Set its value to `true`.

```diff
"product-summary.shelf": {
  "props": {
+   "isPriceAsync": true
  },
  "children": [
    // other children
    "product-list-price#summary",
    "flex-layout.row#selling-price-savings",
    "product-installments#summary",
    "add-to-cart-button",
  ]
}
```

4. Wrap the price blocks in the `product-price-suspense`.

```diff
{
  "product-summary.shelf": {
    "props": {
     "isPriceAsync": true
    },
    "children": [
      // other children
-     "product-list-price#summary",
-     "flex-layout.row#selling-price-savings",
-     "product-installments#summary",
-     "add-to-cart-button",
+     "product-price-suspense"
   ]
  },
+ "product-price-suspense": {
+   "children": [
+     "product-list-price#summary",
+     "flex-layout.row#selling-price-savings",
+     "product-installments#summary",
+     "add-to-cart-button"
+   ]
+ },
}
```

And that's it! Now you can have the most up-to-date price without dealing with a increase in the page response time.
