---
title: Interfaces
description: "Interfaces concept"
date: "2020-04-09"
tags: ["interface"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/docs/en/Concepts/edition-app.md"
---

# Interfaces

Interface is what links a block to a **React component**.

To make the concept more tangible, think about the `vtex.product-summary` app. In addition to exporting different blocks that are then declared and configured in your theme's code, the app also exports React components that are related to these blocks and which are then rendered on your store's front end. 

This means that **for every exported block, the app also defines a React component that's linked to that block**. This link is done in the app's `interfaces.json` and is used by the Store Builder to correctly build the store's front end. 

For example:

```jsonc
// /store/interfaces.json
{
  "product-summary": {
    "component": "ProductSummary",
    "composition": "children",
    "content": {
      "$ref": "app:vtex.product-summary#/definitions/ProductSummary"
    }
  }
}
```
