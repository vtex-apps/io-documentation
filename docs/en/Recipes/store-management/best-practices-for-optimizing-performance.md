---
title: Best practices for optimizing performance
description: "A common worry among us all: website performance. Check out now the good practices you must adopt in order to have the fastest store ever!"
date: "2020-03-23"
tags: ["good", "practices", "guideline", "performance", "sales-conversion", "site"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store-management/best-practices-for-optimizing-performance.md"
---

# Optimizing performance

For the e-commerce business, appealing offers, high-quality products, or brand recognition might not be enough for *converting leads* if *user-experience* is left behind.

In digital, the store's website *performance* plays an essential role in *user-experience*, directly impacting *sales conversion rate* and *user session time*, among other important metrics.

Every millisecond counts and affects not only *the consumer decision-making* process but also your store's website *rank* in search engine results.

Thus, to help you guarantee the success of your brand's online presence, this article presents a few practices you can implement to optimize your store's performance and, consequently, improve the shopper experience.

Some actions that can boost your store's website performance can be enabled in your store's Admin Panel, under *Store Setup > CMS > Store > Advanced*.

![cms-store-advanced](https://user-images.githubusercontent.com/52087100/96817679-3a8af580-13f6-11eb-918d-2c60e7c685df.png)

These features are presented and explained in the [Enabling store settings](#enabling-store-settings) section.

Furthermore, additional actions, presented in the [Manual optimizations](#manual-optimizations) section, can be taken.

>⚠️ For implementation details, check our documentation on [how to safely enable performance settings in your store.](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-safely-enabling-performance-settings)

Once adopted, such practices can lead to an improvement of up to 80% in SEO and over 50% in page loading time. This data can be identified in the main website performance analysis tools, such as [Google Lighthouse](https://developers.google.com/web/tools/lighthouse) and [Google Analytics](https://support.google.com/analytics/answer/1205784?hl=en).

## Enabling store settings

### Optimizing the shopping cart data fetching

The `orderForm` is an object used to record and fetch data from a user's order, including each item added to the cart.

To give other store theme blocks access to the `orderForm` stored data and, consequently, allow them to render it, Store Framework runs the `OrderFormProvider` object in each store page. This object is responsible for exporting all the necessary `orderForm` data to these blocks.

However, currently, all stores using VTEX IO Store Framework have two `OrderFormProviders`: a legacy one, still consumed by native blocks such as `minicart` and `buy-button`, and another newer, better suited to replace it.

As a result, we recommend that stores already using the new `minicart.v2` and `add-to-cart-button` blocks (instead of the `minicart` and `buy-button`, respectively) set aside the `OrderFormProvider` legacy. This way, consuming a single provider, you'll notice improvements in your store performance.

>ℹ️ More details on how to perform this optimization can be found in the documentation on [Enabling OrderForm optimization](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-enabling-order-form-optimization/).

### Deactivating the VTEX IO native service worker

The VTEX IO platform provides a native service worker to every store using the Store Framework. However, since a website can only run one service worker at a time, you may face conflicts when working with a third-party service that provides its own service worker.

Hence, you can choose to deactivate the native service worker provided by VTEX IO in order to successfully use a third-party solution in your store.

>ℹ️ For more information, check our documentation on [Deactivating the VTEX IO native service worker](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-deactivating-the-vtex-io-native-service-worker/).

### Optimizing critical CSS

The content which a user first sees when opening a web page is known as *above-the-fold*. Besides, since this part of the page must be loaded quickly for better user experience, it can also be referred to as *critical*.

![critical](https://user-images.githubusercontent.com/60782333/93504484-ed47cf80-f8ef-11ea-8af9-4d640f9cfe6b.png)

In other words, before anything else, the critical part of the page must be correctly and promptly rendered. 

However, by default, the browser starts rendering a web page only after it has finished loading, parsing, and executing all related CSS files. As a result, given large CSS codes, the time taken by a browser to render the critical part of the page can significantly increase. 

Fortunately, VTEX IO offers the possibility of enabling critical CSS optimization in home pages. This feature provides the browser a way to find the *minimum blocks of CSS code* needed to first display the critical content of the page. Meanwhile, the remainder CSS code is loaded asynchronously.

>⚠️ Keep in mind that by enabling this option, you might notice style inconsistencies in your store's layout. Hence, test it with caution before enabling it on a production workspace. Also, if you notice any kind of side-effect on your store's website, please [open a ticket](https://help-tickets.vtex.com/smartlink/sso/login/zendesk) and let us know!

### Improving download speed with CSS concatenation

To properly display a web page layout, the browser needs to make multiple HTTP requests to download each CSS file. However, numerous requests might increase the time taken to render a single web page. 

In this sense, VTEX IO offers the possibility of avoiding various download requests by concatenating multiple CSS files into one. 

![concatenation](https://user-images.githubusercontent.com/60782333/93513175-dd35ed00-f8fb-11ea-8da4-95acd6b56d3f.png)

Notice that, by combining CSS in a single file, the browser makes fewer requests and loads web pages faster, improving your store website's performance.

### Lazy loading page metadata 

Before displaying a web page, the VTEX IO service app responsible for server-side rendering, or simply, the Render Runtime, interprets the page's metadata script. An example of the before-mentioned script is presented below.

```ts
<script>
        __RUNTIME__ = {"account":"vtexstore","amp":false,"bindingChanged":false,"binding":{"id":"aacb04t3-a8fa-4bab-b5bd-2d654d20dcd8","canonicalBaseAddress":"vtexstore.vtex.com"},"culture":{"availableLocales":[],"country":"USA","currency":"USD","language":"en","locale":"en-US","customCurrencyDecimalDigits":null,"customCurrencySymbol":"$"},"production":true,"query":{},"settings":{....
```

Notice that this script holds many important data about a web page and it can be long, characterizing a long task to be performed by the browser. 

Therefore, to avoid your store website's total blocking time to be compromised, by enabling the lazy runtime, such script will be broken into smaller ones.

This way, long tasks will be prevented and you'll advantage of a faster store.

>⚠️ Keep in mind that, by enabling this option, some apps might not work as expected. Hence, test it with caution, and analyze the effects on different pages of your website before enabling it on a production workspace. Also, if you notice any kind of side-effect on your store's website, please [open a ticket](https://help-tickets.vtex.com/smartlink/sso/login/zendesk) and let us know!

### Lazy rendering submenu items

By enabling this option, menus containing submenus will take advantage of automatically having the `experimentalOptimizeRendering` prop enabled. Such configuration prevents a whole chain of `submenu`s to be loaded unnecessarily. 

Therefore, `submenu`s will be loaded only in case the user interacts with its parent menu (in which the prop was configured).

>⚠️ Google will not be able to track the hidden submenu items for SEO purposes, since their contents only will be loaded with user interaction. Therefore, ensure your SEO strategy is already covered by the store's sitemap or by the store's first meaningfully painted content.

### Lazy rendering search results and facets

By enabling this option, scrollable facets box and search result pages will be lazy rendered.

This way, content contained inside the user's viewport will be initially loaded for rendering. On the other hand, content outside the user viewport will be loaded only during scrolling. 

>⚠️ Keep in mind that, by enabling this option, you might notice unexpected behaviors, such as gaps while scrolling. Hence, if you experience any kind of side-effect in your website pages, please [open a ticket](https://help-tickets.vtex.com/smartlink/sso/login/zendesk) and let us know!

### Partially fetching facets 

This option improves search pages' performance by partially fetching the total number of facets available to be displayed.

Once this option is enabled, users on the search results page will see a maximum of 10 facets per filter - the remaining facets, if any, will not be automatically fetched by the search query, nor displayed to the end-user. 

Instead, a `Show more` button will be displayed below the rendered facets, allowing users to fetch the remaining ones.

>ℹ️ Remember: we call Facets the filter's value. For example: `Color` is a filter whose value, `Blue`, is its Facet.

## Manual optimizations

### Improving scrolling performance

We recommend the use of the `__fold__` block in scrollable pages. 

With this block, it's possible to define which interface components will be initially loaded for rendering and which will be loaded during user scrolling. 

This way, only the first visible blocks will be loaded, and the ones "below the fold" will be lazy-loaded during scrolling.

In addition, use the `__fold__.experimentalLazyAssets` block to indicate which of your theme's blocks must be loaded statically until the first user interface interaction with it.

>ℹ️ Follow [this link](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-using-the-fold-blocks/) to learn more about Fold blocks.

>⚠️ If any of these blocks cause any kind of side-effect in your website pages, please [open a ticket](https://help-tickets.vtex.com/smartlink/sso/login/zendesk) and let us know!

### Reducing the number of menu blocks

In scenarios in which a Menu block doesn't contain submenus declared within itself, we recommend that you change its configuration to use `menu-item` blocks as props.

For instance, in the example below, the main `menu-items` (Apparel & Accessories, Home & Decor, and More) cannot have their implementation changed. They must remain as children, since they have a trigger to open a `submenu`.

![menu](https://user-images.githubusercontent.com/60782333/93248000-9a421100-f765-11ea-90b1-144f7622138d.png)

The internal `menu-items` (Clothing, Accessories and, Eyeglasses), however, can have their implementation changed from children to props. 

Notice that, previously, every `menu-item` was configured as a children/block. With the change, the `menu-items` group, declared as props, is interpreted as a single block (blue square). 

This way, the number of blocks is reduced from 3 to 1. 

>ℹ️ Check out how to apply both configurations in the [Menu's documentation](https://developers.vtex.com/vtex-developer-docs/docs/vtex-menu).

### Adjusting image sizes

The size of the displayed images in your store's website can directly impact overall performance. Thus, to optimize your website's image rendering, we recommend that you adopt the practices detailed on [Best practices for rendering images](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-best-practices-for-rendering-images/), with regards to the media type used in your theme.

>ℹ️ Follow this [link](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-best-practices-for-rendering-images/) to learn more about the best practices for rendering images.

### Improving search results

By being flooded with information on various products, the Search Results page can run into performance problems when loading or rendering its data.

Fortunately, there are two props that can change this scenario, namely `skusFilter` and `simulationBehavior`.

These props are responsible for controlling the SKUs returned for each product in the Search query and for defining whether the displayed search data will be up-to-date (`skusFilter`) or fetched using the cache (`simulationBehavior`).

We recommend that you only allow the first available SKU to be returned for each product (using the `FIRST_AVAILABLE` value in the `skusFilter` prop) and that use cache to display the search data (using the `skip` value in the `simulationBehavior` prop).

>ℹ️ Find out more about how to properly configure the above by going through our [Search Results app documentation](https://developers.vtex.com/vtex-developer-docs/docs/vtex-search-result).

### Lazy loading images and products data in a slider

We recommend that you build your theme's Shelf and Carousel blocks using the Slider Layout.

That's because the Slider Layout natively performs a lazy load of the images or product data being rendered. That means that the information contained in a Shelf or Carousel built with Slider will only be loaded when components receive interaction from users, decreasing the website's page load time.

However, always keep in mind that the more products your Shelf or the more images your Carousel contains, the bigger the impact on your website's performance.

>ℹ️ You can find more details on how to use the Slider Layout when configuring these two blocks by accessing the [Shelf documentation](https://developers.vtex.com/vtex-developer-docs/docs/vtex-shelf/) and the recipe on [Building a Carousel using Slider Layout](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-building-a-carousel-using-slider-layout/).
