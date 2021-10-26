---
title: Building a horizontal Product Summary
description: "Learn now all best practices for rendering images in your store's theme and improve the way in which images are cropped, rendered and displayed to end users"
date: "2020-12-14"
tags: ["product-summary", "horizontal", "product-summary", "flex-layout"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/edit/master/docs/en/Recipes/templates/building-a-horizontal-product-summary.md"
---

# Building a horizontal Product Summary

The [Product Summary](https://developers.vtex.com/vtex-developer-docs/docs/vtex-product-summary) is a VTEX native app responsible for displaying important product data in your store's components, such as the Shelf and the Minicart.

![product-summary-vertical](https://user-images.githubusercontent.com/52087100/102239663-dbb59a00-3ed5-11eb-882f-48672d6f1325.png)

Thanks to the [Flex Layout app](https://developers.vtex.com/vtex-developer-docs/docs/vtex-flex-layout), it is possible to customize the default presentation showed above and thereby display the Product Summary blocks in a **horizontal alignment** to your users:
 
![horizontal-product-summary](https://user-images.githubusercontent.com/52087100/102240101-436be500-3ed6-11eb-84a1-0c957cf4f4d6.png)

Learn in the instructions below how to use the powerful combination between the Flex Layout and the Product Summary apps in order to display your product data horizontally.

## Step by step

>ℹ️ This recipe requires previous understanding of the [Flex Layout app](https://developers.vtex.com/vtex-developer-docs/docs/vtex-flex-layout). It is strongly advised that you read the app documentation before performing the steps below!

1. Make sure the Flex Layout app has been declared as a theme's dependency in the `manifest.json` file:

```json
"dependencies": {
  "vtex.flex-layout": "0.x"
}
```

2. Add the `flex-layout.row` block as a child of the `product-summary.shelf` and/or the `product-summary` blocks, according to the desired scenario:

```json
"product-summary.shelf": {
  "children": ["flex-layout.row#product-summary-mobile"]
},
```

>ℹ️ The `flex-layout.row` block allows its children to be displayed side by side on the UI.

>⚠️ Notice that the block naming always depends on your store scenario. In the example above, `#product-summary-mobile` is only being used for identification purposes.

3. Add the `flex-layout.col` blocks as children of the `flex-layout.row` block to define the desired disposition of elements on the screen - the first `flex-layout.col`'s children will be displayed on the left side of the horizontal Product Summary, whereas the second will be on the right side:

```json
"flex-layout.row#product-summary-mobile": {
  "children": [
    "flex-layout.col#product-image",
    "flex-layout.col#product-summary-details"
  ],
},
```

4. Add the [`product-summary-image` block](https://developers.vtex.com/vtex-developer-docs/docs/vtex-product-summary-productsummaryimage) to the `flex-layout.col#product-image`'s children list and then declare it as desired: 

```json
"flex-layout.col#product-image": {
  "children": ["product-summary-image#shelf"]
},
"product-summary-image#shelf": {
  "props": {
    "showBadge": false,
    "aspectRatio": "1:1",
    "maxHeight": 300
  }
},
```

5. Add the desired blocks responsible for displaying product data to the `flex-layout.col#product-summary-details`'s children list and then declare them as desired. For example:

```json
"flex-layout.col#product-summary-details": {
  "children": [
    "product-summary-name",
    "product-summary-space",
    "product-list-price",
    "flex-layout.row#selling-price-savings",
    "product-installments",
    "product-summary-sku-selector#buy-together"
  ],
  "props": {
    "marginLeft": 4
  },
},
"flex-layout.row#selling-price-savings": {
  "children": [
    "product-selling-price",
    "product-price-savings#summary"
  ],
  "props": {
    "colGap": 2,
    "preserveLayoutOnMobile": true,
    "preventHorizontalStretch": true,
    "marginBottom": 4
  },
},
"product-price-savings#summary": {
  "props": {
    "markers": ["discount"]
  }
},
"product-summary-sku-selector#buy-together": {
  "props": {
    "thumbnailImage": "skuvariation",
    "imageHeight": 28,
    "blockClass": "buyTogether",
    "visibility": "more-than-one"
  }
}
```

6. [Deploy your changes](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-making-your-theme-content-public/).
