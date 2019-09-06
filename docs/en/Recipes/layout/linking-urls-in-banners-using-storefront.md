---
title: Linking URLs in banners using Storefront
description: "Linking URLs in banners can be a great opportunity to influence user browsing! Check out how fast and easy linking URLs in your store's banners can be when using Storefront."
date: "2019-08-21"
tags: ["storefront", "url", "banner", "link", "linking", "internal-url", "external-url", "redirect"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/layout/LinkingURLsInBannersUsingStorefront.md"
---

# Linking URLs in banners using Storefront

You can configure one of your store’s banner to have page redirect, meaning that it can take users to any address of your choosing. To configure this using Storefront, simply link the banner to any external or internal URL by following the steps below:

## Internal URLs

1. Access the **CMS** module.
2. Click on **Storefront**.
3. Select the **Carousel** block and choose the banner that will have its content edited.
4. Maintain the **External route** toggle active and in the `Internal URL` field, simply copy and paste the internal desired address.


Indicate that an internal URL will be inserted in the banner, selecting the **External Route** toggle. Then, in the `Internal URL` field, simply copy and paste the internal desired address.

![internal-url-field](https://user-images.githubusercontent.com/52087100/63995069-6e59dc00-cacd-11e9-92de-da14a89b4117.png)

5. Click on **Save**.

<div class="alert alert-warning">
The <code>Banner target page</code> and <code>Params</code> fields were deprecated. Therefore, the filled in Internal URL data will be the only data taken into account when indicating the desired internal route.
</div>

## External URLs

1. Access the **CMS** module.
2. Click on **Storefront**.
3. Select the **Carousel** block and choose the banner that will have its content edited.
4. Selecting the **External Route** toggle and in the `URL (external)` field, simply copy and paste the external desired address.

![external-url-field-storefront](https://user-images.githubusercontent.com/52087100/63995053-541ffe00-cacd-11e9-9760-385e2f526941.png)

5. Click on **Save**.
