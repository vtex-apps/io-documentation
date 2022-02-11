---
title: Building a Shelf
description: "The new Shelf configuration is practical, giving the component a lot of flexibility. Learn how to replace the old `shelf` block using the Slider Layout."
date: "2020-08-06"
tags: ["shelf", "product-list", "slider-layout"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/edit/master/docs/en/Recipes/templates/building-a-shelf.md"
---

# Building a Shelf 

The Shelf component is a product list that helps you to build your own shop window and work on your store's visual merchandising.

![shelf](https://user-images.githubusercontent.com/52087100/70079904-60dc5280-15e4-11ea-8ef6-0aa69cadd61d.png)

Using VTEX Store Framework, you can build two different shelves in your store: one to be rendered in the store home page, displaying any products you desire, and another one to be rendered in the product details page, displaying related products that may be interesting for users. 

By installing the [Shelf app](https://developers.vtex.com/vtex-developer-docs/docs/vtex-shelf), you can use the `shelf.RelatedProducts` block to build the Shelf in your store. However, when building the traditional Shelf to be displayed on your store home page, the Shelf app will not suffice since the `shelf` block was deprecated. 

Aiming to display a flexible product list in your home page, the traditional shelf component as we know is now configured using the [Product Summary List](https://developers.vtex.com/vtex-developer-docs/docs/vtex-product-summary-productsummarylist), the [Product Summary Shelf](https://vtex.io/docs/components/all/vtex.product-summary/) and the [Slider Layout](https://vtex.io/docs/components/all/vtex.slider-layout/) blocks.

>ℹ️ Info
> 
> Since these three blocks come from the [**Product Summary**](https://github.com/vtex-apps/product-summary) and the [**Slider-Layout**](https://github.com/vtex-apps/slider-layout) app, it is strongly recommended to check out each documentation in order to understand how the blocks work as well as the props available to set their behavior and consequently the Shelf behavior. 

Check out the instructions below for how it can be done.

## Step by step

1. Add the `product-summary` and the `slider-layout` apps to your theme's dependencies in the `manifest.json` file:

```json
  "dependencies": {
    "vtex.product-summary": "2.x",
    "vtex.slider-layout": "0.x"
  }
```

2. Add the `list-context.product-list` into your `store.home` theme template and add in its blocks list the `product-summary.shelf` block. Also, add as its children the `slider-layout` block. For example:

```json
{
  "product-summary.shelf#demo1": {
    "children": [
      "stack-layout#prodsum",
      "product-summary-name",
      "product-rating-inline",
      "product-summary-space",
      "product-summary-price",
      "product-summary-buy-button"
    ]
  },
  "list-context.product-list#demo1": {
    "blocks": ["product-summary.shelf#demo1"],
    "children": ["slider-layout#demo-products"]
  }
}
```

3. Declare the `product-summary.shelf` block and add the desired blocks as children, as shown in the example below. If you have any questions about structuring the block, check its [documentation](https://developers.vtex.com/vtex-developer-docs/docs/vtex-product-summary).

```json
{
  "list-context.product-list#demo1": {
    "blocks": ["product-summary.shelf#demo1"],
    "children": ["slider-layout#demo-products"]

  },

 +  "product-summary.shelf#demo1": {
 +   "children": [
 +    "product-summary-name",
 +    "product-summary-description",
 +    "product-summary-image",
 +    "product-summary-price",
 +    "product-summary-sku-selector",
 +    "product-summary-buy-button"
    ]
  }
}
```

4. Declare the `slider-layout` block, adding as desired child blocks and props. If you have any questions about structuring the block, check its [documentation](https://developers.vtex.com/vtex-developer-docs/docs/vtex-slider-layout).

```json
{
  "list-context.product-list#demo1": {
    "blocks": ["product-summary.shelf#demo1"],
    "children": ["slider-layout#demo-products"]

  },

    "product-summary.shelf#demo1": {
     "children": [
      "product-summary-name",
      "product-summary-description",
      "product-summary-image",
      "product-summary-price",
      "product-summary-sku-selector",
      "product-summary-buy-button"
    ]
  },

  + "slider-layout#demo-products": {
  +    "props": {
  +      "itemsPerPage": {
  +        "desktop": 1,
  +        "tablet": 1,
  +        "phone": 1
  +      },
  +      "infinite": true,
  +      "showNavigationArrows": "desktopOnly",
  +      "blockClass": "carousel"
  +    },
  +    "children": ["rich-text#1", "rich-text#2", "rich-text#3"]
 +  },
}
```

After the last step, you now have a functioning Shelf for your store.
