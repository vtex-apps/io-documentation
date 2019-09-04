---
title: Using Google Tag Manager
description: "This recipe will explain how to start using Google Tag Manager on your store, clarify current restrictions and how to overcome them."
date: "19/08/2019"
tags: ["google", "tag", "manager", "store", "googletagmanager", "gtm"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/using-google-tag-manager.md"
---

# Using Google Tag Manager

## Introduction 

This recipe will explain how to start using Google Tag Manager on your store, clarify current restrictions and how to overcome them.


## Installing GTM app

### Through the VTEX APP Store
1. Enter on the app page on VTEX App Store  https://apps.vtex.com/google-tag-manager/p  
2. Click on the button "Get" to install the app for free  
3. Type your account name and click on the confirmation button  
4. If not logged-in in your account yet, proceed with login
5. Click on "Install" button
6. You'll see a warning message, indicating to enter the needed configurations. Scroll down your page, and type your GTM ID in the proper field.
7. Click on the "Save" button. You are good to go! To check or change configurations of your app, visit the Apps page in VTEX admin portal of your store, click on the GTM app that is already installed and make the necessary changes.

### Through VTEX toolbelt cli
1. Login into your account 
```
vtex login myaccount
```
2. Go to the desired account and workspace 
```
vtex switch {{your_acount}}
vtex use {{your_workspace}}
```
3. Check that the app is not installed yet typing 
```
vtex ls
```
4. Install the desired app 
```
vtex install vtex.google-tag-manager@2.x
```
3. Check that the app is now installed typing 
```
vtex ls
```
5. Visit the Apps page in VTEX admin portal of your store, click on the GTM app that is already installed and type your GTM ID in the indicated field.
6. Click on the **Save** button, and you are good to go!

After installing the app you can use your GTM as usual by accessing your dashboard at [Google Tag Manager](https://tagmanager.google.com/). 

## Current integrated events

VTEX IO's Google Tag Manager solution is compliant with the Universal Analytics Enhanced Ecommerce events format. See reference here: [Enhanced Ecommerce](https://developers.google.com/tag-manager/enhanced-ecommerce) 

Currently we support the following events:
- Product Impression
- Product Click
- Product Detail Impression
- Add / Remove from Cart
- Checkout
- Purchase

These events are already natively emitted by our native components. 

In order to set the tracking of these events on Google Analytics - and much more - check this recipe: [Using Google Analytics](https://vtex.io/docs/recipes/store/googleAnalytics)

## Restrictions

In order to prevent performance problems and unexpected behavior, our VTEX IO Google Tag Manager solution uses the native GTM feature of blacklist. You can read more about this feature in the [Google Developer Guide](https://developers.google.com/tag-manager/devguide).

We currently blacklist the id html, which automatically blacklists all the tags, variables and triggers from the type customScripts. Tags, variables and triggers from all the other types work as usual. The main effect of this blacklist is that Custom HTML tags will NOT be triggered. 

>**Important note:**  The html blacklist is the VTEX GTM solution's default and only possible setting. It is not currently possible to opt-out this blacklist. 

You may check below the full list of tags and variables that are blocked in VTEX IO Google Tag Manager solution:

### Blocked Tags:
- Custom HTML Tag - html
- Eulerian Analytics Tag - ela
- SaleCycle JavaScript Tag  - scjs
- Upsellit Global Footer Tag - uslt
- Upsellit Confirmation Tag - uspt

### Blocked Variables:
- Custom JavaScript Variable - jsm

You can see a list with all the GTM available tags on the [Google Developer Guide](https://developers.google.com/tag-manager/devguide).


## What do I do with my Custom HTML tags?

Most of the Custom HTML tags that are largely used, are integrations with third party services, like Customer Chat, Analytics, Remarketing and Pixel tags. If your Custom HTML fit in one of those cases, this should be transformed into a VTEX IO App.
