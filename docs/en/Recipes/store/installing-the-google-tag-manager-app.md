---
title: Installing the Google Tag Manager app
description: "Start using Google Tag Manager app in your VTEX store to easily track your data through Google Analytics."
date: "05/09/2019"
tags: ["google", "tag", "manager", "store", "google-tag-manager", "gtm"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/installing-the-google-tag-manager-app.md"
---

# Installing the Google Tag Manager app

## Introduction 

Google Tag Manager is a **JavaScript and HTML tag management system** for tracking user browsing. It avoids any contact with the source code when adding, editing or removing website tags and easily provides user browsing tracking for Google Analytics as well.  

The VTEX IO Google Tag Manager native solution is compliant with Universal Analytics [Enhanced Ecommerce](https://developers.google.com/tag-manager/enhanced-ecommerce) events format and natively supports the following events emitted by our components:

- Product Impression
- Product Click
- Product Detail Impression
- Add / Remove from Cart
- Checkout
- Purchase

<div class="alert alert-info">
In order to set the tracking of these events in Google Analytics, learn how to<a href="https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/setting-up-google-analytics.md">set up Google Analytics</a> in your store.
</div>

## Step by step

It is possible to install the GTM app in your store, either by using App Store or the VTEX IO Toolbelt.

### Through VTEX App Store

1. Access the [Google Tag Manager app](https://apps.vtex.com/google-tag-manager/p) in your **VTEX App Store** and install it. 
2. Follow all account login steps and click on the **Install** button.
3. You'll see a warning message about needing to enter the necessary configurations. Scroll down and type in your **GTM ID** in the `Google Tag Manager` field.
4. Click on **Save**. 

To check or update the app's settings afterwards, simply visit the **Apps** section in your account's admin and select the Google Tag Manager box. 

### Using VTEX IO Toolbelt

1. Using your terminal, **login** to your account.

```
vtex login {account}
```

2. Access the account's desired **workspace**.

```
vtex use {workspace}
```

You can confirm whether or not the GTM app is installed by running `vtex ls`. 

3. **Install** the GTM app.

```
vtex install vtex.google-tag-manager@2.x
```

You can confirm that the app has now been installed by running `vtex ls` again. 

4. Access the **Apps** section within your account's admin page and click on Google Tag Manager box.
5. Fill in the `Google Tag Manager` field with your **GTM ID**. 
6. Click on **Save**.

<div class="alert alert-info">
Acess<a href="https://tagmanager.google.com/"> Google Tag Manager page</a> and login to you account in order to find out what is your account <strong>GTM ID</strong>. The number your should use is the one provided by the table 3rd column. 
</div>

After installing the Google Tag Manager app, you are ready to use your GTM as usual by accessing your account dashboard [Google Tag Manager](https://tagmanager.google.com/). 

## Restrictions
In order to avoid performance problems and unforeseen behavior, our VTEX IO Google Tag Manager solution uses the native GTM **blacklist** feature. You can read more about this feature in the [Google Developer Guide](https://developers.google.com/tag-manager/devguide).

We currently blacklist the `HTML` ID, which automatically blacklists all the tags, variables and triggers of the type `customScripts`. The main consequence of this blacklist is that **Custom HTML tags will not be triggered**. 

<div class="alert alert-warning">
The HTML blacklist is VTEX GTM's default and only possible setting. At present, it is not possible to disable it.
</div>

Most of the widely used Custom HTML tags are integrations with third party services, like Customer Chat, Analytics, Remarketing and Pixel tags. If your Custom HTML fits in one of those cases, it should be transformed into a VTEX IO App. If one does not yet exist, you can request its creation on the VTEX IO [Store Discussion](https://github.com/vtex-apps/store-discussion) board.

Check the full list of tags and variables that are blocked in VTEX IO Google Tag Manager solution below:

### Blocked Tags:

- Custom HTML Tag - `html`
- Eulerian Analytics Tag - `ela`
- SaleCycle JavaScript Tag  - `scjs`
- Upsellit Global Footer Tag - `uslt`
- Upsellit Confirmation Tag - `uspt`

### Blocked Variables:

- Custom JavaScript Variable - `jsm`
See a list with all the GTM available tags in the [Google Developer Guide](https://developers.google.com/tag-manager/devguide).

