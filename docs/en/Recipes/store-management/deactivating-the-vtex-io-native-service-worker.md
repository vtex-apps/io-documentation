---
title: Deactivating the VTEX IO native service worker
description: "Choose to deactivate the native service worker provided by VTEX IO in order to successfully use a third party solution in your store."
date: "2020-07-16"
tags: ["service-worker", "pwa", "deactivate", "deactivating"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store-management/deactivating-the-vtex-io-native-service-worker.md"
---

# Deactivating the VTEX IO native service worker

The VTEX IO platform provides a **native [service worker](https://developers.google.com/web/fundamentals/primers/service-workers)** to every store using VTEX Store Framework. 

This is due to the fact that all VTEX Store Framework stores natively benefit from having a **PWA** at their disposal. 

A PWA is a sort of web app used to promote certain advantageous features to users, such as offline navigation or a home screen icon. Once enabled in a store, the PWA uses the VTEX IO necessarily service worker in order to function. 

As a result of this native usage, you may face a conflict when working with a third party service responsible for providing its own service worker to operate. 
Since a website can only have one service worker running, you can **choose to deactivate the native service worker provided by VTEX IO in order to successfully use a third party solution in your store**. 

## Step by step

1. Access your account's admin.
2. Access CMS and then Store.
3. Click on the Advanced tab.
4. Toggle the Service Worker button.

![service-worker-toggle-recipe](https://user-images.githubusercontent.com/52087100/87695658-233ccc00-c766-11ea-9615-7cab9045f62d.png)

5.  Save changes.

>ℹ️ Notice that the toggle button can activate and deactivate the VTEX IO native service worker. Therefore, use the step by step above to manage it according to your store's needs.

Once you save the changes, the VTEX Service Worker will be automatically disabled.
