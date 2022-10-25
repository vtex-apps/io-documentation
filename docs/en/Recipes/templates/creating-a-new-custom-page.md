---
title: Creating a custom page
description: "Learn how to define a different layout, path and content for a store’s new custom page."
date: "2019-08-30"
tags: ["institutional-page", "page", "new-page", "template", "institutional"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/layout/creating-a-new-custom-page.md"
---

# Creating a new custom page

Stores are made up of several different pages, each one having a different layout and content. When creating a store from scratch in VTEX IO, some default pages with predefined URLs are already available to you, such as:

- `store.home` - Home page
- `store.product`- Product page
- `store.search` - Search Results page
- `store.account` - Client Account page
- `store.login` - Login page
- `store.orderplaced` - Order Placed page

>ℹ️ You can manage each page's title and template in the Pages section, within the admin's CMS. 

However, you may want to create a new custom page to attend your store's specific needs. In this case, a new URL and content to go with it must be created by you from scratch.  

## Step by step

Follow the steps below and learn how to define a different layout and path for a new store page:

1. Create a **new template** in your store theme.
2. Create your **new page's path**.
3. **Add content** to your page.
4. Making your new theme content **publicly available**.

### Creating the new template

A template sets the page layout, so if you want to create a custom page for your store you also will need to create a new template for it. 

In order to do so, you first must choose one of three template types to host your new page:

- **Product** - For pages that must deal with the content of a single product. For instance, a product details page. Adding any new product automatically generates a new Product page.

- **Product collections** - For pages containing a group of products, such as the Search Result page.

- **Standard** - For pages with no specific product content. For instance, the Home page.

>ℹ️ Even though `Standard` pages are not directly linked to any specific product, they may display shelves or lists of any chosen group of products. The main difference is that the group of products shown in such page does not depend on the URL query, but only on the setting of the shelf itself. 

Let's suppose we are going to create a simple About Us page for a store. As such the page is not directly connected to any specific product, we should create a custom `Standard` template for it with an image in its left column and a a title and text content in its right column:

![store-product-exp](https://user-images.githubusercontent.com/12139385/63775975-dbdfef80-c8b6-11e9-9b76-e50924b828ae.png)

1. In your store theme's code, declare a new template within your `blocks` folder or `blocks.jsonc` file.

```json
{
 "store.custom#{templatename}": {
     "blocks": [  
     ]
  }
}
```

2. Fill it out with the blocks that will set the desired layout. For example:

```json
{
 "store.custom#{templatename}": {
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

To learn more about how the Flex Layout works, access its [documentation](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-using-flex-layout).

### Creating the new page's path

Now that your page layout has been defined in the store theme code, the next step is to define the page's path to make the page accessible. You can define it through direct code changes or by using the account's admin. 

#### Through code changes

1. In your theme's source code, access the `routes.json` file. It can be found in the `store` folder. 
2. There, add a path to the recently created template's JSON:

```json
"store.custom#{templatename}": {
  "path": "/{URL}"
}
```

3. Save your files.
4. [Link](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-linking-an-app/) the theme to a Development workspace. You will be able to access and see your new page live through your workspace, using the following format: `{workspaceName}--{accountName}.myvtex.com/{pathName}.

#### Using the account admin

If you prefer to set the new page path using account admin, you must first must [release](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-releasing-a-new-app-version) your changes regarding template creation and [install](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-installing-an-app) the new version of your store theme in a [production workspace](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-creating-a-production-workspace).

Once your changes are set up in a Production workspace, you will be able to use the admin's CMS to create the page's path:

1. Access the admin's **Pages** section.
2. Click on **Create New**.
3. Choose the desired URL and any created template. For instance, the About Us page template previously created:

![custom-pages-pages](https://user-images.githubusercontent.com/52087100/64428903-36353900-d08b-11e9-8d19-186c8831b4d7.png)

Notice that a template only sets the page layout, hence any new template becomes available to be set on any page that accepts templates of the same type as the page itself.

>ℹ️ When editing any content using the CMS section, it's always good to make your changes in a production workspace. Therefore, make sure you are not creating your new custom page in the store's master workspace.

### Adding the content

Your new page now has a custom layout, thanks to the newly created template, and can be accessed thanks to its route creation. The next step is editing its content.

You can define your page content performing changes directly to your Store Theme app or using the admin's Site Editor. When using this last one, you can browse to your custom page or simply write its URL in the `Page URL` field. For example:

![custom-pages-siteeditor](https://user-images.githubusercontent.com/52087100/64428904-36cdcf80-d08b-11e9-8de4-06bf0a89b14f.png)

### Making your theme content publicly available

If you are happy with the changes to your store theme, make your new theme content public. Up until this point, the changes were performed in your development workspace. Access our documentation on [**making your theme content publicly available**](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-making-your-theme-content-public/) and follow the steps detailed there. 
