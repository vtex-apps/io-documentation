---
title: Customizing your store’s typography
description: "A store’s choice in terms of typography is a fundamental step to building its identity. Within this environment, learn how to customize typography styles using the admin’s interface and your theme’s code."
date: "08/07/2019"
tags: ["customizing", "customize", "customization", "typography", "print", "cms", "styles", "css"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/style/customizing-your-stores-typography.md"
---

# Customizing your store’s typography

## Introduction

In addition to being crucial for communicating with users, a store’s typography should be a reflection of its identity, using its characteristic styles, such as font size and spacing.

Whether using the admin’s CMS or your store theme CSS files, Store Framework gives you the flexibility to customize your store’s typography according to your business needs. 

## Step by step

### Using store theme CSS files 

1. Open your store theme directory using a code editor of your preference. 
2. Create a new folder inside the `assets` directory called `fonts`. Make sure your app have the [assets builder in its manifest](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-using-the-assets-builder/).
3. Add the font files inside this folder (`assets/fonts/`).

>⚠️ The font files must be in the following file extensions: `.ttf` or `.woff`. 

4. In `styles/configs` folder, create a new file called `font-faces.css`.
5. Use the `@font-face` rule declaring the CSS properties you desire to apply in your website typography. For example:

```css
@font-face {
  font-family: 'MyHelvetica';
  src: url(assets/fonts/MyHelvetica.woff2), url(assets/fonts/MyHelvetica.ttf);
  font-weight: bold;
}
```

>ℹ️ Notice that fonts uploaded on Assets builder can be referenced in your CSS files by declaring the desired file path in the `src` property. 


>⚠️The `font-faces.css` is a global file meaning its configurations are applied to all texts from the website. If you want to customize a component's typography independently, overriding the global configurations,you should declare the `font-faces.css` file still and refer the desired component font using the `font-family` property in the app's CSS overriding file. 

### Using store's admin

1. Access **Styles** in the desired account’s admin, in **CMS**.
2. Select the More Options (three dots) menu for the store’s style whose typography will be edited.
![customize-typo-image2 EN](https://user-images.githubusercontent.com/52087100/63810485-3602a400-c8fb-11e9-8077-41ab76c66ad2.png)
3. Click on **Edit** and select **Typography**.
![customize-typo-image3 EN](https://user-images.githubusercontent.com/52087100/63810513-431f9300-c8fb-11e9-9f37-9789fbd52776.png)

In the **Font Family** section, you can add a font family of your choosing in order to use in your store’s theme. Simply click on **Add custom font** and upload the desired font’s file. 

Remember to give a name for the font family recently uploaded by you, otherwise you won't be able to properly save your changes. 

>⚠️ The font family file must be uploaded in the following file extensions: `.ttf` or `.woff`. 

After choosing the font family, you can apply it to your store’s text content. The **Type Token** option displays all your store’s text content that can be customized. In addition to each one’s font families, you can also customize other parameters, such as **Font Weight**, **Font Size**, capitalization (**Text Transform**) and spacing (**Letter Spacing**).

For a better understanding of this feature and customization recommendations for each of your store’s text content, access the [VTEX Styleguide](https://styleguide.vtex.com/#/Styles?id=section-typography).

>⚠️ After performing all desired customizations, don’t forget to save your changes! 
