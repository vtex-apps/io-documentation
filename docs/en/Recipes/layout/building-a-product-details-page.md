---
title: Building a Product Details Page
description: "Custom product pages are simple to build with our flexible components"
date: "2019-08-29"
tags: ["pdp", "product", "product-page", "product-details-page"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/layout/building-a-product-details-page.md"
---

# Building a Product Details Page

<div class="alert alert-warning">
For this recipe, knowledge on how the flex-layout works is required. If you have any doubts regarding it, we strongly recommend you to access its own <a href="https://vtex.io/docs/recipes/layout/using-flex-layout">documentation</a>.`
</div>

### Introduction

Your store's Product Page can customized simply by changing the `store.product` block in your `store-theme` source code. 

The `store.product` is a block with children, that is, it is composed by other blocks. This means that the `store.product` block is flexible, so its children blocks can be declared using `flex-layout` to easily build a responsive page.

The `store.product` accepts as children all the blocks allowed by the `store` and `flex-layout` blocks, as well as the following blocks list:

```
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

<div class="alert alert-info">
You can always check out the full and updated list <a href="https://github.com/vtex-apps/store/blob/master/store/interfaces.json">here</a>.
</div>

## Practical example

Let's take a look at our demo store, [Storetheme](https://storetheme.vtex.com/). It has a good example of the usage of the `store.product` flexible block:

![](https://i.ibb.co/VDjQLyJ/image.png)

Follows below its definition:

```

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

As you can verify, the `store.product` children define 5 blocks, the first two being `flex-layout.row`. 

### Breadcrumb

The first row is declaring just the [breadcrumb](https://vtex.io/docs/components/all/vtex.breadcrumb/) and you can see it here:

![](https://i.ibb.co/ZhNry22/image.png)

```
"flex-layout.row#product-breadcrumb": {
    "props": {
      "marginTop": 4
    },
    "children": ["breadcrumb"]
  },
```

Notice above that it says via its `children` array to render the [breadcrumb](https://vtex.io/docs/components/all/vtex.breadcrumb/) block. If your desire is to customize the breadcrumb, such as change its props, you can then declare the breadcrumb block and define it just like you want to. For instance:
 
```
"breadcrumb": {
    "props": {
        "showOnMobile": true
    }
}
```

The second row is the one with the image and the right column with name, price, sku selector, button, etc. as shown below:

```
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

Notice that the second row defines two columns, the `flex-layout.col#product-image` and the `flex-layout.col#right-col`:

```
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

The left column is the one with the [product-images](https://vtex.io/docs/components/product/vtex.store-components/product-images) since it was the first one declared. 

![](https://i.ibb.co/ns8sP0Y/image.png).

As you can see rendered, the right column has many children:

![](https://i.ibb.co/Z6zxSc7/image.png)

### Product name

It starts with a [product-name](https://vtex.io/docs/components/product/vtex.store-components/product-name), used to display the product name, along with its SKU name if desired.

### Product price

Right below it, we can find the [product-price](https://vtex.io/docs/components/product/vtex.store-components/product-price) displaying a properly formatted selling price. You can set it to show the list price (if they diverge), installments, etc. Check out below an example of a Produc Price also displaying discount and list price:

![](https://i.ibb.co/BykKvJM/image.png)

Below the Product Price there is the `product-separator`, a block that just draws a line in your Product Page.

### Product quantity

Then, we have the [product-quantity](https://vtex.io/docs/components/product/vtex.product-quantity). With this block, you can let users choose how many items will be added to the cart.

![](https://i.ibb.co/8Y8gF0R/image.png)

### Product Identifier

Scrolling down, below the Product Quantity component, we arrive at the [product-identifier](https://vtex.io/docs/components/product/vtex.product-identifier). This component allows you to show the user the product identifier. 

You can then customize it with different props, choosing the label you want before the identifier, the display mode and more.

### SKU Selector

We then have a really important component: the [SKU Selector](https://vtex.io/docs/components/product/vtex.store-components/sku-selector). It allows the user to choose his desired SKU, automatically hiding impossible combinations or indicates combinations that are currently unavailable. 

### Buy button

The [buy-button](https://github.com/vtex-apps/store-components/tree/master/react/components/BuyButton) is the classic component that adds a SKU to the cart. You can customize it to show a successful message, to redirect the user to the Cart page immediately, etc.

### Shipping simulator 

Your store can also have a [shipping-simulator](https://vtex.io/docs/components/product/vtex.store-components/shipping-simulator). It allows the user to fill in its postal code and displays the available shipping options and its prices, given that product.

### Share 

Finally, there is [share](https://vtex.io/docs/components/general/vtex.store-components/share). The component allows product sharing in social media by the user. By customizing its props, you can control which options will be displayed to the user:

```
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

Notice that with this block we are hiding the Twitter option from our sharing list. The available social media for now are: `Facebook`,`Twitter`,`Telegram`,`WhatsApp`,`Google+`,`Pinterest` and `E-mail`.

After this right column is done, we our blocks start to render the blocks defined beneath them in our `store.product` block.

### Related products 

The Related Products Shelf (`shelf.relatedProducts`) is a [Shelf](https://vtex.io/docs/components/all/vtex.shelf/) component that displays products related to the one you are browsing. 

The related products displayed in a product page can be defined through your store's admin Catalog. As you can see above, the product we are using as example does not have any. But it should look exactly like this:

![](https://i.ibb.co/QpyMyXM/image.png)

The `shelf.relatedProducts` block lets you choose between different recommendation types. The recommendation property can be a value between: `['similars', 'view', 'buy', 'accessories', 'viewAndBought', 'suggestions']`.

Here is a brief example of a Related Products Shelf:

```
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

Have in mind that the `flex-layout` may suffer modifications if you are on mobile mode. You can check the [Flex Layout](https://vtex.io/docs/recipes/layout/using-flex-layout) recipe out for more information.

![](https://i.ibb.co/vcTGBpq/image.png)
