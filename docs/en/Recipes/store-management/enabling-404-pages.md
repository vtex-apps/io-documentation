---	
title: Enabling 404 pages	
description: "Avoid problems with SEO by enabling 404 pages in your VTEX IO store."	
date: "2020-05-23"	
tags: ["404", "404-pages", "not-found", "HTTP"]	
version: "0.x"	
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store-management"	
---

# Enabling 404 pages

The 404 error is a HTTP standard response code for when the server was not able to return what the browser request or was configured to not handle that request.

When navigating the internet, it's quite common to run across 404 pages or page Not Found when we ask the browser to perform an action that cannot be executed by the server, such as accessing a product page that was deactivated from the store's catalog.

For e-commerce companies, **one of the main advantages of enabling 404 pages is to avoid that Google indexes pages with paths that do not exist**, thereby harming the store's SEO and its customer experience.

In VTEX IO, 404 pages are **natively** enabled for a store's inexistent product pages. But in addition, it is also possible to allow 404 pages when URLs have one or more invalid segments, as shown in the step by step section below.

<div class="alert alert-warning">
Note that the 404 behavior only works on pages whose URLs have one invalid segment if the query-string <code>map=ft</code> is added to the path when a search is being performed, such as <code>https://storecomponents.myvtex.com/top?_q=top&map=ft</code> instead of <code>https://boticario.myvtex.com/top</code>. In the latter scenario, due to implementation rules, the 404 page will not be rendered even if it was properly configured.
</div>

<div class="alert alert-warning">
For pages whose URLs have more than one invalid segment, the 404 behavior only works for stores not using the new VTEX Intelligent Search. When using the Search solution, due to implementation rules, the 404 page will not be rendered even if it was properly configured.
</div>

## Step by step

1. In your VTEX account's admin, access the App section and click on My apps;
2. Look for the **Rewriter** app and click on the gear button icon to go to its settings;
3. In the Settings section, check the radio button to **enable the 404 status code feature**. This will enable 404 pages on pages whose URLs have more than one invalid segments, following the restriction mentioned above;
4. Still in the Settings section, check the radio button to **enable 404 for paths with one segment**, e.g. `/foo`. This will enable 404 pages on pages whose URLs have one invalid segment, also following the restriction stated above;
5. Save your changes.

![404-pages](https://user-images.githubusercontent.com/52087100/82736157-cbea2480-9cfd-11ea-9efc-6a6c62467c5b.gif)

Once your changes are duly saved, your store is ready to display 404 pages whenever one of these scenarios occurs.

<div class="alert alert-info">
For now, no customization is allowed on the 404 pages displayed. The product team is working on a more flexible functionality solution that will be deployed soon.
</div>
