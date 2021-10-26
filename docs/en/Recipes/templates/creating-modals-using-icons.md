---
title: Creating modals using icons
description: "Trigger modals using UI components in order to force user interaction before a certain action is taken during browsing."
date: "2020-06-18"
tags: ["modals", "icon", "store-icons", "creating"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/templates/creating-modals-using-icons.md"
---

# Creating modals using icons 

When talking about ecommerce, a modal is a **popup window**, triggered by an UI component, that forces users to interact with it before a certain action is taken during browsing.

Let's look at the following scenario: ready to proceed to checkout, a user browsing your store has a full cart. The user then removes an item from the product list without noticing, by accidentally clicking on the trash icon.

To your business, it's advantageous to trigger a popup window in this removal icon, requiring user confirmation to complete the action. In a lot of cases, the modal will contribute to an increase in conversion rate.

To build modals in such a scenario using Store Framework, we'll use the [Modal Layout](https://developers.vtex.com/vtex-developer-docs/docs/vtex-modal-layout) block and the icons exported by the [Store Icons](https://developers.vtex.com/vtex-developer-docs/docs/vtex-store-icons) app. 

## Step by step

For this step, we'll take the example given above: let's add a modal to the icon used by the [Minicart](https://developers.vtex.com/vtex-developer-docs/docs/vtex-minicart) to remove product list items.

1. Using a [development workspace](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-creating-a-development-workspace/), open you store's theme using any code editor;
2. In the `blocks.json` folder, look for the block responsible for rendering the desired icon. In our example, the minicart icon is the removal one and the block responsible for rendering it is called `remove-button`:

```json
  "flex-layout.col#remove-button.desktop": {
    "children": ["remove-button"],
    "props": {
      "marginLeft": "3"
    }
  },
```

3. Remove the block responsible for the icon and in its place add the Modal Layout's app `modal-trigger` block:

```json
  "flex-layout.col#remove-button.mobile": {
    "children": ["modal-trigger#confirmation-modal"],
    "props": {
      "marginLeft": "3"
    }
  },
```  

4. Then, declare the new `modal-trigger` block: list the `modal-layout` block as its child and, according to your store's scenario, list the icon you wish to trigger the modal. For example:

```json
  "modal-trigger#confirmation-modal": {
    "children": [
      "icon-delete",
      "modal-layout#confirmation-modal"
    ]
  },
```

>⚠️Looking at our example, the icon we wish to use to trigger the modal is the one for removal. We therefore add the `icon-delete` (exported by the Store Icons app) to the list of `modal-trigger` children. Choose the icon according to your store's scenario.

5. Then, declare the `modal-layout` block along with the `modal-actions` block as a child of the first. You can also declare other blocks you may want to have rendered in the modal, such as a [Rich Text](https://developers.vtex.com/vtex-developer-docs/docs/vtex-rich-text/). For example:

```json
  "modal-layout#confirmation-modal": {
    "children": [
      "modal-actions#confirmation-modal"    
    ]
  },
```

6. Upon declaring the `modal-actions` block, list `modal-actions.close` as its child, along with the block previously removed in step 3 to make way for `modal-trigger`. In our example, it's the `remove-button`:

```json
  "modal-actions#confirmation-modal": {
    "children": [
      "modal-actions.close",
      "remove-button"
    ]
  },
```

7. Once you're happy with the changes, follow our documentation on [making your theme content public](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-making-your-theme-content-public/) to make your configurations available to end users.


