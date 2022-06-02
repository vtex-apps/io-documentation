---
title: Best practices for rendering images
description: "Learn now all best practices for rendering images in your store's theme and improve the way in which images are cropped, rendered and displayed to end users"
date: "2020-04-29"
tags: ["best-practices", "guidelines", "images", "rendering", "display"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/new-docs-and-fix/docs/en/Recipes/templates/best-practices-for-rendering-images.md"
---

# Rendering images

While building your brand's visual identity, you'll often use images in your store theme. Images, however, can significantly impact a website's performance. In this sense, Store Framework provides different image blocks for different use cases. Each block defines how images will be cropped, rendered, and displayed to end-users. Hence, to implement the right solution for your use case, please consider the practices presented in the following.

---

## Uploading images to your theme's code
  
- Upload images to your theme's code using the [**Assets Builder**](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-using-the-assets-builder) or the [Site Editor](https://help.vtex.com/en/tutorial/site-editor-overview). The Assets Builder and the Site Editor ensure that the images are properly cropped, providing end-users a consistent and uniform experience.
- Don't declare the URLs of the desired images directly in the `blocks.json` file. Otherwise, the images may end up deformed.
- Don't use images with large dimensions. Otherwise, the Site Editor may not be able to crop them. 

## Choosing the right image block

Store Framework has different solutions for rendering images, each one of them designed for a specific use case. 

In the following, we outlined the main functionalities of each image block so you can identify which solution is the best fit for what you're trying to achieve and avoid performance drops in your store website.

- [**Logo**](https://developers.vtex.com/vtex-developer-docs/docs/vtex-store-components/logo) - Renders your brand's logo. It should preferably be used in your store's Header and Footer. 
- [**Infocard**](https://developers.vtex.com/vtex-developer-docs/docs/vtex-store-components/infocard) - Renders images in the UI with links and call-to-action buttons that guide the user's flow. Info cards are recommended when you want to render an image directly linked to a call-to-action button.
- [**Rich Text**](https://developers.vtex.com/vtex-developer-docs/docs/vtex-rich-text) - Renders markdown texts. Rich texts allow plenty of customization, such as passing an image URL to be rendered. Rich texts are recommended for building text communications that may need to have an image linked to them.
- [**Product Summary Image**](https://developers.vtex.com/vtex-developer-docs/docs/vtex-product-summary-productsummaryimage) - Renders the product image attached to a product summary information (e.g., name, price). Product summary images must be displayed within other store components, such as the Shelf.
- [**Image**](https://developers.vtex.com/vtex-developer-docs/docs/vtex-store-components-image) - Renders an image without links, buttons, markdown texts, or product summary information attached. It is exclusively responsible for rendering an image of your choosing in your store's theme.

### Product Summary Image block

When using the Product Summary component, define at least one of the following props: `aspectRatio`, `width`, `height`, `maxHeight`. These props define image dimensions and enable you to let Product Summary images be of identical size when rendered, even if the images submitted in the admin's Catalog have a different size.

These props define the image's dimensions and allow product summary images to be presented with the same size, regardless of the dimensions of the images uploaded via the admin's Catalog.

>ℹ️ You don't have to specify these four properties in your Product Summary Image block at the same time. Each one has a distinct purpose and can be used independently. For more information on implementing these props, please refer to the [**Product Summary Image**](https://developers.vtex.com/vtex-developer-docs/docs/vtex-product-summary-productsummaryimage) documentation.

For example, by declaring these props, your store's Shelf will have image consistency across all products being displayed, differently from the Shelf example below:

![beat-practices-images](https://user-images.githubusercontent.com/52087100/80645249-3bdbf680-8a41-11ea-8f63-8b96b20f7c4b.png)


