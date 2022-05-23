---
title: Using partytown on you pixel apps to improve store performance
description: "Improve store performance by running your pixels on web workers using partytown."
date: "2022-05-23"
tags: ["third-party", "performance", "partytown"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/templates/using-partytown-to-improve-store-performance.md"
---

# Using partytown on you pixel apps to improve store performance

Third-party scripts (aka pixels) are a primary cause of performance slowdowns. One of the main reasons is that those scripts congest the main thread, slowing down the speed at which the page content is loaded.

[Partytown](https://partytown.builder.io/) is a library that relocate third-party scripts into a web worker leaving the main thread free for rendering your page.

> ℹ️ **Partytown is currently in Beta**. Which means it's still not a final version and may have flaws. We recommend always testing all scripts while implementing this guide.

## Installing partytown

1. Install the `vtex.partytown@0.x` on your new workspace.

2. Some of our pixel apps already have support for partytown. If you use one of them, make sure to update them to the last major.

- `vtex.google-tag-manager@4.x`
- `vtex.hotjar@1.x`
- `vtex.facebook-pixel@3.x`


> ℹ️ Installing new majors of these apps resets their settings. So it will be necessary to reconfigure them.

## Migrating your pixel app to the partytown format

1. Open the `pixel/head.html` file

2. Add the `type="text/partytown"` attribute to each individual `<script>` to run from a web worker.
```diff
- <script>...</script>
+ <script type="text/partytown">...</script>
```

3. (Optional) If you want to access some global variables added to the `window` by the pixel apps, you need to declare it. Go to the `https://{{myworkspace}}--{{myaccount}}.myvtex.com/admin/apps` URL, select the `partytown` app and then add the name of the variables you want to access in the `Forward` field.

![image](https://user-images.githubusercontent.com/40380674/169821502-4148db94-4a1a-493f-95ee-aaf5e243ebec.png)
