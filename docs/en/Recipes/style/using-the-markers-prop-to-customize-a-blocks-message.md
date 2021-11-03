---
title: Using the Markers prop to customize a block's message
description: "Use the Markers prop and customize messages exported by blocks."
date: "2020-04-09"
tags: ["message", "markers", "prop", "customize"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/new-docs-1/docs/en/Recipes/style/using-the-markers-prop-to-customize-a-blocks-message.md"
---

# Using the Markers prop to customize a block's message
  
CSS Handles and Block Classes are identifiers used to give storefront components a unique identity through CSS classes.

While capable of solving most scenarios, both identifiers have limitations in terms of more specific customization.

For example: you can customize all blocks exported by an app in the same way using CSS Handles or you can customize each one of them in a unique way using Block Classes. However, none of the two identifiers is capable of customizing the **messages** these blocks export. 

To resolve this scenario, we use the `markers` prop. Following the same logic as the Block Class prop, the `markers` prop is tasked with **defining unique values that will ultimately act as identifiers for the text messages** that are exported by the block in which it was declared. 

Find out how to configure the `markers` prop in the step-by-step below. 

## Step by step

>ℹ️ Before going through the steps, make sure that the block in which you are working accepts the `markers` prop. You can check this in its <a href="https://developers.vtex.com/vtex-developer-docs/docs/overview-5/">documentation</a>.

1. Using your terminal and [VTEX IO CLI](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installation-and-command-reference/), log in to the desired VTEX in a [Development workspace](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-creating-a-development-workspace/).
2. Access the directory where your store's theme is stored and open it using your code editor.
3. Once the theme's code is open, add the `markers` prop to the desired block and give it a unique value. For example:

```json
"product-price-savings#summary": {
  "props": {
    "markers": [
      "discount"
    ],
  }
},
```

4. Save your changes and [link](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-linking-an-app/) the app.
5. Using the Developer workspace you were previously working in, access the admin of the VTEX account in which your are working (`{workspaceName}--{accountName}.myvtex.com/admin`).
6. Then, open the admin's Site Editor in the CMS module.
7. Select the block in which the `markers` prop was added during step 3;
8. Once the editing screen is open, use the prop's value as a tag, wrapping the block's desired message variable that will ultimately be customized. For example: `<discount>-{savingsPercentage}</discount>`

![markers-prop-site-editor](https://user-images.githubusercontent.com/52087100/78163670-0f6f9300-741f-11ea-83a4-7122113234fb.gif)

>ℹ️ You can use the prop's value to wrap any desired part of the block's message.

>ℹ️ Notice: the block's message variables can be found in the block/app documentation.

9. Save the changes. This will give the wrapped text a unique identifier, allowing for CSS customization of the HTML message related element.
10. Using the Development workspace, access the site of the account that you are working on (`{workspaceName}--{accountName}.myvtex.com`). Thereafter, inspect the HTML element that corresponds to the edited block's message.

![product-price-markers-inspect](https://user-images.githubusercontent.com/52087100/78162509-578db600-741d-11ea-9d7d-e4c74399576e.png)
*Notice that the message's HTML element is wrapped in a new `span` with its own unique selector: `<span class="vtex-product-price-1-x-savings-discount">`.*

If you are happy with the changes to your store theme, make your new theme content public. Up until this point, only you could see the changes performed using the `markers` prop in your Development workspace. Access our documentation on [Making your theme content publicly available](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-making-your-theme-content-public/) and follow the steps detailed there.

Once your changes are publicly available, meaning they are reflected in your store's Master workspace, you will be able to use the new identifier created for the HTML element and customize it at will. Access the recipe on [customizing your store using CSS Handles](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-using-css-handles-for-store-customization/) for more on this customization topic.
