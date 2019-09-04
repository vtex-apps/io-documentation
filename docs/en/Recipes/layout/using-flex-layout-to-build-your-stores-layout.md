---
title: Using flex-layout to build your store's layout
description: "With Store Framework you're able to use iframes to attend specific custom needs"
date: "2019-08-21"
tags: ["flex-layout", "layout"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/layout/flexLayout.md"
---

# Using flex-layout to build your store's layout

## What is flex-layout?

Flex-layout is a layout structuring paradigm built within VTEX IO store framework to allow the construction of complex custom layouts. This paradigm uses the concept of rows and columns to set the desired structure and positioning of components in a given page.

There two basic building blocks of every `flex-layout`, the `flex-layout.row` component and the `flex-layout.col` component. If you are already familiar with the [`flexbox`](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) layout used in CSS, `flex-layout` should be easy to get a grasp since that's being used by `flex-layout.row` and `flex-layout.col` under the hood.

## Using flex-layout

We are going to build the About Us page from our default [`store-theme`](https://storetheme.vtex.com/about-us) using `flex-layout` from scratch.

![Screen Shot 2019-08-21 at 5 47 45 PM](https://user-images.githubusercontent.com/27777263/63467414-d0667180-c43b-11e9-8cf3-473c1c94f10e.png)

This page can easily be thought of as a `row` with two columns, and in fact, that's exactly how we are going to model it. The image below is from the finished page with the `Flexbox Highlighter` from Firefox enabled, which shows how this layout is divided.

![Screen Shot 2019-08-21 at 4 05 19 PM](https://user-images.githubusercontent.com/27777263/63467270-736abb80-c43b-11e9-8a7b-dfe8f218f081.png)

To achieve this layout, we are going to use `flex-layout.row` and `flex-layout.col`, which are going to define each row and column in this layout.

First, let's declare the main block for the whole page:

```json
"store.custom#about-us": {
  "blocks": [
    "flex-layout.row#about-us"
  ]
},
```

As you can see, the `store.custom#about-us` consists of a single `flex-layout.row` block. A `flex-layout.row` is always the highest order block of the `flex-layout`, and you should never use the `flex-layout` block directly.

Okay, so now that we declared that we are going to use `flex-layout.row#about-us`, let's actually define it:

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

So here we declared `flex-layout.row#about-us` with two `children` blocks, one of them being an `image` and the other a `flex-layout.col` block. Notice that the `flex-layout.row` block does not accept only `flex-layout.col` blocks. Actually, both `flex-layout` blocks accept **any** block that is marked as `allowed` by their parent.

The `flex-layout.row` block is going to display its children with the same behavior as a `flexbox` container with the `flex-direction: row;` property, which means from left-to-right, one right after the other.

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

Now we are declaring `flex-layout.col#text-about-us` with two children, which are going to be displayed the same as if they were inside a `flexbox` container with the `flex-direction: column;` property, which means from top-to-bottom.

We are also passing down a specific prop to the `flex-layout.col`: `preventVerticalStretch`, which prevents the column from occupying 100% of its parent height.

We are not going to use all of the available props for customizing the row in this example, but they can be found at: [vtex.flex-layout](https://vtex.io/docs/components/general/vtex.flex-layout).

Okay! So that's pretty much what it takes to use `flex-layout` to build a simple layout. Here's the final `about-us.json`[https://github.com/vtex-apps/store-theme/blob/master/store/blocks/about-us.json] file:

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

This is a simple example, but you can also check out the blocks definition files for our default footer used by [`store-theme`](https://storetheme.vtex.com/) here: [Footer](https://github.com/vtex-apps/store-theme/blob/master/store/blocks/footer/footer.json).

## Rules and recommendations

- The highest level in a `flex-layout` is **always** made of rows.
- It is only possible to add a `flex-layout.col` inside of a `flex-layout.row` - never as a first-level block.
- When creating levels, it is necessary to alternate between rows and columns. Inside a row, you can only place columns, and inside of columns, you can only place rows.
- Each row and column can have as many levels as you need.
- It is important to note that the flex layout not only improves the layout building but also helps to make everything aligned. Gaps, margins, and paddings can be passed down to `flex-layout.row` and `flex-layout.col` as props.
- Be aware that the structure that you set in your flex layout does not affect only the organization of your code, but also reflects in the way that blocks will be shown and maintained in the StoreFront CMS.
  It is always important to take the organization of both the code and the StoreFront CMS into consideration when planning on how to apply the flex-layout into a page.
