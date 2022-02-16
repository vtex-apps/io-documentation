---
title: Building a Product Details Page
description: "Learn how simple can be to build and custom a Product Details Page with our flexible components”"
date: "2019-08-29"
tags: ["pdp", "product", "product-page", "product-details-page"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/templates/building-a-product-details-page.md"
---

# Building a Product Details Page

> ⚠️ For this recipe, knowledge of how the flex-layout works is required. If you have any doubts regarding this, we strongly recommend you access this [documentation](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-using-flex-layout).

### Introduction

Your store's Product Page can be customized by simply changing the `store.product` block in your `store-theme` source code. 
The `store.product` is a block with child dependencies, which means it consists of other blocks. Since it is flexible, its child blocks can be declared using `flex-layout` to easily build a responsive page.

The `store.product` accepts all blocks allowed by the `store` and `flex-layout` blocks as child dependencies, as well as the following blocks list:

```json
"product-add-to-list-button"
"product-details"
"product-kit"
"product-reviews"
"product-questions-and-answers"
"product-rating-summary"
"product-rating-inline"
"product-images"
"product-brand"
"product-name"
"product-price"
"sku-selector"
"buy-button"
"product-separator"
"product-description"
"product-specifications"
"product-quantity"
"breadcrumb"
"shipping-simulator"
"availability-subscriber"
"share"
"product-highlights"
"product-availability"
"product-identifier"
"blog-related-posts"
"product-assembly-options"
"product-teaser.product"
```

> ℹ *You can always check out the full and updated list [here](https://github.com/vtex-apps/store/blob/master/store/interfaces.json#L49).*

## Practical example

Let's take a look at our demo store, [Storetheme](https://storetheme.vtex.com/). It has a good example of how to use the `store.product` flexible block:

![storetheme-product-details-page](https://user-images.githubusercontent.com/52087100/64383385-26c2db00-d00c-11e9-96d4-d3b7ecaf0376.png)

Its definition is as follows:

```json
{
  "store.product": {
    "children": [
      "flex-layout.row#product-breadcrumb",
      "flex-layout.row#product-main",
      "shelf.relatedProducts"
    ]
  },
  "flex-layout.row#product-breadcrumb": {
    "props": {
      "marginTop": 4
    },
    "children": ["breadcrumb"]
  },
  "flex-layout.row#product-main": {
    "props": {
      "colGap": 7,
      "rowGap": 7,
      "marginTop": 4,
      "marginBottom": 7,
      "paddingTop": 7,
      "paddingBottom": 7
    },
    "children": ["flex-layout.col#product-image", "flex-layout.col#right-col"]
  },
  "flex-layout.col#product-image": {
    "props": {
      "width": "60%",
      "rowGap": 0
    },
    "children": ["product-images"]
  },
  "product-images": {
    "props": {
      "displayThumbnailsArrows": true
    }
  },
  "flex-layout.col#right-col": {
    "props": {
      "preventVerticalStretch": true,
      "rowGap": 0
    },
    "children": [
      "product-name",
      "product-rating-summary",
      "product-price#product-details",
      "product-separator",
      "product-quantity",
      "product-identifier.product",
      "sku-selector",
      "flex-layout.row#buy-button",
      "availability-subscriber",
      "shipping-simulator",
      "share#default"
    ]
  },
  "product-price#product-details": {
    "props": {
      "showInstallments": true,
      "showSavings": true
    }
  },
  "flex-layout.row#buy-button": {
    "props": {
      "marginTop": 4,
      "marginBottom": 7
    },
    "children": ["buy-button"]
  },

  "share#default": {
    "props": {
      "social": {
        "Facebook": true,
        "WhatsApp": true,
        "Twitter": false,
        "Pinterest": true
      }
    }
  }
}

```

As you can see, the `store.product` child dependencies define 5 blocks, the first two being `flex-layout.row`. 

### Breadcrumb

The first row is only declaring the [breadcrumb](https://developers.vtex.com/vtex-developer-docs/docs/vtex-breadcrumb/) and you can see it here:

![](https://i.ibb.co/ZhNry22/image.png)

```json
"flex-layout.row#product-breadcrumb": {
    "props": {
      "marginTop": 4
    },
    "children": ["breadcrumb"]
  },
```

Notice that above that it sets out to render the [breadcrumb](https://developers.vtex.com/vtex-developer-docs/docs/vtex-breadcrumb/) block through its `child` array.  If you want to customize the breadcrumb, with changes to its props, you can declare the breadcrumb block and define it according to your goal. For instance:
 
```json
"breadcrumb": {
    "props": {
        "showOnMobile": true
    }
}
```

The second row is the one showing the image, while the right column displays name, price, sku selector, button, etc. as shown below:

```json
 "flex-layout.row#product-main": {
    "props": {
      "colGap": 7,
      "rowGap": 7,
      "marginTop": 4,
      "marginBottom": 7,
      "paddingTop": 7,
      "paddingBottom": 7
    },
    "children": ["flex-layout.col#product-image", "flex-layout.col#right-col"]
  },
```

Notice that the second row defines two columns, `flex-layout.col#product-image` and `flex-layout.col#right-col`:

```json
"flex-layout.col#product-image": {
    "props": {
      "width": "60%",
      "rowGap": 0
    },
    "children": ["product-images"]
  },
  "product-images": {
    "props": {
      "displayThumbnailsArrows": true
    }
  },
  "flex-layout.col#right-col": {
    "props": {
      "preventVerticalStretch": true,
      "rowGap": 0
    },
    "children": [
      "product-name",
      "product-price#product-details",
      "product-separator",
      "product-quantity",
      "product-identifier.product",
      "sku-selector",
      "flex-layout.row#buy-button",
      "shipping-simulator",
      "share#default"
    ]
  },
```

### Product images

The left column is the one with the [product-images](https://developers.vtex.com/vtex-developer-docs/docs/vtex-store-components-productimages) since it was the first one to be declared.

![](https://i.ibb.co/ns8sP0Y/image.png).

As you can see from the rendering, the right column has many child dependencies:

![storetheme-product-details-page](https://user-images.githubusercontent.com/52087100/64394071-ddce4f00-d02a-11e9-8c7a-2a4b346d59e3.png)

### Product name

It starts with a [product-name](https://developers.vtex.com/vtex-developer-docs/docs/vtex-store-components-productname), used to display the product name, along with its SKU name, if desired.

![productdetailspage-productname](https://user-images.githubusercontent.com/52087100/64384533-6f7a9400-d00c-11e9-91f3-82b1cb394d88.png)

### Product price

Right below it, we can find the [product-price](https://developers.vtex.com/vtex-developer-docs/docs/vtex-store-components-productprice) displaying a properly formatted selling price. You can set it to show the list price (if it's different), installments, etc. Check out below an example of a Product Price displaying both the sale and the list price:

![productdetailspage-productprice](https://user-images.githubusercontent.com/52087100/64384891-83be9100-d00c-11e9-9f54-5e501cb7c9a0.png)

Below the Product Price we have the `product-separator`, a block that just draws a line in your Product Page.

### Product quantity

Then, we have the [product-quantity](https://developers.vtex.com/vtex-developer-docs/docs/vtex-product-quantity). With this block, you can let users choose how many items are added to the cart.

![productdetailspage-productquantity](https://user-images.githubusercontent.com/52087100/64385226-9933bb00-d00c-11e9-8332-ff8c49b7cea7.png)

### Product Identifier

Scrolling down, below the Product Quantity component, we arrive at the [product-identifier](https://developers.vtex.com/vtex-developer-docs/docs/vtex-product-identifier). This component allows you to show the user the product identifier. 

![productdetailspage-productidentifier](https://user-images.githubusercontent.com/52087100/64385400-bbc5d400-d00c-11e9-8d39-852b880a753f.png)

You can then customize it with different props, choosing the label you want before/in front of the identifier, the display mode and more.

### SKU Selector

We then have a really important component: the [SKU Selector](https://developers.vtex.com/vtex-developer-docs/docs/vtex-store-components-skuselector). It allows the user to choose his desired SKU, automatically hiding impossible combinations or indicating combinations that are currently unavailable. 

![productdetailspage-skuselector](https://user-images.githubusercontent.com/52087100/64385450-d8faa280-d00c-11e9-8630-2dc07b7dc010.png)

### Buy button

The [buy-button](https://github.com/vtex-apps/store-components/tree/master/react/components/BuyButton) is the classic component that adds a SKU to the cart. You can customize it to show a successful message, to redirect the user to the Cart page immediately, etc.

![productdetailspage-buybutton](https://user-images.githubusercontent.com/52087100/64385524-fdef1580-d00c-11e9-86f8-76edaf02263b.png)

### Shipping simulator 

Your store can also have a [shipping-simulator](https://developers.vtex.com/vtex-developer-docs/docs/vtex-store-components-shippingsimulator). It allows users to fill in their postal code to then display the available shipping options and their respective prices for that cart.

![productdetailspage-shippingsimulator](https://user-images.githubusercontent.com/52087100/64385562-1bbc7a80-d00d-11e9-9a22-de78ebb49050.png)

### Share 

Finally, we have the [Share](https://developers.vtex.com/vtex-developer-docs/docs/vtex-store-components-share) component, which allows product sharing on social media. 

![productdetailspage-share](https://user-images.githubusercontent.com/52087100/64385594-368eef00-d00d-11e9-8cb8-90ea770d55ac.png)

By customizing its props, you can control which options will be shown to the user:

```json
"share#default": {
    "props": {
      "social": {
        "Facebook": true,
        "WhatsApp": true,
        "Twitter": false,
        "Pinterest": true
      }
    }
  }
```

Notice that in this block we are hiding the Twitter option from our sharing list. The available social media platforms for now are: `Facebook`,`Twitter`,`Telegram`,`WhatsApp`,`Google+`,`Pinterest` and `E-mail`.

After this right column is done, we start to render the blocks defined under them in our `store.product` block.

### Related products

The Related Products Shelf (`shelf.relatedProducts`) is a [Shelf](https://developers.vtex.com/vtex-developer-docs/docs/vtex-shelf/) component that displays products related to the one you are browsing. 

The related products displayed in a product page can be defined through your store's admin Catalog. As you can see above, the product we are using as example does not have any. But it should look exactly like this:

![](https://i.ibb.co/QpyMyXM/image.png)

The `shelf.relatedProducts` block lets you choose between different recommendation types. The recommendation property can be one of the following values: `['similars', 'view', 'buy', 'accessories', 'viewAndBought', 'suggestions']`.

Here is a brief example of a Related Products Shelf:

```json
"shelf.relatedProducts": {
    "props": {
        "recommendation": "view",
        "productList": {
            "titleText": "Who saw also saw",
            "itemsPerPage": 3
        }
    }
}
```

## Mobile

Keep in mind that the `flex-layout` may suffer modifications if you are on mobile mode. You can check out the [Flex Layout](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-using-flex-layout) recipe for more information.
