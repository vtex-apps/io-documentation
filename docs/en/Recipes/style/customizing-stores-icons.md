---
title: Customize store's icons
description: "VTEX Styleguide has a default iconography that is used in all VTEX's components. Their implementation is imported via the [Store Icons](https://github.com/vtex-apps/store-icons) app."
date: "19/08/2019"
tags: ["icon", "custom", "icons", "iconography"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/style/customizeIcons.md"
---

# Customizing store's icons

[VTEX Styleguide](https://styleguide.vtex.com) has a [default iconography](https://styleguide.vtex.com/#/Icons) that is used in all VTEX's components. Their implementation is imported via the [Store Icons](https://github.com/vtex-apps/store-icons) app. 

Since iconography is an important part of a brand identity, the Store Icons' app allows icon overriding. 
To get started with **icon customization**, the first thing you need to do is to create a new folder your `store-theme`. That folder must be named `iconpacks/` and it should be inside the `styles/` folder. 
Inside the `iconpacks/` folder, you should create a new file called `iconpack.svg` and copy the content from VTEX's [default iconpack.svg](https://raw.githubusercontent.com/vtex-apps/store-icons/master/styles/iconpacks/iconpack.svg). This is how your projects' directory structure should look like after you've accomplished that: 

![image](https://user-images.githubusercontent.com/18701182/61138550-1bd14b80-a49e-11e9-9c9f-8fad3c59ebbb.png) 

The `iconpack.svg` file implements [SVG frament identifiers](https://css-tricks.com/svg-fragment-identifiers-work/), so in order for you to customize an icon, you should just change the part of the code that declares the g tag of that iconn. For instance, to change the cart icon ( that uses the name hpa-cart), you should change its `g` content: 

![image](https://user-images.githubusercontent.com/18701182/61139096-0dcffa80-a49f-11e9-8ff9-4c4f805a2738.png) 

Link your code and you should now see your change 

![image](https://user-images.githubusercontent.com/18701182/61139698-360c2900-a4a0-11e9-910b-8391ca58565e.png) 

You can see whole iconpack and each icon's id in: [ICONPACK](https://github.com/vtex-apps/store-icons/blob/master/ICONPACK.md) 

**TROUBLESHOOT:** If you've linked your code and you haven't seen your changes it may be because your `styles builder` is not up-to-date with this functionality, please install, in your store, the version 1.8.1 or higher: 
```
vtex install vtex.styles-graphql@1.8.1
``` 
