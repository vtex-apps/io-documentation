---
title: Improving your store's performance
description: "A common worry among us all: site performance. Check out now the good practices you must adopt in order to "
date: "2020-03-23"
tags: ["good", "practices", "guideline", "performance", "sales-conversion", "site"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/new-docs-and-fix/docs/en/Recipes/store-management/improving-your-stores-performance.md"
---

# Improving your store's performance

A common worry among e-commerce stores is **site performance**.

Such worries are more than understandable: to guarantee your brand's online success, you must absolutely look after your site's performance and how fast its content is displayed to end users, since this directly impacts the **sales conversion rate**, **user session time**, **bounce rate** and even the number of **visited pages** and **site findability**. 

Therefore, perfecting performance data from live stores is one of our product team's main responsibilities.

Check out our performance best practices that you can already implement in your store to ensure a better end user experience.

<div class="alert alert-info">
Once adopted, <strong>such practices can lead to a SEO improvement of up to 80% and over 50% in page loading time</strong>. This data can be identified in the main website performance analysis tools, such as Google Lighthouse and Google Analytics Load Time.
</div>

## Best practices

### Using the Fold blocks

Using the `__fold__` block directly impacts your website's initial loading performance, since this block is responsible for defining which interface components are loaded first for rendering and which are loaded with user scrolling.

In addition, the `__fold__.experimentalLazyAssets` block is tasked with indicating which of your theme's blocks are loaded statically until the first user interface interaction. 

Access the recipe on [**Using the Fold blocks**](https://vtex.io/docs/recipes/templates/using-the-fold-blocks/) in order to properly implement them in your store theme and improve your site's performance.

### Properly configuring the Menu

You can change your theme's Menu block configuration to adopt performance best practices. 

The first such practice is the **use of** `menu-item` **blocks as props** in scenarios in which these don't contain submenus declared within themselves.

The second practice that can be applied to the Menu is the **use of the** `experimentalOptimizeRendering` **prop** that prevents a whole chain of `submenus` to be loaded until the user interacts with the parent `menu` (in which the prop was configured).

These configurations generate significant changes in your theme's total number of blocks, optimizing its framework, loading and rendering and directly impacting the component's performance.  

<div class="alert alert-warn">
Google will not be able to track the hidden submenu items for SEO purposes, since their contents only will be loaded with user interaction. Therefore, ensure your SEO strategy is already covered by the store's sitemap or by the store's first meaningfully painted content.
</div>

Check out how to apply both configurations in the [**Menu's documentation**](https://vtex.io/docs/components/all/vtex.menu@2.24.1/).

### Adjusting image sizes

The size of a website's displayed images can directly impact its performance. Therefore, it's crucial that you **adopt best practices with regards to which media is used in your theme**.

Learn how to optimize your website's image rendering and improve its performance by reading the recipe on [**Best practices for rendering images**](https://vtex.io/docs/recipes/templates/best-practices-for-rendering-images/).

### Optimizing the `OrderFormProvider`

The `orderForm` is an object to record and fetch data from a user's order, including each item added to the cart.

In order to give theme blocks access to this information and thereby allow them to render it, Store Framework works with a `OrderFormProvider` in each store page that, behind the scenes, is responsible for exporting the needed order data to the blocks.

At present, all store using VTEX IO Store Framework have two `OrderFormProvider`s: a **legacy** one, still consumed by native blocks such as `minicart` and `buy-button`, and another newer, better suited to replace it.

Stores that already use the new `minicart.v2` and `add-to-cart-button` blocks, replacing the `minicart` and `buy-button`, can set aside the `OrderFormProvider` legacy and, therefore, improve your theme's performance - that now function with just 1 provider.

More details on how to perform this optimization can be found in the documentation on [**Enabling OrderForm optimization**](https://vtex.io/docs/recipes/store-management/enabling-order-form-optimization/).

### Building Shelf and Carousel components using Slider

Another important best practice is to build your theme's Shelf and Carousel blocks using Slider Layout.

That's because the **Slider Layout natively performs a lazy load of the product data being rendered**. In practice, this means that the information contained in a Shelf or Carousel built with Slider will only be loaded when components receive interaction from users, decreasing the website's page load time.

You can find more details on how to use the Slider Layout when configuring these two blocks by accessing the [**Shelf documentation**](https://vtex.io/docs/components/all/vtex.shelf/) and the recipe on [**Building a Carousel using Slider Layout**](https://vtex.io/docs/recipes/templates/building-a-carousel-using-slider-layout/).

<div class="alert alert-info">
The more products your Shelf or the more images your Carousel contains, the bigger the impact on your website's performance.
</div>

### Configuring the Search Result page

By being flooded with information on various products, the Search Results page can run into performance problems when loading or rendering its data.

Fortunately, there are **two key props** that change this scenario, namely `skusFilter` and `simulationBehavior`.

These two props are responsible for controlling the SKUs returned for each product in the Search query and for defining whether the displayed search data will be up-to-date or fetched using the cache, respectively.

To improve your search results page performance and consequently your website, we recommend that you **only allow the first available SKU to be returned for each product** (using the `FIRST_AVAILABLE` value in the `skusFilter` prop ) and that **use cache to display the search data** (using the `skip` value in the `simulationBehavior` prop).

Find out more about how to properly configure the above by going through our [**Search Results**](https://www.vtex.io/docs/components/all/vtex.search-result@3.56.1/) app documentation.
