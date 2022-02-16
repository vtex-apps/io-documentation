---
title: Customizing your store’s typography
description: "A store’s choice in terms of typography is a fundamental step to building its identity. Within this environment, learn how to customize typography styles using the admin’s interface and your theme’s code."
date: "08/07/2019"
tags: ["customizing", "customize", "customization", "typography", "print", "cms", "styles", "css"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/style/customizing-your-stores-typography.md"
---

# Customizing your store’s typography

In addition to being crucial for communicating with users, a store’s typography should be a reflection of its identity, using its characteristic styles, such as font size and spacing.

Whether using the admin’s CMS or your store theme CSS files, Store Framework gives you the flexibility to customize your store’s typography according to your business needs. 

> ⚠️
> If you want to perform your store's typography customization in **the Admin's CMS**, refer to [Customizing your store’s typography documentation in the Help Center](https://help.vtex.com/tutorial/personalizando-a-tipografia-da-sua-loja--2R0ByIjvJtuz99RK3OL5WP).

## Before you start

Bear in mind that for the customization to work, the **Styles builder of your store must be 2. x.** To successfully migrate to Styles Builder 2.x, you must update the version of the `styles` builder in the `manifest.json` file of your store theme app, as the example below:

```json
builders{
...
"styles": "2.x"
}
```

In the following, check the [best practices of CSS handles](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-using-css-handles-for-store-customization#best-practices) to review and update every CSS customization for your store elements.


## Step by step

### Using store theme CSS files 

1. Open your store theme directory using a code editor of your preference. 
2. Create a new folder inside the `assets` directory called `fonts`. Make sure your app have the [assets builder in its manifest](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-using-the-assets-builder/).
3. Add the font files inside this folder (`assets/fonts/`).

>⚠️ Warning
>
> The font files must be in the following file extensions: `.ttf` or `.woff`. 

4. In `styles/configs` folder, create a new file called `font-faces.css`.
5. Use the `@font-face` rule declaring the CSS properties you desire to apply in your website typography. For example:

```css
@font-face {
  font-family: 'MyHelvetica';
  src: url(assets/fonts/MyHelvetica.woff2), url(assets/fonts/MyHelvetica.ttf);
  font-weight: bold;
}
```

>ℹ️ Info
>
> Notice that fonts uploaded on Assets builder can be referenced in your CSS files by declaring the desired file path in the `src` property. 


>⚠️ Warning
>
> The `font-faces.css` is a global file meaning its configurations are applied to all texts from the website. If you want to customize a component's typography independently, overriding the global configurations,you should declare the `font-faces.css` file still and refer the desired component font using the `font-family` property in the app's CSS overriding file. 
