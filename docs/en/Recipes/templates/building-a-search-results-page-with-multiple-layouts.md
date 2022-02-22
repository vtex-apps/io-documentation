---
title: Building a search results page with multiple layouts
description: "Build your store's search results page using multiple layouts and provide a custom experience to your users."
date: "2021-01-13"
tags: ["multiple", "layout", "search-results"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/templates/building-a-search-results-page-with-multiple-layouts.md"
---

# Building a search results page with multiple layouts 

Your results presentation on the search results page doesn't need to be always the same for your users: thanks to enhancements in the Search Result app, you can provide them a more **customized experience** to navigate between the fetched products. 

![multiple-layouts](https://user-images.githubusercontent.com/52087100/104608825-1e979880-5661-11eb-9088-d337680bbb5a.png)
*Notice that the search results page above works with two different layouts: `grid` and `list`.*

The flexibility to offer multiple layouts, which can help the sales tax rates by enhancing the shopping experience, is at hands! Check out the step-by-step section below.

>⚠️ 
>
> To obtain successful results with this recipe, it is strongly recommended to understand previously how the [Flex Layout](https://developers.vtex.com/vtex-developer-docs/docs/vtex-flex-layout) and the [Search Result](https://developers.vtex.com/vtex-developer-docs/docs/vtex-search-result) apps work. We also advise you to go through the [Building a Horizontal Product Summary recipe](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-building-a-horizontal-product-summary) to achieve similar results on your search results page.

## Step by step

1. Implement the Search Result app in your Store Theme according to the instructions in the [documentation](https://developers.vtex.com/vtex-developer-docs/docs/vtex-search-result/). 
2. Declare the `gallery` block responsible for structuring the page layout, use its `layouts` prop to define the desired layouts for the search results page. For example:

```json
"gallery": {
  "props": {
    "layouts": [
      {
        "name": "grid",
        "component": "GridSummary",
        "itemsPerRow": {
          "(min-width:1008px)":4,
          "(min-width:623px) and (max-width:1007px)":3,
          "(max-width:622px)":2
        }
      },
      {
        "name": "list",
        "component": "ListSummary",
        "itemsPerRow": 1
      }
    ],
    "ListSummary": "product-summary.shelf#listLayout",
    "GridSummary": "product-summary.shelf"
  }
}
```

Notice that all of the `layouts`'s three properties are mandatory and must be provided for each layout.

| Property | Description |
| -------------- | ----------------------------------------------- |
|`name`|specifies the search result layout. It can be `grid` or `list`.|
|`component`|Defines the parent block responsible for defining the layout's components. For the `grid` layout, we define the component `GridSummary` that will then present items vertically and horizontally from each other. For the `list` layout, we define the `ListSummary` to show a list of items below one another.|
|`itemsPerRow`| controls how many items per row will be displayed by each layout. You can use media queries to define the layouts' widths properties for desktop, tablet, and phone, such as `min-width` and `max-width`, or you can use the layouts' name, such as `desktop`, `tablet` and `phone`.|


Choosing to use the layouts' name, such as `desktop`, `tablet` and `phone`, in `itemsPerRow`, you should declare them as the example below:

```json
{
  "component":"GridSummary",
  "itemsPerRow":{
    "desktop":4,
    "tablet":3,
    "phone":2
   }
}
```

Once you define the `list` and `grid` layouts, declare which blocks you should use in the code to build the desired pages:

| Component | Block |
| -------------- | ----------------------------------------------- |
| `ListSummary`  |  `product-summary.shelf#listLayout` block       |
|  `GridSummary` |  `product-summary.shelf` block                  |


3. Define the default layout i.e. which layout will be first presented to your users using the `defaultGalleryLayout` prop, from the `search-result-layout.mobile` and `search-result-layout.desktop` blocks:

```json
"search-result-layout.desktop": {
  "children": [
    "flex-layout.row#searchbread",
    "flex-layout.row#searchtitle",
    "flex-layout.row#result"
  ],
  "props": {
    "pagination": "show-more",
    "preventRouteChange": false,
    "defaultGalleryLayout": "grid"
  }
}
```

>ℹ️ Until now, you have a functioning search page with multiple layouts but with no flexibility to switch between them. For this purpose, we are going to declare next the `gallery-layout-switcher` block.

4. Declare the `gallery-layout-switcher` block in the search results template (`store.search`):

```jsonc
"gallery-layout-switcher": {
  "children": [
    /*
      * For accessibility purposes, it is fundamental to define the layout options following the same ordering used to declare them in step 2.
      */
    "gallery-layout-option#grid",
    "gallery-layout-option#list"
  ]
},
"gallery-layout-option#grid": {
  "props": {
    "name": "grid"
  },
  "children": [
    "icon-grid",
    "responsive-layout.desktop#textOptionGrid"
  ]
},
"gallery-layout-option#list": {
  "props": {
    "name": "list"
  },
  "children": [
    "icon-inline-grid",
    "responsive-layout.desktop#textOptionList"
  ]
},
"responsive-layout.desktop#textOptionGrid": {
  "children": [
    "rich-text#option-grid"
  ]
},
"responsive-layout.desktop#textOptionList": {
  "children": [
    "rich-text#option-list"
  ]
},
"rich-text#option-grid": {
  "props": {
    "text": "Grid",
    "textColor": "c-auto",
    "blockClass": "layout-option"
  }
},
"rich-text#option-list": {
  "props": {
    "text": "List",
    "textColor": "c-auto",
    "blockClass": "layout-option"
  }
}
```

>ℹ️ As seen above, each `gallery-layout-option` block receives the `name` prop with the name of the layout it corresponds to - this is a **mandatory** prop. In addition to this, you can also declare other blocks as its children and customize the selected layout option using the `galleryLayoutOptionButton--selected` [CSS Handle](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-using-css-handles-for-store-customization/).

5. Add the `gallery-layout-switcher` block as a child of the `search-result-layout.mobile` and `search-result-layout.desktop` blocks to display the switcher button on the page for both devices (mobile and desktop). For example:

```json
"flex-layout.row#searchinfo": {
  "children": ["flex-layout.col#productCount", "flex-layout.row#orderByAndSwitcher"]
},
"flex-layout.row#orderByAndSwitcher": {
  "children": ["order-by.v2", "gallery-layout-switcher"],
  "props": {
    "horizontalAlign": "right",
    "preventHorizontalStretch": true,
    "blockClass": "orderByAndSwitcher",
    "colGap": 3
  }
}
"flex-layout.col#switcherMobile": {
  "children": ["gallery-layout-switcher"],
  "props": {
    "verticalAlign": "middle"
  }
}
```

6. [Deploy your theme changes](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-making-your-theme-content-public).






