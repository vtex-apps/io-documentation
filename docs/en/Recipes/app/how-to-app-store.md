---
title: How to setup the product page of your app in the App Store
description: "Your app can have a nice product page in our App Store."
date: "2019-08-1"
tags: ["vtex-io", "app-store"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/app/how-to-app-store.md"
---

# How to setup the product page of your app in the App Store

Your app can have a nice product page in our App Store. You can add icon, a description and some screenshots. [See an example of a app page](https://apps.vtex.com/google-shopping/p).

1. Create a folder called `public`
2. Create another folder called `metadata` inside the `public` folder
3. Add your icon to the `metadata` as `icon.png`

You can translate the description and screenshots of your app. You must have at least the English version.

1. Create a folder called `en-US` inside `metadata`
2. Add a file called `full_description.txt`. This file will be interpreted as a Markdown and will be displayed in the product page.
3. Create a folder called `screenshots` inside `en-US`.
4. Add the screenshots as PNG files, you should prefix them with `mobile-` or `desktop-`. Add a number after, the screenshots will be displayed in order. Example: `desktop-01.png`.

Full app structure example:

```bash
public/
└── metadata
    ├── icon.png
    ├── en-US
    │   ├── full_description.txt
    │   └── screenshots
    │       ├── mobile-01.png
    │       ├── desktop-01.png
    │       ├── desktop-02.png
    │       └── desktop-03.png
    ├── es-AR
    │   ├── full_description.txt
    │   └── screenshots
    │       ├── desktop-01.png
    │       ├── desktop-02.png
    │       └── desktop-03.png
    └── pt-BR
        ├── full_description.txt
        └── screenshots
            ├── desktop-01.png
            ├── desktop-02.png
            └── desktop-03.png
```
