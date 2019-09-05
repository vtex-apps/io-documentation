---
title: Installing the Google Tag Manager app
description: "Start using Google Tag Manager app on your VTEX store to easily track your data through Google Analytics."
date: "05/09/2019"
tags: ["google", "tag", "manager", "store", "google-tag-manager", "gtm"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/setting-up-google-tag-manager.md"
---

# Installing the Google Tag Manager app

## Introduction 

Google Tag Manager is a **JavaScript and HTML tags management system** for tracking user browsing. It avoids any contact with the source code when adding, editing or removing your website tags and provides easily user browsing tracking for Google Analytics as well.  

The VTEX IO's Google Tag Manager native solution is compliant with the Universal Analytics [Enhanced Ecommerce](https://developers.google.com/tag-manager/enhanced-ecommerce) events format and supports the following events natively emitted by our components:

- Product Impression
- Product Click
- Product Detail Impression
- Add / Remove from Cart
- Checkout
- Purchase

<div class="alert alert-info">
In order to set the tracking of these events on Google Analytics, learn how to<a href="https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/setting-up-google-analytics.md"> set up Google Analytics</a> in your store.
</div> 

## Step by step

It is possible to install the GTM app in your store via App Store or using the VTEX IO Toolbelt.

### Through the VTEX App Store

1. Access the [Google Tag Manager app](https://apps.vtex.com/google-tag-manager/p) in your **VTEX App Store** and install it. 
2. Follow all account login steps and click on the **Install** button.
3. You'll see a warning message indicating to enter the needed configurations. Scroll down your page and type your **GTM ID** in the `Google Tag Manager` field.
4. Click on the **Save** button. You are good to go! 

To check or updtate the app's settings posteriormente, simply visit the **Apps** section in your account's admin and select the Google Tag Manager box. 

### Through VTEX IO Toolbelt

1. Using your terminal, **login** to your account.

```
vtex login {account}
```

2. Access the account's desired **workspace**.

```
vtex use {workspace}
```

You can confirm if the GTM app is not installed yet by running `vtex ls`. 

3. **Install** the GTM app.

```
vtex install vtex.google-tag-manager@2.x
```

You can confirm that the app is now installed by running again `vtex ls`. 

4. Access the **Apps** section within your account's admin page and click on Google Tag Manager box.
5. Fill in the `Google Tag Manager` field with your **GTM ID**. 
6. Click on the **Save** button.

After installing the Google Tag Manager app, you are ready to use your GTM as usual by accessing your account's dashboard at [Google Tag Manager](https://tagmanager.google.com/). 

## Restrictions

In order to prevent performance problems and unexpected behavior, our VTEX IO Google Tag Manager solution uses the native GTM feature of **blacklist**. You can read more about this feature in the [Google Developer Guide](https://developers.google.com/tag-manager/devguide).

We currently blacklist the `HTML` ID, which automatically blacklists all the tags, variables and triggers from the type `customScripts`. The main effect of this blacklist is that **Custom HTML tags will not be triggered**. 

<div class="alert alert-warning">
The HTML blacklist is the VTEX GTM solution's default and only possible setting. It is not currently possible to disable it.
</div>

Most of the largely used Custom HTML tags are integrations with third party services, like Customer Chat, Analytics, Remarketing and Pixel tags. If your Custom HTML fit in one of those cases, this should be transformed into a VTEX IO App. If it does not exist yet, you can request its creation on the VTEX IO [Store Discussion]().

Check below the full list of tags and variables that are blocked in VTEX IO Google Tag Manager solution:

### Blocked Tags:

- Custom HTML Tag - `html`
- Eulerian Analytics Tag - `ela`
- SaleCycle JavaScript Tag  - `scjs`
- Upsellit Global Footer Tag - `uslt`
- Upsellit Confirmation Tag - `uspt`

### Blocked Variables:

- Custom JavaScript Variable - `jsm`

See a list with all the GTM available tags on the [Google Developer Guide](https://developers.google.com/tag-manager/devguide).

