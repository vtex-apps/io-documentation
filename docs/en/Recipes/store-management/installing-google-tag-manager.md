---
title: Installing Google Tag Manager
description: "Install the Google Tag Manager app, a first party integration to manage your stores variables, tags and triggers."
date: "01/02/2022"
tags: ["google-analytics", "store", "google-tag-manager", "gtm", "tags", "variables", "triggers"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store-management/installing-google-tag-manager.md"
---

# Installing Google Tag Manager

## Before you start

You need a Google account to use Google Tag Manager. If you already use Google products, such as Gmail, you can use the same account.

If you do not have an account for a Google product, create one at [Creating your Google account](https://accounts.google.com/signup/v2/webcreateaccount?service=analytics&continue=https%3A%2F%2Ftagmanager.google.com%2F&dsh=S1158101756%3A1642078409369040&biz=true&flowName=GlifWebSignIn&flowEntry=SignUp&nogm=true). 

> ⚠️
> 
> If you install a new version of the Google Tag Manager (GTM) app, the VTEX environment deletes the previous GTM data stored. Therefore, if you already have a GTM version installed in your account, review the data that you have added before installing a new version of the app.

## Step-by-step

1. Access your VTEX **Admin** and go to **Account settings > Apps > App Store**
2. Search for the Google Tag Manager app and click on `Install`. You will be redirected to the [App Store page](https://apps.vtex.com/vtex-google-tag-manager/p) and login into your App Store account if you are not already logged in.
![image2](https://user-images.githubusercontent.com/67270558/151416637-46d44cb0-c1a2-4b56-8116-778c2c0ce8b3.gif)

3. After you will be redirected to the [App Store landing page](https://apps.vtex.com/), and in the search field, type `Google Tag Manager`, click on the app, then on  `GET APP`.
4. On the checkout page, click on *check out the Google Tag Manager terms and conditions*, and if you agree, click on `PLACE ORDER`.

> ℹ️ Info
>
> The GTM is a free app.

5. You’ll see a success message about the purchase and click on `GO TO INSTALL PAGE`, which will redirect you to the GTM setup page.
6. You'll see a warning message about needing to enter the necessary configurations. Scroll down and type your **GTM ID** in the Google Tag Manager field.
7. Click on Save.


> ℹ Info
>
> To find your store’s **GTM ID**, first, you need a container to the Tag Manager account. If you do not have one follow the [create a new account and container tutorial](https://support.google.com/tagmanager/answer/6103696?hl=en#install) and after find the GTM ID in The `Container ID` column of the container.

Once you have installed the app, go to [Setting up Google Tag Manager documentation](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-setting-up-google-tag-manager) and learn how to set up the variables, triggers, and tags necessaries for the app to work.



## Restrictions
In order to avoid performance problems and unforeseen behavior, the VTEX IO Google Tag Manager solution uses the native GTM blacklist feature. You can read more about this feature on the [Google Developer Guide](https://developers.google.com/tag-platform/tag-manager/web/restrict).
By default, the HTML ID is blocked, which automatically blocklists all the tags, variables, and triggers of the type `customScripts`. The main consequence of this blocklist is that Custom HTML tags will not be triggered.
**The HTML blacklist is a VTEX Google Tag Manager app's default.** If you want to disable this restriction go to https://{accountName}.myvtex.com/admin/apps/vtex.google-tag-manager@3.x/setup and check the toggle below.

![restrictions](https://user-images.githubusercontent.com/67270558/149350479-42dd3fbd-c727-4181-9c84-b76da0873d2f.png)


Most of the widely used Custom HTML tags are integrations with third-party services, like Customer Chat, Analytics, Remarketing, and Pixel tags. If your store needs a Custom HTML for one of those cases, the integration can either be done by transforming the tags into a [VTEX IO Pixel App](https://developers.vtex.com/vtex-developer-docs/docs/pixel-apps) or by removing this restriction.
Check out below the full list of tags and variables that are blocked, by default, in VTEX IO Google Tag Manager solution below:

**Blocked tags**
- Custom HTML Tag - html
- Eulerian Analytics Tag - ela
- SaleCycle JavaScript Tag - scjs
- Upsellit Global Footer Tag - uslt
- Upsellit Confirmation Tag - uspt

**Blocked variables**
- Custom JavaScript Variable - jsm

Check out a list with all the GTM available tags on [the Google Developer Guide](https://developers.google.com/tag-platform/tag-manager/web/datalayer).

## Next Step

- [Setting up Google Tag Manager documentation](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-setting-up-google-tag-manager)
