---
title: Creating a custom search results page
description: "Engage your users with specific products through an URL path! Learn how to create a custom search results page for your store's website."
date: "2020-08-11"
tags: ["custom", "search-result", "search-results-page"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/edit/master/docs/en/Recipes/templates/creating-a-custom-search-results-page.md"
---

# Creating a custom search results page

When [creating a brand new landing page](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-creating-a-new-custom-page/) for your store's website, you can decide to promote in it certain products to increase their sales or even user interactions, creating then a custom search results page. 

Even though custom pages do not have the needed context to fetch search data, since they are build from scratch, the `search-result-layout.customQuery` block from the [Search Result app](https://developers.vtex.com/vtex-developer-docs/docs/vtex-search-result/) is able to specify which query should be performed in order to get and render the desired search results for your users. 

**Engage your users with specific products through an URL path!** Check out the instructions below: 

## Step by step

>⚠️ In order to build a custom search results page for your store, you must understand how a search results page is built and works in the first place. Access the  <a href="https://developers.vtex.com/vtex-developer-docs/docs/vtex-search-result/">Search Result app documentation</a> and learn more about the blocks exported by this app, including the `search-result-layout.customQuery`. 

1. Access your Store Theme app directory using whichever code editor you prefer. 
2. In the `routes.json` file, define a new path called `store.custom#landing`, as shown below:

```json
"store.custom#landing": {
  "path": "/landing"
}
```

>ℹ️ The value defined for `path` can and should be replaced according to what is most suitable for your store's scenario. 

3. In the `blocks.jsonc` folder, create a new file to store the new custom search results page blocks. The new file could be called `search-landing.jsonc`, for example. 
4. In the file, declare the new custom page template name, such as `store.custom#landing`. Notice that the name must match the one declared in *step 2*.
5. In the template's block list, add any theme block you want to build your new custom page. But remember: the `search-result-layout.customQuery` block is mandatory in order to define how the search query should be fetched. For example:

```json
{
  "store.custom#landing": { 
    "blocks": [
      "image#landingbanner", 
      "search-result-layout.customQuery"
    ]
  }
}
```

>ℹ️ You can learn how to use the `search-result-layout.customQuery` block in order to define how the search query data should be fetched accessing the <a href="https://developers.vtex.com/vtex-developer-docs/docs/vtex-search-result/">3rd step of the Search Result app documentation</a>. 

6. Declare the blocks according to the search results custom page you wish to have. Below you can find an example of a custom search results template: 

```json
{
  "store.custom#landing": { 
    "blocks": ["image#landing", "search-result-layout.customQuery"]
  },
  "image#landing": { 
    "props": { 
      "minWidth": "100%",
      "src": "https://user-images.githubusercontent.com/18701182/69889938-64b16180-12d2-11ea-8d8a-e3089cbeaffd.png"
    }
  },
  "search-result-layout.customQuery": {
    "props": {
      "querySchema": {
        "orderByField": "OrderByReleaseDateDESC",
        "hideUnavailableItems": true,
        "maxItemsPerPage": 8,
        "queryField": "Blue Top Retro Camera",
        "mapField": "ft"
      }
    },
    "blocks": [
      "search-result-layout.desktop",
      "search-result-layout.mobile",
      "search-not-found-layout"
    ]
  },
  "search-result-layout.desktop": {
    "children": [
      "breadcrumb.search",
      "search-title.v2",
      "flex-layout.row#top",
      "search-fetch-previous",
      "flex-layout.row#results",
      "search-fetch-more"
    ],
    "props": {
      "pagination": "show-more",
      "preventRouteChange": true
    }
  },
  "flex-layout.row#top": { 
    "children": [
      "total-products.v2",
      "order-by.v2"
    ]
  },
  "flex-layout.row#results": { 
    "children": [ 
      "flex-layout.col#filter",
      "flex-layout.col#search"
    ]
  },
  "flex-layout.col#filter": { 
    "props": {
      "width": "20%"
    },
    "children": [
      "filter-navigator.v3"
    ]
  },
  "flex-layout.col#search": { 
    "children": [
      "search-content"
    ]
  },
  "search-content": { 
    "blocks": ["gallery", "not-found"]
  },
  "gallery": {
    "blocks": ["product-summary.shelf"]
  }
}
```

7. Save the changes performed in your Store Theme app. 
8. [Using your terminal](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installation-and-command-reference/), log in to your VTEX Account and [create a new development workspace](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-creating-a-development-workspace/).
9. Once logged into the desired account and workspace, [link](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-linking-an-app/) your Store Theme app in order to see your new custom page live. 
10. Access your store's website using the following format: `{workspaceName}--{accountName}.myvtex.com/{pathName}`. You should see your new page live. 

If you are happy with the changes to your store theme, make your new theme content public. Up until this point, only you could see it in your development workspace. Access our documentation on [**making your theme content publicly available**](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-making-your-theme-content-public/) and follow the steps detailed there. 



