---
title: Enabling 404 pages
description: "Avoid problems with SEO by enabling 404 pages in your VTEX IO store."
date: "2020-05-23"
tags: ["404", "404-pages", "not-found", "http"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store-management/enabling-404-pages.md"
---

# Enabling 404 pages

The 404 error is a HTTP standard response code for when the server was not able to return what the browser request or was configured to not handle that request.

When navigating the internet, it's quite common to run across 404 pages or page Not Found when we ask the browser to perform an action that cannot be executed by the server, such as accessing a product page that was deactivated from the store's catalog.

For e-commerce companies, **one of the main advantages of enabling 404 pages is to avoid that Google indexes pages with paths that do not exist**, thereby harming the store's SEO and its customer experience.

In VTEX IO, 404 pages are **natively** enabled for inexistent product pages and for URLs that have more than one invalid segment. But in addition, it is also possible to allow 404 pages when URLs have a **single** invalid segment, as shown in the step by step section below.

>ℹ️ Due to implementation rules, the native functionality of 404 pages does not function for URLs originating from user searches. The reason behind this is that URLs originating from product searches include the `map=ft` parameter in their path, helping the platform to interpret that such URL segments reflect user performed searches, and thus should not be interpreted as non-existent (which would lead to a 404 page being rendered).

>⚠️ In rare cases when the parameter `map=specificationFilter` is present in the path of such search originated URLs, 404 pages may be rendered. This happens because the platform cannot interpret these URL segments as originating from user searches since it cannot find the `map=ft` parameter usually present in such URLs. This behavior is uncommon and is being addressed by our product team.

## Step by step

1. In your VTEX account's admin, access the App section and click on **My apps**.
2. Look for the **Rewriter** app and click on the gear button icon to go to its settings.
3. In the Settings section, check the radio button to **enable 404 for paths with one segment**, e.g. `/foo`. This will enable 404 pages on pages whose URLs have one invalid segment, following the restriction stated above.
4. Save your changes.

![404-pages](https://user-images.githubusercontent.com/60782333/87157435-a0fb6600-c294-11ea-8f46-e47ac4549c6f.png)

Once your changes are duly saved, your store is ready to display 404 pages whenever this scenario occurs.

### Customizing your 404 Page

You can customize 404 pages using blocks in your store's theme following the step by step below:

1. In your terminal, [create a development workspace](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-creating-a-development-workspace/).
2. Then, open your store's theme in it using your preferred code editor.
3. In the theme's product or search template (`store.product` or `store.search`) you can declare, respectively, the block `store.not-found#product` or `store.not-found#search`  and have it contain another Rich Text block. 

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

>ℹ️ The `store.not-found` blocks will only be triggered when the server returns a 404 error for a browser request. In such scenarios, the block that is set as child will be effectively rendered to users.

4. Save your changes and then run `vtex link` in your terminal to witness the above block being rendered as follows:  

![not-found-block](https://user-images.githubusercontent.com/52087100/76447318-4108b780-63a7-11ea-9b03-77413e0e4855.png)

5. If you're happy with all configurations done in your Development workspace, it is time do [make your new theme version publicly available](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-making-your-theme-content-public/). 
