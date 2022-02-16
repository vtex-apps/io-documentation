---
title: Customizing your store's icons
description: "VTEX Styleguide has a default iconography that is used in all VTEX's components. Learn with this recipe how to change it and customize according to your store's identity. "
date: "04/09/2019"
tags: ["icon", "custom", "icons", "iconography", "change", "edit"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/edit/master/docs/en/Recipes/style/customizing-your-stores-icons.md"
---

# Customizing your store's icons

## Introduction

[VTEX Styleguide](https://styleguide.vtex.com) has a [default iconography](https://styleguide.vtex.com/#/Icons) that is used in all VTEX IO store's components. Their implementation is imported via the [Store Icons](https://github.com/vtex-apps/store-icons) app. 

Although these can satisfy your store’s needs, you may want to override and customize default icons according to your store's identity. If so, simply follow the steps below. 

## Step by step

1. In your `store-theme` code, create a new folder named `iconpacks/` within `styles/`. 
2. Inside `iconpacks/`, create the file `iconpack.svg`. 
3. Copy the content from VTEX'S default [iconpack.svg](https://github.com/vtex-apps/store-icons/blob/master/styles/iconpacks/iconpack.svg?short_path=62ebf4b) and paste it in the `iconpack.svg` file. 

>⚠️ The maximum size allowed for icons is `20x20`.

>⚠️  A [workspace](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-workspace) can **only** have a single app installed that contains the `iconpack` customization. 

This is how your `styles/` folder structure should look like after you've accomplished that: 

![iconpack-folder](https://user-images.githubusercontent.com/52087100/64298990-d2592600-cf4d-11e9-994c-eaefd317f9ef.png)

The `iconpack.svg` file will implement [SVG frament identifiers](https://css-tricks.com/svg-fragment-identifiers-work/), allowing you to simply change the part of the code that declares the icon's `g` tag instead of customize itself. 

For instance, let's customize the cart icon (`hpa-cart`) changing only its `g` content: 

![image](https://user-images.githubusercontent.com/18701182/61139096-0dcffa80-a49f-11e9-8ff9-4c4f805a2738.png) 

After [linking](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-linking-an-app) your app, you should see the changes in the browser:

![image](https://user-images.githubusercontent.com/18701182/61139698-360c2900-a4a0-11e9-910b-8391ca58565e.png) 

Check out each icon's ID by accessing the [Icon Pack list](https://github.com/vtex-apps/store-icons/blob/cbbb1b82bfca247a811d146b1e2cafb642db1928/docs/ICONPACK.md). 

>⚠️ If you've linked your code and haven't seen your changes, it may be because your `Styles builder` is not up-to-date with this functionality. Make sure your store has it installed at version <bold>1.8.1</bold> or higher. 
