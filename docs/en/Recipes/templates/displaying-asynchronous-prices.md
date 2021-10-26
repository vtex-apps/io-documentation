---
title: Displaying asynchronous prices
description: "Learn how to get the most up-to-date prices without dealing with an increase in the page response time!"
date: "2020-11-18"
tags: ["price", "async", "product-summary"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/templates/displaying-asynchronous-prices.md"
---

# Displaying asynchronous prices

Although useful to enhance user experience, displaying the most up-to-date prices comes at the heavy cost of increasing your store's page response time. 

This is due to the fact that fetching the newest prices in your store database relies on making a new request to the server every time a product is rendered on the interface. 

A favorable way out is to set your store to fetch product prices on the client-side, promoting a decrease of response time in your pages in order to display the *asynchronous prices*.

> ℹ️ **Asynchronous prices do not mean outdated**. They are product prices stored in the browser cache according to the user navigation. If your store does not routinely update product prices, it is strongly recommended to display asynchronous prices instead. 

![priceasync](https://user-images.githubusercontent.com/40380674/96735041-85265680-1391-11eb-80e9-2eb35607fd72.gif)

Learn below how to set your store up to decrease page response time with asynchronous prices!

## Step by step

1. Ensure that your store is not fetching the price data on the server-side by setting the `simulationBehavior` prop (from the [Search Result](https://developers.vtex.com/vtex-developer-docs/docs/vtex-search-result/) app) to `skip`:

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

2. Ensure that the [Product Summary](https://developers.vtex.com/vtex-developer-docs/docs/vtex-product-summary/) and the [Product Price](https://developers.vtex.com/vtex-developer-docs/docs/vtex-product-price/) apps are listed as dependencies in your theme's `manifest.json` file:

```json
"dependencies": {
  "vtex.product-summary": "2.x",
  "vtex.product-price": "1.x"
}  
```

3. Add the `priceBehavior` prop to your [`product-summary.shelf`](https://developers.vtex.com/vtex-developer-docs/docs/vtex-product-summary/product-summary-shelf/) block and set its value to `async`:

```diff
"product-summary.shelf": {
  "props": {
+   "priceBehavior": "async"
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

4. Wrap the all price blocks under the `product-price-suspense` block (from the [Product Prices app](https://developers.vtex.com/vtex-developer-docs/docs/vtex-product-price/)):

```diff
{
  "product-summary.shelf": {
    "props": {
     "priceBehavior": "async"
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
+ }
}
```
