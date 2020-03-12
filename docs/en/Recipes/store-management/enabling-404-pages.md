---
title: Enabling 404 pages
description: "Avoid problemas with SEO by enabling 404 pages in your store."
date: "2020-03-11"
tags: ["404", "404-pages", "not-found", "HTTP"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/development/enabling-404-pages.md"
---

# Enabling 404 pages

The 404 error is a HTTP standard response code for when the server was not able to return what the browser request or was configured to not handle that request. 

When navigating the internet, it's quite common to run across 404 pages or page Not Found errors when we ask the browser to perform an action that cannot be executed by the server, such as accessing a product page that was deactivated from the store's catalog.

For e-commerce companies, one of the main advantages of enabling 404 pages is to avoid that Google indexes pages with paths that do not exist, thereby harming the store's SEO and its customer experience. 

You can also enable 404 pages for your store by going through the following 4 steps:

## Step by step

### Step 1 - Enabling the Broadcaster notification

The Broadcaster Worker is an app that checks for catalog changes and triggers events for other platform services, such as  Store Indexer (which is responsible for indexing a store's routes). 

One of the vital steps to configuring 404 pages is reindexing the Catalog, ensuring that all store routes are up-to-date with the module's latest information.

Since the Broadcaster merely triggers events in response to Catalog changes and no change is performed when reindexing, you'll need to configure the app to trigger the event even in such cases.

As such, the Store Indexer receives the broadcasted event and properly indexes all routes based on how the Catalog was reindexed (which we'll look at in step 3 below).

1. Access the desired account's admin. You can use the following URL structure: `{accountName}.myvtex.com/admin` ;
3. Access the **Apps** section, in the admin's sidebar;
4. Select the **Broadcaster Worker** app box. If the card is not available, you must first [install](https://vtex.io/docs/recipes/store/installing-an-app) the app on the account;
5. Check the `Always Notify` box in the Broadcaster app and save your changes. 

![broadcaster-worker](https://user-images.githubusercontent.com/52087100/76466530-a61fd580-63c6-11ea-8e1d-1d0dda1feb7a.png)

### Step 2 - Re-indexing the Catalog

Before configuring the 404 behavior, you need to reindex the store's catalog to ensure that every store route is properly saved in VBase. 

1. [Reindex the account's catalog](https://help.vtex.com/tutorial/understanding-how-to-maintain-a-database--34P9LGs7BCIQK6acQom802). You can use the following URL structure: `{accountName}.vtexcommercestable.com.br/admin/Site/fullcleanup.aspx`;


<div class="alert alert-info">  
Depending on the size of your catalog, it may take a couple of hours to reindex everything and save every store route in VBase. Therefore, before moving on to the next steps, it is strongly recommended to wait a couple of hours. 
</div> 

2. Once it was reindexed, navigate your store's pages to check whether every route is correct and every page is being rendered properly;
3. Uncheck the `Broadcaster` app's `Always Notify` box and save your changes. 

### Step 3 - Enabling Fallback functionality in Rewriter

The Rewriter is a service at the forefront of the operation, responsible for receiving browser requests and directing them to the server. 

Therefore, to complete the configuration of 404 pages, we need to configure the Rewriter so that is knows that it should return a 404 error every time the server does not meet the browser requirements.

1. Access the account's admin from a [production workspace ](https://vtex.io/docs/recipes/store/creating-a-production-workspace). You can use the following URL structure, replacing the values between {} according to your scenario: `{workspaceName}--{accountName}.myvtex.com/admin` ;
2. Access the **Apps** section, in the admin's sidebar;
3. Select the **Rewriter** app box. If the card is not available, you must first [install](https://vtex.io/docs/recipes/store/installing-an-app) the app on the account;
4. Check the `Enable fallback entities` box in the Rewriter app and save your changes. Make sure you are still navigating using the workspace created in the previous step;
5. [Promote](https://vtex.io/docs/recipes/store/promoting-a-workspace-to-master) your workspace to Master.

### Step 4 - Building your 404 Page

Now that you've enabled 404 pages in your store, you need to access your store's theme and use blocks to define this page's interface.

Follow these steps:

1. Create a development workspace;
2. Open the store's theme in your preferred code editor;
3. In the theme's product or search template (`store.product` or `store.search`) you can declare, respectively, the block `store.not-found#product` or `store.not-found#search`  and have it contain another Rich Text block. 
 
 Find below an example of a `store.not-found#product` in a product template: 

```JSON
"store.not-found#product": {
  "blocks": ["rich-text#not-found"]
},

"rich-text#not-found": {
  "props": {
    "textAlignment": "CENTER",
    "textPosition": "CENTER",
    "text": "**PAGE NOT FOUND**",
    "font": "t-heading-1"
  }
}
```

<div class="alert alert-info">  
The <code>store.not-found</code> blocks will only be triggered when the server returns a 404 error for a browser request. In such scenarios, the block that is set as child will be effectively rendered to users. 
</div> 

4. Run `vtex link` and witness the above block being rendered as follows:  

![not-found-block](https://user-images.githubusercontent.com/52087100/76447318-4108b780-63a7-11ea-9b03-77413e0e4855.png)

5. If you're happy with all your configurations, repeat everything in a [production workspace](https://vtex.io/docs/recipes/store/creating-a-production-workspace);
6. Lastly, [promote your production workspace](https://vtex.io/docs/recipes/store/promoting-a-workspace-to-master) to Master.
--- 

Done! Once the fourth and final step is completed, you can test the new 404 pages in your store. Simply access an already deactivated product page and witness to magic happen!