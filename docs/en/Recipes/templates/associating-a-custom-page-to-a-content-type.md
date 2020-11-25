---
title: Associating a custom page to a content type
description: "Learn how to have your custom landing page tied to an id instead of a URL."
date: "2020-11-25"
tags: ["custom", "content type", "landing", "page"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/edit/master/docs/en/Recipes/templates/associating-a-custom-page-to-a-content-type.md"
---

# Associating a custom page to a content type

In general, the assets of a [custom landing page](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-creating-a-new-custom-page) are tied to the URL. However, in some situations, you may want to have the page content tied to an id instead of a URL.

For example, you may want to relate an identifier of the cities where your store is located to a *Store Finder* page.

For that, it's possible to benefit from *content types* and use them as variables in your route path.

This way, the assets of the page will be related to the id values of that *content type.* 

Take the following example: imagine you created a page in *Store Setup > CMS > Pages* with the following URL `/store/:store_id`. A few days have passed and you decided to change the `/store/:store_id` URL to `/store-finder/:store_id`. Notice that this wouldn't be a problem and the assets previously related to `/store/:store_id` would be available in `/store-finder/:store_id` since, in this example, the page content is tied to a content type and not a URL.

For implementation details, check the following sections.

## Guidelines

To associate the assets of a [custom landing page](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-creating-a-new-custom-page) to an id, you must note the following when creating the URL:

1. The URL recognizes any param named `{entity}_id` as a *content type* (e.g., `${entity}`).

>⚠️ *Notice that, for the URL definition, adding the name of the content type is not enough. You must also attach `_id` in the sequence.*

>⚠️ *If you create a URL such as `/foo/:bar`, the content will be tied to that URL, since there's no param capable of being interpreted as a content type. Thus, if, for example, you access *Store Setup > CMS > Site Editor* and look for  `/foo/skywalker`, the content related to `/foo/:bar` won't be displayed.*

2. The page URL can have only one parameter containing a content type.
3. The page URL can have only one parameter ending with `_id`.
4. If there are other variable parameters in the URL, they are ignored when matching content. For example, if you create the route `/foo/:bar/:{entity}_id`, the same content will be delivered for `/foo/skywalker/1` and `/foo/palpatine/1` since the content will be tied to the `{$entity}` content type.
