---
title: Setting up Google Analytics
description: "This guide provides instructions to setup all the necessary Tags, Triggers, Variables, and configurations to Google Tag Manager and Google Analytics, so at the end of it you will have all the user and ecommerce analytics available in your Google Analytics dashboard."
date: "19/08/2019"
tags: ["google", "analytics", "store", "googletagmanager", "gtm"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/googleTagManager.md"
---

# Setting up Google Analytics

This guide provides instructions to setup all the necessary Tags, Triggers, Variables, and configurations to Google Tag Manager and Google Analytics, so at the end of it you will have all the user and ecommerce analytics available in your Google Analytics dashboard.

## Google Tag Manager Setup

Open the Google Tag Manager dashboard at [tagmanager.google.com](https://tagmanager.google.com/).

## Creating variables

To create a Variable, click on **Variables** on the menu on the left and then on the button **New**.

## Data Layer Variables

1. Click in Variable Configuration
2. Choose "Data Layer Variable"
3. Type "campaignMedium" in "Data Layer Variable Name"
4. Click Save, and save as "Data Layer Variable - campaignMedium"

Do the same thing for the variables: 
- **campaignName**
- **campaignSource**
- **currency**
- **transactionId**
- **transactionTotal**

## Google Analytics Variables

### Default

1. Click in **Variable Configuration**
2. Choose **Google Analytics Settings**
3. Type your `Tracking ID`
4. Click in **Ecommerce**
5. Click in **Enable Enhanced Ecommerce Features**
6. Click in **Use data layer**
7. Click **Save**, and save as **Google Analytics** 

### Checkout

1. Click in **Variable Configuration**
2. Choose **Google Analytics Settings**
3. Type your **Tracking ID**
4. Click in **More Settings**
5. Click in **Fields to Set**
6. Add the fields:

|  Field Name     |                 Value                    |   
|-----------------|------------------------------------------| 
|  campaingName   | {{Data Layer Variable - campaignName}}   |
|  campaignMedium | {{Data Layer Variable - campaignMedium}} |
|  campaignSource | {{Data Layer Variable - campaignSource}} |

7. Click in **More Settings**
8. Click in **Ecommerce**
9. Click in **Enable Enhanced Ecommerce Features**
10. Click in **Use data layer**
11. Click **Save**, and save as `Google Analytics - Checkout and Order Placed`


## Creating Triggers

To create a Trigger, click on **Trigger** on the menu on the left and then on the button **New**.

### Custom Events

1. Click in **Trigger Configuration**
2. Choose **Custom Event**
3. Type `addToCart` in Event Name
4. Click Save, and save as `Custom Event - addToCart`

Repeat the previous steps creating new Triggers for the events: 
- cart 
- email
- orderPlaced 
- payment
- productDetail
- productImpression 
- profile
– remoFromCart
- shipping

## Creating Tags

To create a Tag, click on **Tags** on the menu on the left and then on the button **New**.

### Google Analytics - Checkout and Order Placed

1. Click in **Tag Configuration**
2. Choose **Google Analytics - Universal Analytics**
3. Choose Track Type as **Event**
4. Type `Ecommerce` in Category
5. Type `Event` in Action
6. In Google Analytics Settings choose `Google Analytics - Checkout and Order Placed`
7. Choose the Triggers: 
  - Custom Event - cart
  - Custom Event - email
  - Custom Event - orderPlaced
  - Custom Event - payment
  - Custom Event - profile
  - Custom Event - shipping
10. Save as `Google Analytics - Checkout and Order Placed`

### Google Analytics - Enhanced Ecommerce

1. Click in **Tag Configuration**
2. Choose **Google Analytics - Universal Analytics**
3. Choose **Track Type** as **Event**
4. Type **Ecommerce** in **Category**
5. Type **Event** in **Action**
6. In Google Analytics Settings choose **Google Analytics**
7. Choose the Triggers:
  - Custom Event - addToCart
  - Custom Event - productDetail
  - Custom Event - productImpression
  - Custom Event - removeFromCart
8. Save as `Google Analytics - Enhanced Ecommerce`

### Google Analytics - Page View

1. Click in **Tag Configuration**
2. Choose **Google Analytics - Universal Analytics**
3. Choose Track Type as **Page View**
4. In Google Analytics Settings choose **Google Analytics**
5. Choose the Triggers:
  - All Pages
6. Save as **Google Analytics - Page View**

### Conversion Linker

1. Click in Tag Configuration
2. Choose **Conversion Linker**
3. Choose the Triggers:
  - All Pages
4. Save as **Conversion Linker**

### Google Ads Conversion Tracking

1. Click in Tag Configuration
2. Choose "Google Ads Conversion Tracking"
3. Fill the fields "Conversion ID" and "Conversion Label" as instructed in the Google Ads panel.
4. Fill the other fields with Data Layer variables:
  - Conversion Value": **{{Data Layer Variable - transactionTotal}}**
  - Order ID: **{{Data Layer Variable - transactionId}}**
  - Currency Code*: **{{Data Layer Variable - currency}}**
5. Save as `Google Ads Conversion Tracking`
