---
title: Enabling 404 pages
description: "Avoid problems with SEO by enabling 404 pages in your VTEX IO store."
date: "2020-05-23"
tags: ["404", "404-pages", "not-found", "http"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store-management/enabling-404-pages.md"
---

# Enabling 404 pages

The 404 error is an HTTP standard response code for when the server is not able to return a given browser request or is configured to not handle that request.

When navigating the internet, it's quite common to run across 404 pages or page Not Found when we ask the browser to perform an action that cannot be executed by the server, such as accessing a product page that was deactivated from the store's catalog.

For e-commerce companies, **one of the main advantages of enabling 404 pages is to avoid that Google indexes pages with paths that do not exist**, thereby harming the store's SEO and its customer experience.

In VTEX IO, 404 pages are **natively** enabled for a store's inexistent product pages. But in addition, it is also possible to allow 404 pages when URLs have one or more invalid segments, as shown in the step by step section below.

<div class="alert alert-warning">
A 404 HTTP response will return in case:
<li>A request for a non-existent URL segment is performed, for example, <code>https://mystore.myvtex.com/non-existent-path"</code>. It is possible to handle this error by adding a "map=ft" query-string, for example, <code>https://mystore.myvtex.com/non-existent-path?_q=non-existent-path&map=ft</code>. In this case, instead of returning a 404 page for the user, the API will interpret the "non-existent-path" string as a "full-text" (ft) search and will display the results of the search. That's why if a search is performed through the search bar, the query-string <code>map=ft</code> will automatically appear in the URL of the given search.</li> 
<li>A query string <code>map=specificationFilter</code> is used, for example, <code>https://mystore.myvtex.com/True?map=specificationFilter_410</code>. In this case, a 404 page will be displayed to the user.</li>
</div>

## Step by step

1. In your VTEX account's admin, access the App section and click on **My apps**;
2. Look for the **Rewriter** app and click on the gear button icon to go to its settings;
3. In the Settings section, check the radio button to **enable the 404 status code feature**. This will enable 404 pages on pages whose URLs have more than one invalid segments, following the restriction mentioned above;
4. Still in the Settings section, check the radio button to **enable 404 for paths with one segment**, e.g. `/foo`. This will enable 404 pages on pages whose URLs have one invalid segment, also following the restriction stated above;
5. Save your changes.

![404-pages](https://user-images.githubusercontent.com/52087100/82736157-cbea2480-9cfd-11ea-9efc-6a6c62467c5b.gif)

Once your changes are duly saved, your store is ready to display 404 pages whenever one of these scenarios occurs.

### Customizing your 404 Page

Now that you've enabled 404 pages in your store for the scenarios stated above, you can customize them using blocks in your store's theme following the step by step below:

1. In your terminal, [create a development workspace](https://vtex.io/docs/recipes/development/creating-a-development-workspace/);
2. Then, open your store theme app using your preferred code editor;
3. In the theme's product or search template (`store.product` or `store.search` in the `blocks` folder) you can declare, respectively, the block `store.not-found#product` or `store.not-found#search`  and have it contain, for example, another Rich Text block inside. 

 Find below an example of a `store.not-found#product` in a product template: 
 
```json
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

4. Save your changes and then run `vtex link` in your terminal to witness the above block being rendered in your development workspace as follows:  

![not-found-block](https://user-images.githubusercontent.com/52087100/76447318-4108b780-63a7-11ea-9b03-77413e0e4855.png)

5. If you’re happy with all your configurations, [release](https://vtex.io/docs/recipes/development/releasing-a-new-app-version/) a new version for your store theme app and then [publish](https://vtex.io/docs/recipes/development/publishing-an-app/) it;
6. Then, [create a production workspace](https://vtex.io/docs/recipes/store/promoting-a-workspace-to-master) and [install](https://vtex.io/docs/recipes/development/installing-an-app/)  the store theme app (in the version previously published) in it;
7. Access your store through your product workspace ({workspaceName}--{accountName}.myvtex.com) and inspect the page to ensure everything is running normally;
8. Finally, [promote your production workspace](https://vtex.io/docs/recipes/store/promoting-a-workspace-to-master) to master, making the changes permanent and public to your end-users.
