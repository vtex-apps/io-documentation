---
title: Associating a custom page to a content type
description: "Learn how to have your custom landing page tied to an id instead of a URL."
date: "2020-11-25"
tags: ["custom", "content type", "landing", "page"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/edit/master/docs/en/Recipes/templates/associating-a-custom-page-to-a-content-type.md"
---

# Associating a custom page to a content type

In general, the assets of [custom landing pages](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-creating-a-new-custom-page) are tied to a store URL. However, in some situations, you may want to have those assets associated with a **content type** instead. Content types indicate the nature of a page. For instance, Product Listing Pages (PLPs) and Product Detail Pages (PDPs) are examples of content types. 

You can create your own content types to manage your website content more easily. For example, you can create a content type named "Store Finder" for the web pages of your site that indicate the cities where your store is located. To associate the assets of these pages with this content type, you need to set up an id value for this content type and use it as a variable in your route paths.

Take the following example: imagine you created a page in *Store Setup > CMS > Pages* with the following URL `/store/:store_id`, where `store_id` represents the `${store}` content type.

A few days have passed and you decided to change the `/store/:store_id` URL to `/store-finder/:store_id`. Because the assets of that page are related to the `${store}` content type and not to a specific URL, the assets previously related to `/store/:store_id` would continue to be available in `/store-finder/:store_id` without any problem.

For implementation details on how to associate a custom page to a content type, check the following sections.

## Step by step

In this step by step, you will learn how to create a content type and customize different pages associated with it via the Admin. As an example, we'll use the `${collection}` content type.

>ℹ️ Content types cannot be used in the `blocks.json` file.

### Step 1 - Creating a new page

1. Access the Admin.
2. Go to **Store Setup > CMS > Pages**.
3. Click on **Create New** to create a new page.
4. Fill in the fields according to your scenario. For the URL input field, check the [URL guidelines section](#URL-guidelines) and set up the route of your page using the desired content type (e.g., `/collection/:collection_id`).
5. Click **Save**.

### Step 2 - Adding the content

For each page that you want to customize based on your new content type, repeat the following steps.

1. Go to **Store Setup > CMS > Site Editor**.
2. In the URL input field, type the full URL of the page you want to customize (e.g., `/collection/summer`).
3. Make the desired changes in the page.
4. Click Save.

## URL guidelines

To associate the assets of a [custom landing page](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-creating-a-new-custom-page) to a content type, you must note the following when creating your page's URL:

- Any parameter named `{entity}_id` is recognized as a content type. For example, `finder_id` creates the `${finder}` content type.

  >⚠️ Notice that, for the URL definition, adding the identifier of the content type is not enough. You must also attach `_id` in the sequence. For example, if you create a URL such as `/foo/:bar`, the content will be tied to that URL since there's no parameter capable of being interpreted as a content type. Thus, if, for example, you access *Store Setup > CMS > Site Editor* and update the content for `/foo/skywalker`, the content related to any page matching `/foo/:bar` will be updated as well.

- The page URL can have only one parameter containing a content type.
- The page URL can have only one parameter ending with `_id`.
- If there are other variable parameters in the URL, they are ignored when matching content. For example, if you create the route `/foo/:bar/:{entity}_id`, the same content will be delivered for `/foo/skywalker/1` and `/foo/palpatine/1` since the content will be tied to the `{$entity}` content type.
