---
title: Lazy loading components
description: "Improve your website performance using these two Fold blocks."
date: "2020-04-29"
tags: ["performance", "fold", "experimentalLazyAssets", "blocks"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/new-docs-and-fix/docs/en/Recipes/templates/using-the-fold-blocks.md"
---

# Lazy loading components

In the VTEX IO Store Framework, there are the `__fold__` and the `__fold__.experimentalLazyAssets` blocks responsible for improving your website's performance. 

The `__fold__` block is responsible for defining which interface components will be loaded first for rendering and which will be loaded together with the user's scrolling. 

The `__fold__.experimentalLazyAssets`, an optional block, defines which components will be loaded statically until the first interaction with users. 

**They impact the initial loading performance** of the page on which they are configured, improving your storefront UX. 

## Before you start
- **Optimizing performance**

The blocks `__fold__` and `__fold__.experimentalLazyAssets` requires manual optimization of your store's page. However, there are features in the Admin that enable page performance. For further details, see the [Optimizing performance](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-best-practices-for-optimizing-performance#enabling-store-settings) guide.

- **Blocks configuration**

You do not need to declare and configure both blocks in your theme code. Adding the `__fold__` and the `__fold__.experimentalLazyAssets` in the template's block list is enough for improving your website's performance.

## Adding the `__fold__` block

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

> ⚠️ 
> 
> Google will not be able to track content positioned under the Fold block for SEO purposes, since the components are only loaded with user scrolling. Therefore, ensure you add all the SEO-relevant information above the fold block when applying this improvement.

## Optional: Adding the `__fold__.experimentalLazyAssets` block

> ⚠️
> 
>  The `__fold__.experimentalLazyAssets` block is experimental, which means it may cause side-effects, such as failing to render an interactive component in the storefront, such as the Carousel, and should be used with caution. If you are working in scenarios that you need to [lazy load images and products data in a slider](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-best-practices-for-optimizing-performance#lazy-loading-images-and-products-data-in-a-slider) we recommend [building a carousel using Slider Layout](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-building-a-carousel-using-slider-layout).

In the template's block list, add the `__fold__.experimentalLazyAssets` above the blocks whose loading will be static until the user's first interaction. We recommend that you add the `__fold__.experimentalLazyAssets` block to your store's home page (`store.home` theme template) for better results. For example:

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

> ⚠️
> 
> Make sure that it is added below blocks whose components are interactive, such as the Carousel. That's because the static loading, provided by the `__fold__.experimentalLazyAssets` block, can be detrimental to the proper functioning of these interactive components, negatively impacting user navigation.  
