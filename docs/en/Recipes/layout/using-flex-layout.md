---
title: Using flex-layout
description: "Improve your store's layout building by positioning its component as desired with flex-layout."
date: "2019-08-21"
tags: ["flex-layout", "layout", "using"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/layout/using-flex-layout.md"
---

# Using flex-layout

## Introduction

Flex-layout is a layout structuring paradigm built within VTEX IO Store Framework that allows the construction of complex custom layouts. This paradigm uses the concept of rows and columns to set the desired positioning of components in a given page.

There two basic building blocks of every `flex-layout`: the `flex-layout.row` and the `flex-layout.col`. If you are already familiar with the [`flexbox`](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) layout used in CSS, `flex-layout` should be easy to get a grasp since that's what `flex-layout.row` and `flex-layout.col` use under the hood.

The flex layout not only improves the layout building but also helps to make everything aligned since gaps, margins and paddings can be passed down to `flex-layout.row` and `flex-layout.col` as props.

## Practical example

Let's build an About Us page as the one below using `flex-layout` from scratch. 

![Screen Shot 2019-08-21 at 5 47 45 PM](https://user-images.githubusercontent.com/27777263/63467414-d0667180-c43b-11e9-8cf3-473c1c94f10e.png)

If we think on how we could divide this page layout, we will realize that it could be easily thought as one row with two columns model: 

![Screen Shot 2019-08-21 at 4 05 19 PM](https://user-images.githubusercontent.com/27777263/63467270-736abb80-c43b-11e9-8a7b-dfe8f218f081.png)

To achieve the layout shown above, we are going to use the `flex-layout.row` and `flex-layout.col` components, which are going to define each row and column for this page's layout.

First, let's declare (in the `blocks` folder or `blocks.jsonc` file) the main block for the whole About Us page:

```
json
"store.custom#about-us": {
  "blocks": [
    "flex-layout.row#about-us"
  ]
},
```

As you can see, the `store.custom#about-us` block consists of a single `flex-layout.row` block because it is always the highest order block of the `flex-layout`. You should never use the `flex-layout` block directly.

Now that we declared that we are going to use `flex-layout.row#about-us`, let's actually define it:

```json
"store.custom#about-us": {
  "blocks": [
    "flex-layout.row#about-us"
  ]
},

"flex-layout.row#about-us": {
  "children": [
    "image#mobile-phone",
    "flex-layout.col#text-about-us"
  ]
},
```
<div class="alert alert-info">
The <code>flex-layout.row</code> block is going to display na interface its children from left-to-right, one right after the other.
</div>

As shown above, the `flex-layout.row#about-us` was declared with two `children` blocks, one of them being an `image` and the other a `flex-layout.col` block. The `flex-layout.row` block does not accept first-level blocks in it, but notice that the it does not accept only `flex-layout.col` blocks. Actually, both `flex-layout` blocks only accept blocks classified as `allowed` by their parent.

Let's define our `flex-layout.col#text-about-us` block:

```json
"store.custom#about-us": {
  "blocks": [
    "flex-layout.row#about-us"
  ]
},

"flex-layout.row#about-us": {
  "children": [
    "image#mobile-phone",
    "flex-layout.col#text-about-us"
  ]
},

"flex-layout.col#text-about-us": {
  "children": [
    "rich-text#title-about-us",
    "rich-text#about-us"
  ],
  "props": {
    "blockClass": "textColumn",
    "preventVerticalStretch": true
  }
},
```

<div class="alert alert-info">
The <code>flex-layout.col#text-about-us</code> block is going to display na interface its children from top-to-bottom, one right after the other.
</div>

The `preventVerticalStretch` prop prevents the column from occupying 100% of its parent height when set as `true`. Other props for a custom row can be used by you and found at the [Flex Layout](https://vtex.io/docs/components/all/vtex.flex-layout/) documentation.

Here's the final `about-us.json`[https://github.com/vtex-apps/store-theme/blob/master/store/blocks/about-us.json] file using the flex-layout: 

```json
{
  "store.custom#about-us": {
    "blocks": ["flex-layout.row#about-us"]
  },

  "flex-layout.row#about-us": {
    "children": ["image#mobile-phone", "flex-layout.col#text-about-us"]
  },

  "flex-layout.col#text-about-us": {
    "children": ["rich-text#title-about-us", "rich-text#about-us"],
    "props": {
      "blockclass": "textColumn",
      "preventVerticalStretch": true
    }
  },

  "rich-text#title-about-us": {
    "props": {
      "text": "# Create meaningful and relevant experiences.",
      "blockClass": "title"
    }
  },

  "image#mobile-phone": {
    "props": {
      "src": "https://storecomponents.vteximg.com.br/arquivos/mobile-phone.png",
      "maxHeight": "",
      "maxWidth": "",
      "blockClass": "storePrint"
    }
  },

  "rich-text#about-us": {
    "props": {
      "text": "**Optimized store framework** \n Free your front-end with our React + Node store framework. Improve usability and SEO, while driving more conversion with modular components, single-page applications, and a ready-for-PWA structure. \n **Multi-currency and language** \n Go international with multiple storefronts to support different languages and easily manage local currencies and payment conditions. \n **Serverless development platform** \n Reduce loading time, improve usability, and make the best out of SEO. Developing scalable components with a comprehensive, easy-to-use toolset, you can build stores faster than ever.",
      "blockClass": "about"
    }
  }
}
```

## Rules and recommendations

- Each row and column can have as **many levels as you need**.
- When creating levels, it is necessary to **alternate between rows and columns**. Inside a row, you can only place columns, and inside of columns, you can only place rows.
- Be aware that the structure that you set in your flex layout does not only affect your code organization, but also reflects in the way that blocks will be shown and managed through the admin's Storefront. Therefore, it is always important to **take the organization of both the code and the StoreFront into account when planning to apply the flex-layout** into a page.
