---
title: Understanding how store URL indexing works
description: "Understand how VTEX IO indexes your store's URLs."
date: "2020-04-08"
tags: ["indexing", "url", "seo", "canonical", "most-visited"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/new-docs/docs/en/Recipes/store-management/understanding-how-store-url-indexing-works.md"
---

# Understanding how store URL indexing works

## Introduction

In order to be accessed by any type of user, all website pages need to have their own addresses, called **URLs**.

It is however possible for a page to have more than one address format, thereby allowing users to access it from different URLs, such as `www.storetheme.com.br` and `storetheme.com.br` .

The two URLs in the example above are distinct and therefore indexed separately by search engines - even if they direct to the same page.

To solve this issue, **each website URL needs its canonical URL**, which is nothing more than the official URL - not necessarily identical - that will be given to search engines and indexed, thereby improving the site's overall content findability.
  
## URL indexing requisites

**In VTEX IO, all store canonical URLs (product, category, subcategory, brand and custom page URLs) are automatically held in Sitemap where they are indexed by search engines.** 

As the name suggests, Sitemap is simply the mapping tool for all canonical URLs, and displays your site's architecture to search bots and user browsers.

To ensure that every relevant URL from your site has been indexed, VTEX IO also identifies the **most visited search URLs** and transforms these into canonical URLs that are then added to Sitemap.

### Most visited search URLs 

To define the most visited search URLs, the platform calculates how many users already visited each of these site addresses, as long as the site is online.

By default, a URL needs to have been accessed at least **once** to enter the list of most visited site addresses.

The algorithm that calculates the accesses to each of these URLs in order to add them to the list of most visited addresses takes the following criteria into account:

- Any type of access is valid, including those stemming from workspaces or from the `myvtex.com.br` domain;
- URLs that are accessed from results returned by the store's search bar are not taken into account.

Once on the most visited list, URLs get their own canonical URL and are then added to Sitemap, where they're indexed by search engines.

A URL can be removed from the Sitemap listing and no longer be indexed if:

- It returns a status code `404`;
- It lost its relevance (is no longer accessed) and, consequently, fell off the list of most visited site URLs.

>ℹ️ Note: URLs that will are removed from the Sitemap list and are no longer indexed by search engines will still continue to work normally for site users. 

#### Managing the most visited search URLs list

It's not possible to control which search URLs will enter the most visited list, since this is based on user activity.

What you can do is **control the max number of most visited URLs that your site will index**, by following the instructions below:

1. Log in to the admin of the desired VTEX account; 
2. Access the Apps section, located in the admin side bar;
3. Select the Store Indexer;
4. In the Setup section, fill out the following field with the desired value `Number of search URLs to be indexed`;

![store-indexer](https://user-images.githubusercontent.com/52087100/78806539-2ec76c80-7999-11ea-81cb-5286e0444410.png)

5. Save the configurations.

The Store Indexer app, which is responsible for indexing your site's main URLs, builds a list of the most visited site URLs according to the frequency with which those pages are accessed and the max number of possible URLs you configured in the above mentioned step-by-step.

The app automatically corrects and uniformizes the listed URLs to create canonical URLs, removing coded values such as  `map=c,c` and `/example?map=specificationFilter_X` from them.

As said previously, these URLs are then added to Sitemap by the Store Indexer and thus get indexed by web search engines.
