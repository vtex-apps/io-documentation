---
title: Setting up Google Tag Manager
description: "Set up all the necessary tags, triggers, variables and configurations with Google Tag Manager and easily manage user and website data using Google Analytics dashboards."
date: "19/08/2019"
tags: ["google-analytics", "store", "google-tag-manager", "gtm", "tags", "variables", "triggers"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/setting-up-google-tag-manager.md"
---

# Setting up Google Tag Manager

[Google Tag Manager](https://tagmanager.google.com/) is a **JavaScript and HTML tag management system** provided by Google for tracking user browsing.

With the [**VTEX IO Google Tag Manager Pixel App**](https://developers.vtex.com/vtex-developer-docs/docs/vtex-google-tag-manager), you can avoid any contact with the store's source code when adding, editing or removing these website tags and easily provide user browsing tracking for Google Analytics as well.  

The VTEX IO Google Tag Manager native solution is compliant with Universal Analytics [Enhanced Ecommerce](https://developers.google.com/tag-manager/enhanced-ecommerce) events format and natively supports the following events emitted by our components:

- Product Impression;
- Product Click;
- Product Detail Impression;
- Add/Remove from Cart;
- Promotion Impression;
- Promotion Click;
- Checkout;
- Purchase.

>ℹ️ In order to set the tracking of these events in Google Analytics, learn how to <a href="https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-setting-up-google-analytics-search-tracking/">set up Google Analytics search tracking</a> in your VTEX IO store.

In order to set up Google Tag Manager in your store, you first must set up all necessary **variables**, **triggers** and **tags**. 

These GTM components will work together to measure your store's data, allowing you to properly manage user and website traffic in your Google Analytics dashboard. 

>ℹ️ If you are not familiar with the GTM components, we strongly recommend you to access the <a href="https://support.google.com/tagmanager/answer/6103657?hl=en">Google Tag Manager documentation</a> before starting your setup.

Follow the steps below to create all necessary GTM components for your store. Begin by installing the [Google Tag Manager Pixel App](https://developers.vtex.com/vtex-developer-docs/docs/vtex-google-tag-manager) and opening your Google Tag Manager account dashboard at [tagmanager.google.com](https://tagmanager.google.com/).

## Step by step

### Creating variables

To create a variable, click on **Variables** in the left menu and then on **New**:

![GTM-variables-menu](https://user-images.githubusercontent.com/52087100/64815325-ae17cd80-d57b-11e9-90fb-ff13e4026e72.png)

#### Data Layer Variables

1. In the **User-Defined Variables** box, click on **New**;
2. Click on the **Variable Configuration** box and select **Data Layer Variable**;
3. Type `campaignMedium` in the `Data Layer Variable Name` field;
4. Click on **Save** and save it as **Data Layer Variable - campaignMedium**.

Repeat the instructions above, now changing the Data Layer Variable name for each of the following variables: 

- `campaignName`
- `campaignSource`
- `currency`
- `transactionId`
- `transactionTotal`
- `userId`

#### Google Analytics Variables

- **Default:**

1. In the **User-Defined Variables** box, click on **New**;
2. Click on the **Variable Configuration** box and select **Google Analytics Settings**; 
3. Type in your Google Analytics **Tracking ID**;
4. Click on **More Settings** and then on **Ecommerce**;
5. Tick the **Enable Enhanced Ecommerce Features** and **Use data layer** boxes;
6. **Save** your changes as **Google Analytics**.

If you intend to use the [User ID feature of Google Analytics](https://support.google.com/analytics/answer/3123662), you need to set a field using the `userId` variable previously created. 

For this, click on **Fields to Set**, and then add the field `userId` with its desired value.

- **For the store's checkout:**

1. In the **User-Defined Variables** box, click on **New**;
2. Click on the **Variable Configuration** box and select **Google Analytics Settings**;
3. Type in your Google Analytics **Tracking ID**;
4. Click on **More Settings** and then **Fields to Set**.
5. **Add** then the following fields:

|  Field name     |                 Value                    |   
|-----------------|------------------------------------------| 
|  `campaignName`   | {Data Layer Variable - campaignName}   |
|  `campaignMedium` | {Data Layer Variable - campaignMedium} |
|  `campaignSource` | {Data Layer Variable - campaignSource} |

>⚠️ Remember to replace the values between the curly brackets according to your scenario.

6. Then, click on **Ecommerce** and check the **Enable Enhanced Ecommerce Features** and **Use data layer** boxes;
7. **Save** your changes as **Google Analytics - Checkout and Order Placed**.

### Creating triggers

To create a trigger, click on **Trigger** in the left menu and then on **New**:

![GTM-triggers-menu](https://user-images.githubusercontent.com/52087100/64815364-c7207e80-d57b-11e9-8d7a-5f2634c7bdb7.png)

#### Custom Events

1. Click on the **Trigger Configuration** box;
2. Select **Custom Event**;
3. Type `addToCart` in the `Event Name` field;
4. Click on **Save** and save it as `Custom Event - addToCart`.

Repeat the instructions above, now changing the event name for each of the following event triggers:

- `cart`
- `email`
- `orderPlaced`
- `payment`
- `productClick`
- `productDetail`
- `productImpression`
- `promotionClick`
- `promoView`
- `profile`
- `removeFromCart`
- `shipping`
- `pageView`

### Creating Tags

To create a tag, click on **Tags** in the left menu and then on **New**:

![GTM-tags-menu](https://user-images.githubusercontent.com/52087100/64815399-e28b8980-d57b-11e9-8913-1c0dc05f96a0.png)

#### Google Analytics - Checkout and Order Placed

1. Click on the **Tag Configuration** box;
2. Select **Google Analytics - Universal Analytics**;
3. Choose **Event** from the `Track Type` field;
4. Type in **Ecommerce** in the `Category` field;
5. Type in **Event** in the `Action` field;
6. In `Google Analytics Settings`, select **Google Analytics - Checkout**;
7. In the **Triggering** box, choose the following triggers: 
  - Custom Event - `cart`
  - Custom Event - `email`
  - Custom Event - `orderPlaced`
  - Custom Event - `payment`
  - Custom Event - `profile`
  - Custom Event - `shipping`
8. Save the new tag as **Google Analytics - Checkout and Order Placed**.

#### Google Analytics - Enhanced Ecommerce - No Interaction

1. Click on the **Tag Configuration** box;
2. Select **Google Analytics - Universal Analytics**;
3. Choose **Event** from the `Track Type` field;
4. Type in **Ecommerce** in the `Category` field;
5. Type in **Event** in the `Action` field;
6. Select **True** in the `Non-Interaction Hit` field;
7. In `Google Analytics Settings`, choose **Google Analytics**; 
8. In the **Triggering** box, choose the following triggers:
  - Custom Event - `productDetail`
  - Custom Event - `productImpression`
  - Custom Event - `promoView`
9. Save the new tag as **Google Analytics - Enhanced Ecommerce - No Interaction**.

#### Google Analytics - Enhanced Ecommerce - Yes Interaction

1. Click on the **Tag Configuration** box;
2. Select **Google Analytics - Universal Analytics**;
3. Choose **Event** from the `Track Type` field;
4. Type in **Ecommerce** in the `Category` field;
5. Type in **Event** in the `Action` field;
6. Select **False** in the `Non-Interaction Hit` field;
7. Choose **Google Analytics** in the `Google Analytics Settings` field; 
7. In the **Triggering** box, choose the following triggers:
  - Custom Event - `addToCart`
  - Custom Event - `removeFromCart`
  - Custom Event - `productClick`
  - Custom Event - `promotionClick`
8. Save the new tag as **Google Analytics - Enhanced Ecommerce - Yes Interaction**.

#### Google Analytics - Page View

1. Click on the **Tag Configuration** box; 
2. Select **Google Analytics - Universal Analytics**;
3. Choose **Page View** from the `Track Type` field;
4. In `Google Analytics Settings`, select **Google Analytics**;
5. In the **Triggering** box, select the `Custom Event - pageView` trigger;
6. Save the new tag as **Google Analytics - Page View**.

#### Conversion Linker

1. Click on the **Tag Configuration** box;
2. Select **Conversion Linker**;
3. In the **Triggering** box, choose the `All Pages` trigger;
4. Save the new tag as **Conversion Linker**.

#### Google Ads Conversion Tracking

1. Click on the **Tag Configuration** box;
2. Choose **Google Ads Conversion Tracking**;
3. Fill in the fields `Conversion ID` and `Conversion Label` according to what is instructed by the Google Ads panel;
4. Fill in the following fields with Data Layer variables:
  - `Conversion Value`: {Data Layer Variable - transactionTotal}
  - `Order ID`: {Data Layer Variable - transactionId}
  - `Currency Code`: {Data Layer Variable - currency}
  
>⚠️ Remember to replace the values between the curly brackets according to your scenario.

5. In the **Triggering** box, choose the `All Pages` trigger;
6. Save the new tag as **Google Ads Conversion Tracking**.
