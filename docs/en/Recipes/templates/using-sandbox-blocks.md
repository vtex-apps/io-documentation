---
title: Using Sandbox blocks
description: "Understand what the Sandbox app is and use iframes to attend to your store's custom needs"
date: "2019-08-19"
tags: ["iframe", "sandbox-app", "sandbox-block", "custom"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/templates/using-sandbox-blocks.md"
---

# Using Sandbox blocks

## Introduction

VTEX Store Framework is a very powerful tool meant to attend most client needs. It's understandable, though, that some custom requirements that your store needs and will not be served by the framework. That's where the **Sandbox App** comes in.

The **Sandbox App** is basically a component that supports iFrames. Therefore, it allows you to use custom `html`, `css` and `js` code to customize your store.

## Step by step

1. Go ahead and open your `manifest.json` file and declare the Sandbox app as a dependency. 

![sandbox dependency](https://user-images.githubusercontent.com/19555647/64436951-b95e8b00-d09b-11e9-90af-7d11f6d9d501.png)

2. Then, declare the Sandbox block in the `blocks` folder or in the `blocks.jsonc` file.

```json
"sandbox#h1": {
  "props": {
    "width": "100%",
    "height": "auto",
    "initialContent": "<h1 style=\"text-align:center;\">Hello World</h1>",
    "allowCookies": false
  }
}
```

Let's suppose you want to create a simple `h1` sandbox block. It would look similar to the following:

![sanbox hello world](https://user-images.githubusercontent.com/19555647/64436924-ae0b5f80-d09b-11e9-9080-fd4c983689d1.png)

3. Reference it in another's block `child dependency` or `blocks`. For instance, your `store.home`: 

```json
//home.jsonc
"store.home": {
  "blocks": [
    "carousel#home",
    "sandbox#h1",
    "flex-layout.row#deals",
    "shelf#home",
    "info-card#home",
    "rich-text#question",
    "rich-text#link",
    "newsletter"
  ]
},
```

That should render the h1 sandbox on the store's page!

## Best Practices

If you think that a component is very similar to what will serve your store needs but that it still needs some tweaks, you should find the right style and props to turn into the custom component you are looking for. 

**Sandbox should only be used whenever Store Framework native components won't handle your scenario** and when what you intend to do is simple enough that it doesn't require a lot of outsource data. Creating everything using iFrames will make your store easily obsolete to new Store Framework features and not very good in terms of performance.
