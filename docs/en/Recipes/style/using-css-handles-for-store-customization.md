---
title: Using CSS Handles for store customization
description: "CSS Handles are magic tools developed by VTEX IO to make it easier to customize components using CSS. Have a look at this recipe for more on how to identify and apply CSS Handles to your store, without the need for HTML CSS selectors"
date: "10/24/2019"
tags: ["customization", "css", "css-selectors", "css-handles", "layout"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/style/using-css-handles-for-store-customization.md"
---

# Using CSS Handles for store customization

## Introduction 

CSS Handles is a **HTML elements identifier**. Therefore, it can be used to customize any of your store components by simply using CSS classes through the store theme's code. 

At the end of the day, CSS Handles are nothing more than your **store's layout building assistants**. Follow the step-by-step below and find out how to use them in a fast and simple way! 

## Step by step 

1. Upon inspecting the page, find the CSS Handle for the component you want to customize. 

![css-handles-inspect](https://user-images.githubusercontent.com/52087100/67318146-79cfef00-f4e1-11e9-8c63-56cae3c6d593.png)

During the inspection, bear in mind your store's following **component identification structure**: 

![component-id-structure](https://user-images.githubusercontent.com/52087100/67318281-adab1480-f4e1-11e9-9c8f-c20b8f0647ec.png)

2. In your store theme code, create a file inside the `css` folder, giving it the name of the app in which the inspected component is defined and adding `vtex.` as the beginning of the name and `.css` at the end, such as `vtex.store-components.css`. 
3. In the recently created file, declare the component's CSS Handle, taking into account the following format: 

```
.{CSSHandleName} {  
{CSSClass1}: {DesiredValue};
{CSSClass2}: {DesiredValue};  
}
```

_Remember to replace the value inserted in the keys with real values, according to your store's scenario._

Following the example given above, we get: 

![css-handles-vscode](https://user-images.githubusercontent.com/52087100/67318352-c287a800-f4e1-11e9-921c-ec3ed3b681f1.png) 

Once you app is linked and the changes duly saved, the new customization should immediately be reflected onto your workspace.  

<div class="alert alert-info">  
Our team is constantly working on developing CSS Handles for every possible store component. If however your are unable to find a CSS Handle for a component you wish to customize, share this scenario with us at <a href="https://github.com/vtex-apps/store-discussion">Store Discussion</a>.  
</div>

## Best practices

In order to standardize CSS customization and avoid any potential breakdown in layout, **we recommend store customization to be performed exclusively using CSS Handles**. 

However, it's common to come across store scenarios whose customization uses CSS Selectors. As the name implies, they are used to select elements for CSS customization according to the page HTML hierarchy. 

This customization practice by HTML hierarchy was mostly deprecated. It means that **only** the CSS Selectors listed below will continue to be allowed for your store customization:

- `:hover`   
- Link selectors, such as `:visited`, `:active` and `:focus`.   
- Every pseudo-element, such as  `::before`, `::after` and `::placeholder`. 
- `:nth-child(even)` and `:nth-child(odd)` 
- `:first-child` and `:last-child`
- Descendant combination element through space, such as `.{Element1} .{Element2}` 
- `[data-*]` 
- `:global(vtex-{AppName}-{AppVersion}-{ComponentName})`

**Any CSS Selectors not on this list, such as** `:nth-child`**,** `foo > bar` **and** `[alt="bar"]`**, will no longer be accepted by Toolbelt during the [linking](https://vtex.io/docs/recipes/store/linking-an-app) of the store's theme with its local files.**

<div class="alert alert-warning">  
Bear in mind that any customization that uses CSS Selectors is dependent on a HTML structure that, when changed, can break the retailer's desired customization.<strong> Always opt to use CSS Handles</strong>. 
</div>
