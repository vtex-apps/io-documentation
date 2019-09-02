---
title: Building your Product Page
description: "Custom product pages are simple to build with our flexible components"
date: "2019-08-29"
tags: ["pdp", "product", "product page", "product details page"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/layout/productDetailsPage.md"
---

# Building your Product Page
​
### Disclaimer
​
In this tutorial, we will not cover much about `flex-layout`, we highly recommend you reading its own tutorial to understand everything taught here properly.
​
### Introduction
​
The Product Page is customized by changing the `store.product` block.
​
The `store.product` is a block that is composed with children, meaning it is a flexible block, so you can compose its children blocks using `flex-layout` to easily build a responsive page.
​
It accepts as children, all the blocks allowed in `store`, the `flex-layout` block and the following blocks:
​
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
​
If you want to have an uptaded list, you can always check the allowed list [here](https://github.com/vtex-apps/store/blob/master/store/interfaces.json).
​
### Real world example
​
Now, we are going to look at our demo store, [Storetheme](https://storetheme.vtex.com/).
![](https://i.ibb.co/VDjQLyJ/image.png)
​
It has a good example of the usage of the `store.product` flexible block, you can see it [here](https://github.com/vtex-apps/store-theme/blob/master/store/blocks/product.json).
​
Here is its definition:
​
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
​
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
​
```
​
As you can see, in its `store.product` children, it defines 5 blocks, the first two being `flex-layout.row`.
​
The first row is just the breadcrumb and you can see it here:
![](https://i.ibb.co/ZhNry22/image.png)
Its related block:
​
```
"flex-layout.row#product-breadcrumb": {
    "props": {
      "marginTop": 4
    },
    "children": ["breadcrumb"]
  },
```
​
As you can see, it says via its `children` array, to render the [breadcrumb](https://github.com/vtex-apps/breadcrumb) block.
​
If wanted to customize the breadcrumb, like change its props, you can then define the breadcrumb block and set it just like you want to:
​
```
"breadcrumb": {
    "props": {
        "showOnMobile": true
    }
}
```
​
The next row is the one with the image and the right column with name, price, sku selector, button, etc.
​
This row is defined:
​
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
​
It defines two columns:
​
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
​
The left col is the one with the [product-images](https://github.com/vtex-apps/store-components/tree/master/react/components/ProductImages)
![](https://i.ibb.co/ns8sP0Y/image.png).
​
Read its readme to get to know its blocks. You can customize the orientation of the thumbnails (vertical or horizontal), its position (left or right), if you want arrows on it if it overflows and what kind of zoom behaviour you would like.
​
The right column has many children:
![](https://i.ibb.co/Z6zxSc7/image.png)
​
It starts with a [product-name](https://github.com/vtex-apps/store-components/tree/master/react/components/ProductName), used to display the product name, along with its SKU name if you want.
​
Right below it, we have the [product-price](https://github.com/vtex-apps/store-components/tree/master/react/components/ProductPrice). It displays a properly formatted selling price, you can set to show the list price (if different), to show installments, etc.
​
![](https://i.ibb.co/BykKvJM/image.png)
Another example of product-price, this time displaying discount and list price.
​
Right below the price, we see the `product-separator`, a block that just draws a line.
​
Then we have the [product-quantity](https://github.com/vtex-apps/product-quantity).
With this block, you can let users choose how much items will be added to the cart when the add to cart button is clicked.
​
![](https://i.ibb.co/8Y8gF0R/image.png)
​
Continuing from this screen, below the quantity component, we arrive at the [product-identifier.product](https://github.com/vtex-apps/product-identifier).
This component allows you to show to the user the product identifier, you can then customize it with different props and choose the label you want before the identifier, different display modes and more.
​
We then have a really important component, the [SKU Selector](https://github.com/vtex-apps/store-components/tree/master/react/components/SKUSelector). It allows the user to choose what SKU it wants, automatically hiding impossible combinations or indicates combinations that are currently unavailable. Please take your time reading its readme.
​
The [buy-button](https://github.com/vtex-apps/store-components/tree/master/react/components/BuyButton) is the classic component that adds the SKU to the cart. Take a look at its readme, you can customize if you want to show or not the toast with successful message, if you want to redirect user to cart page immediately, etc.
​
You can then have a [shipping-simulator](https://github.com/vtex-apps/store-components/tree/master/react/components/ShippingSimulator). It allows the user to input its postal code and displays the available shipping options and its prices, given that product.
​
We finally have the [share](https://github.com/vtex-apps/store-components/tree/master/react/components/Share). The component lets user share the product in its social media. With its props, you can control what options the user can see.
​
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
​
With this block, we are hiding the Twitter option from our sharing list.
The available social media for now are: `Facebook`,`Twitter`,`Telegram`,`WhatsApp`,`Google+`,`Pinterest` and `E-mail`.
​
After this right column is done, we our blocks start to render the blocks defined beneath them in our `store.product` block.
​
In this case it is a `shelf.relatedProducts` block. It is a [shelf](https://github.com/vtex-apps/shelf). More specifically, a shelf that displays related products.
​
![](https://i.ibb.co/QpyMyXM/image.png)
​
The related products displayed for that product in page can be set in catalog. The `shelf.relatedProducts` block lets you choose different types of recommendation.
​
The recommendation property can be a value between: `['similars', 'view', 'buy', 'accessories', 'viewAndBought', 'suggestions']`.
​
Each value matches on Catalog API being called for that shelf.
Please check its readme for more details.
​
Here is a brief example of a Related products shelf:
​
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
​
### Mobile
​
Its important to note that the `flex-layout` makes some modifications depending if you are on mobile. Check the `flex-layout` tutorial for more information.
​
![](https://i.ibb.co/vcTGBpq/image.png)
