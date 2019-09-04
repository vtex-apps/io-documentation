---
title: Creating a new custom page
description: "This guide will help you to learn how to create a new custom page in your website. You'll be introduced to the framework's template types and default pages. Also, a simple institutional page will be built from scratch."
date: "30/08/2019"
tags: ["institutional page", "page", "new page", "template", "institutional"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/creating-a-new-custom-page.md"
---

# Creating a new custom page

### Introduction
Stores are made of several different pages, each one with a different layout and content. When creating a store from scratch, some default pages are already available:

- store.home
- store.product
- store.search
- store.account
- store.login
- store.orderplaced

These default pages path are already defined in the Admin Pages. You can check them in the website:

>https://YOUR-ACCOUNT.myvtex.com/admin/cms/pages/

Notice that these URLs’ format cannot be changed, since they are default for every store. See the store.product's example:

![store-product-exp](https://user-images.githubusercontent.com/12139385/63775040-ea2d0c00-c8b4-11e9-8697-d33d40df45f4.png)

Besides these default pages, its possible to create other custom pages, such as the ones with Institutional content, or blog content.

It is necessary to create a new custom page whenever you need to define **new URLs with different layouts than the ones already created or defined by default.** 

This recipe will show you how to create a simple institutional page.


### Step by step

**1 - Create a template in your store theme**

Our store framework has 3 different templates’ context:

`Product` - Pages that must deal with the content of a single product. For instance,  a product details page. Every new product registry automatically generates a new product page.

`Product collections` - Pages that must deal with the content of a group of products. For instance, a search result page.

`Standard` - Pages that must deal with no specific product content. For instance, the home page.

> Even though standard pages are not directly linked to any specific product, they may show shelves or lists of any chosen group of products. The main difference is that the group of products to be shown on that page do not depend on the url content, but only on the setting of the shelf itself. 
Product pages, for instance, show the product that is defined in the page's url path, and search results pages show the list of products defined by the urls’ query.

As an institutional page is not directly connected to any specific product we will create a custom Standard Template.

We will create a simple template with a row that contains an image in its left column and, in its right column, a title and text content:

![store-product-exp](https://user-images.githubusercontent.com/12139385/63775975-dbdfef80-c8b6-11e9-9b76-e50924b828ae.png)

To do so, on your theme's source code, declare a custom template layout within your blocks folder:
```

{
 "store.custom#your-template-name-here": {
     "blocks": [	
     ]
  }
}
```

And then, fill them up with the blocks that will set the desired layout:

```
{
 "store.custom#your-template-name-here": {
   "blocks": [
     "flex-layout.row#about-us"
   ]
 },
 
 "flex-layout.row#about-us": {
   "children": [
     "image#about-us",
     "flex-layout.col#text-about-us"
   ]
 },
 
 "flex-layout.col#text-about-us": {
   "children": [
     "rich-text#about-title",
     "rich-text#about-content"
   ],
       "props": {
     "preventVerticalStretch": true
   }
 },
 
"rich-text#about-title": {
   "props": {
     "text":
     "# About us Title"
   }
 },
 
 "rich-text#about-content": {
   "props": {
     "text":
     " About us content - Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum"
   }
 },
 
 "image#about-us": {
   "props": {
     "src": "https://storecomponents.vteximg.com.br/arquivos/mobile-phone.png",
     "maxHeight": "600px"
   }
 }
}
```

Learn more about how the flex layout works in its own recipe.


**2 - Create your page's Route**

Go to your routes.json file, that can be found in the store folder. There, add a route to the json:
```
   "store.custom#your-template-name-here": {
   "path": "/your-url-here"
 }
```


**3 - Check if it worked**

Now, save your files and, through VTEX toolbelt, link the theme to your workspace.

>$ vtex link

Go to the page in your workspace and check that it works:

>https://yourworkspace--youraccount.myvtex.com/your-url-here

Check that everytime you create a new template, a new page is created at your Admin Pages, that can be reached at: 
 >https://yourworkspace--youraccount.myvtex.com/admin/cms/pages

Also, this new template becomes available to be set to any `Standard Page`.

![store-product-exp](https://user-images.githubusercontent.com/12139385/63776208-498c1b80-c8b7-11e9-9e46-3c7f76f58036.png)

>One template can serve different pages. The template will only set the layout of the page, hence you may use the same template to pages that share the same layout but have different URLs and content. To set a new url in your store with a template that already exists, just click on the `Create New` button of your store's Admin Pages, and choose your url and desired template. As these changes affect your workspace immediately, **it's always a good practice to create these new pages on production workspaces and not directly on master.**


**4 - Add content to your page on store-front**

>Be aware that a content can only be promoted to master if created in a **production workspace**. Before setting the content to your new page, check if you are in a production workspace in order to prevent rework.

Go to your storefront:
> https://yourworkspace--youraccount.myvtex.com/admin/cms/storefront

Then navigate to your custom page - or simply write it down at the Page url field. 
Now change the content to each one of the available components of the page.


**5 - Promote your workspace to master**

To make this page available in your store, you might simply promote your production workspace. You can find all the instructions to do so in its own recipe
