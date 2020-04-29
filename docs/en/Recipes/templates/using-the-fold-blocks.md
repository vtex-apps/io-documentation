---
title: Using the Fold blocks
description: "Improve your website performance using these two Fold blocks."
date: "2020-04-29"
tags: ["performance", "fold", "experimentalLazyAssets", "blocks"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/new-docs-and-fix/docs/en/Recipes/templates/using-the-fold-blocks.md"
---

# Using the Fold blocks

In the VTEX IO Store Framework, there are two key blocks responsible for improving your website's performance. 

The first one is the `__fold__` block, responsible for defining which interface components will be loaded first for rendering and which will be loaded together with the user's scrolling. 

The second, called `__fold.experimentalLazyAssets`, defines which components will be loaded statically until the first interaction with users. 

Both are strategic, since **they directly impact the initial loading performance** of the page on which they are configured, improving your store's UX. 

The good news is that these two block can and should be used together to ensure maximum impact in terms of website performance. Check out the step by step below.

## Step by step

### Adding the `__fold__` block

Add the `__fold__` block to your theme's desired templates, such as `store.product` and `store.home`. For example:

```diff
"store.home": {
  "blocks": [
    "carousel#home",
+   "__fold__",
    "shelf#home",
    "info-card#home",
    "rich-text#question",
    "rich-text#link",
    "newsletter"
  ]
},
```

Once added, all blocks below it will get their components loaded **only** with user scrolling. Therefore, it's crucial for this block to be used only in scenarios in which your page is **scrollable**.

When using the `__fold__` block, you can also define different scenarios for mobile and desktop mode, adding `__fold__.mobile` and `__fold__.desktop` instead:

```diff
"store.home": {
  "blocks": [
    "carousel#home",
+   "__fold__.mobile",
    "shelf#home",
+   "__fold__.desktop",
    "info-card#home",
    "rich-text#question",
    "rich-text#link",
    "newsletter"
  ]  
},
```

This configuration by device is very useful, since components are viewed differently on desktop and mobile.

In the example above, both the Carousel and the Shelf will be displayed with the first meaningful paint on desktop mode. However, for mobile users, only the carousel will be loaded first.

<div class="alert alert-warning">
Google will not be able to track content positioned under the Fold block for SEO purposes, since the components are only loaded with user scrolling. Therefore, ensure you add all the SEO-relevant information above the fold block when applying this improvement.
</div>

### Adding the `__fold__.experimentalLazyAssets` block

<div class="alert alert-info">
We recommend that you add the <code>__fold__.experimentalLazyAssets</code> block to your store's home page (<code>store.home</code> theme template) for better results.
</div>

In the template's block list, add the `__fold__.experimentalLazyAssets` above the blocks whose loading will be static until the user's first interaction. For example:

```diff
"store.home": {
  "blocks": [
    "carousel",
+   "__fold__.experimentalLazyAssets", 
    "flex-layout.row#homeBrands",
    "flex-layout.row#homeBanner",
    "__fold__",
    "tab-layout#home",
    "tab-layout#home2",
    "carousel#homeFooter"
  ]
},
```

<div class="alert alert-warning">
Make sure that it is added below blocks whose components are interactive, such as the Carousel. That's because the static loading, provided by the <code>__fold__.experimentalLazyAssets</code> block, can be detrimental to the proper functioning of these interactive components, negatively impacting user navigation. 
</div>

<div class="alert alert-info">
You do not need to declare and configure both blocks in your theme code. Adding the <code>__fold__</code> and the <code>__fold__.experimentalLazyAssets</code> in the template's block list is enough for improving your website's performance. 
</div>
