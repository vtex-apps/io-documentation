---
title: Setting up Google Analytics
description: "Set up all the necessary tags, triggers, variables and configurations to Google Tag Manager and Google Analytics and easily manage user and website data."
date: "19/08/2019"
tags: ["google", "analytics", "store", "google-tag-manager", "gtm", "google-analytics"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/edit/master/docs/en/Recipes/store/setting-up-google-analytics.md"
---

# Setting up Google Analytics

This guide provides instructions to setup all the necessary tags, triggers, variables and configurations to your store's Google Tag Manager and Google Analytics. At the end of it you will have all store analytics available in your Google Analytics dashboard, allowing you to properly manager user and website traffic data. 

To start off, open the Google Tag Manager dashboard at [tagmanager.google.com](https://tagmanager.google.com/).

## Creating variables

To create a variable, click on **Variables** on the menu on the left and then on the button **New**.

### Data Layer Variables

1. Click on **Variable Configuration**.
2. Select **Data Layer Variable**. 
3. Type `campaignMedium` in the `Data Layer Variable Name` field.
4. Click on **Save** and save as **Data Layer Variable - campaignMedium**.

Do the same thing for the following variables: 

- `campaignName`
- `campaignSource`
- `currency`
- `transactionId`
- `transactionTotal`

### Google Analytics Variables

#### Default

1. Click on **Variable Configuration**.
2. Select **Google Analytics Settings**.
3. Type your **Tracking ID**. 
4. Click on **Ecommerce** and then on **Enable Enhanced Ecommerce Features**.
5. Click on **Use data layer**.
7. **Save** your changes as **Google Analytics**.

#### Checkout

1. Click on **Variable Configuration**.
2. Select **Google Analytics Settings**.
3. Type your **Tracking ID**.
4. Click in **More Settings**.
5. Click on **Fields to Set**.
6. Add the following fields:

|  Field Name     |                 Value                    |   
|-----------------|------------------------------------------| 
|  `campaingName`   | {{Data Layer Variable - campaignName}}   |
|  `campaignMedium` | {{Data Layer Variable - campaignMedium}} |
|  `campaignSource` | {{Data Layer Variable - campaignSource}} |

7. Click on **More Settings** and then on **Ecommerce**.
8. Select **Enable Enhanced Ecommerce Features**.
9. Click on **Use data layer**.
10. **Save** your changes as **Google Analytics - Checkout and Order Placed**.


## Creating triggers

To create a trigger, click on **Trigger** on the menu on the left and then on the button **New**.

### Custom Events

1. Click in **Trigger Configuration**
2. Choose **Custom Event**
3. Type `addToCart` in Event Name
4. Click Save, and save as `Custom Event - addToCart`

Repeat the previous steps creating the following triggers for the events: 
- `cart 
- `email`
- `orderPlaced` 
- `payment`
- `productDetail`
- `productImpression` 
- `profile`
– `remoFromCart`
- shipping

## Creating Tags

To create a Tag, click on **Tags** on the left menu and then on the **New** button.

### Google Analytics - Checkout and Order Placed

1. Click on **Tag Configuration**.
2. Select **Google Analytics - Universal Analytics**.
3. Choose **Track Type** as Event.
4. Type **Ecommerce** in `Category`.
5. Type **Event** in `Action`.
6. In `Google Analytics Settings`, choose **Google Analytics - Checkout and Order Placed**.
7. Choose the following triggers: 
  - Custom Event - `cart`
  - Custom Event - `email`
  - Custom Event - `orderPlaced`
  - Custom Event - `payment`
  - Custom Event - `profile`
  - Custom Event - `shipping`
8. Save as **Google Analytics - Checkout and Order Placed**.

### Google Analytics - Enhanced Ecommerce

1. Click on **Tag Configuration**.
2. Select **Google Analytics - Universal Analytics**.
3. Choose **Track Type** as Event.
4. Type **Ecommerce** in `Category`.
5. Type **Event** in `Action`.
6. In G`oogle Analytics Settings`, choose **Google Analytics**
7. Choose the following triggers:
  - Custom Event - `addToCart`
  - Custom Event - `productDetail`
  - Custom Event - `productImpression`
  - Custom Event - `removeFromCart`
8. Save as **Google Analytics - Enhanced Ecommerce**.

### Google Analytics - Page View

1. Click on **Tag Configuration**.
2. Select **Google Analytics - Universal Analytics**.
3. Choose **Page View** as Track Type. 
4. In `Google Analytics Settings`, choose **Google Analytics**.
5. Choose the `All Pages` trigger.
6. Save as **Google Analytics - Page View**.

### Conversion Linker

1. Click on **Tag Configuration**.
2. Select **Conversion Linker**.
3. Choose the `All Pages` trigger.
4. Save as **Conversion Linker**.

### Google Ads Conversion Tracking

1. Click on **Tag Configuration**.
2. Choose **Google Ads Conversion Tracking**.
3. Fill in the fields `Conversion ID` and `Conversion Label` as instructed in the Google Ads panel.
4. Fill in the other fields with Data Layer variables:
  - `Conversion Value`: {{Data Layer Variable - transactionTotal}}
  - `Order ID`: {{Data Layer Variable - transactionId}}
  - `Currency Code`: {{Data Layer Variable - currency}}
5. Save as **Google Ads Conversion Tracking**.
