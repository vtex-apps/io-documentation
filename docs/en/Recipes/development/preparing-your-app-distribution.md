---
title: Preparing your app for distribution
description: "In this guide, you will learn how to prepare your app for distribution in the VTEX App Store and let merchants benefit from your solution."
date: "2021-03-04"
tags: ["app-store", "app", "distribution"]
version: " "
git: " "
---

# Preparing your app for distribution

In this guide, you will learn how to prepare your app for distribution in the VTEX App Store and let merchants benefit from your solution. 

Before making it available at the VTEX App Store, your app must go through our homologation process. During this process, our review team ensures that your app follows our quality, viability, and usability standards.

## Before you start


1. Have developed your app. You can follow the [Developing an app guide](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-developing-an-app) for more information on this step. 


2. Ensure you are a registered [VTEX App Store developer](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-becoming-a-registered-vtex-app-store-developer).

## Step-by-step
### Step 1 - Preparing your app billing options
After developing your app, you have to establish whether your app will be charged or not and whether it should be private or public in the VTEX IO platform. The VTEX App Store's business models are flexible and, thus, adaptable to different scenarios for marketing your app. Currently, there are two models available:

- Free distribution: offer your app for free, without installation costs for users. 

- Paid distribution: offer your app a fee depending on your app's purpose.


Refer to [Setting your app's billing model](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-setting-your-apps-billing-model) documentation and follow the instructions according to the desired scenario for your app distribution. Also, take a look at the [app monetization guideline](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-business-guidelines-app-monetization) for more information on the topic.

### Step 2 - Setting the `public` folder

Now that you set your app billing model, you can start your app distribution material to the VTEX App Store.The goal is to have a page in the App Store similar to the following after the homologation process:


![appstore-page-example](https://user-images.githubusercontent.com/67270558/153282275-98bab015-81e8-4858-8538-72c9fa33d17e.gif)

> ℹ️
> 
> The homologation process is when our review team ensures that your app follows our quality, viability, and usability standards described in the [App Store Guidelines](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-homologation-requirements-for-vtex-app-store).


1. Create a new folder named `public` in the root directory of your project.

2. Inside the `public` folder, create the `metada` folder and inside it create the folders: `images`, `licenses`, `messages`.

3. Create the following folders and files for the respectives directories.


```
   public
	metadata
		images
			icon.png
			screenshots
				desktop

				mobile
	lincenses
		en-US.md
		es-AR.md
		pt-BR.md
	messages
		en-US.json
		es-AR.json
		pt-BR.json

```


>⚠️ Warning
>
> Ignore this step if your app already have the folder `public/metada`

4. Create the files and folders needed to compose  your app page in the VTEX App Store according to the following:

#### The `images` folder

The Images folder is where you store the images of your app that are displayed in VTEX App Store such as the app’s Icon and Screenshots to show how the application will display in the Admin panel and in the storefront. Inside this folder, you must have:


```

		images
			icon.png 
			screenshots
				desktop
					{add-a-file}.png
					{add-a-file}.png

				mobile
					{add-a-file}.png
					{add-a-file}.png

```

- `icon.png` - It expresses the visual identity and helps reinforce your brand in our enviroment.
- `screenshots` - It contains the app’s screenshots and show the users how the application will behave, either in the Admin panel or in the storefront itself.
- `desktop` - It contains the app’s screenshots for desktop screens.
- `mobile` - It contains the the app’s screenshots for mobile screens.

You can add mobile and desktop screenshots by saving them into sub-folders for each device. For example: `public/metadata/images/screenshots/mobile` and `public/metadata/images/screenshots/desktop`.

Check out the images’ guidelines at the [Marketing Assets guidelines](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-business-guidelines-marketing-assets) for more information.


### The `licenses` folder

The `licenses` folder contains the terms and conditions of your application, which are essential to establish the direct business relationship between you, the developer, and the retailer that installs the app.


️The terms and conditions must be offered in three languages: English, Spanish and Portuguese, and they should be available in the paths `public/metadata/licenses/en-US.md`, `public/metadata/licenses/es-AR.md`, and `public/metadata/licenses/en-BR.md`, respectively.


#### The `messages` folder

The `messages` folder contains information regarding your app, such as its name and list of features, in different languages.
See below the base template for structuring this file:

```
    {
  "name": "Order Tracker",
    "headline": "Headline Order Tracker.",
  "overview": "Tracks all orders\\nSecond line\\n\\nThird line\\n\\n\\n\\n\\nFourth line",
  "features": [
    "First feature",
    "Second feature",
    "Third feature",
    "Fourth feature"
  ],
    "additionalinformation": "Additional information\\nYou can also write new lines here\\n\\n\\nIt should work just like the overview",
  "video": "<https://www.youtube.com/embed/645ASYhJS-Q>",
  "websiteURL": "<https://www.website.com/en>",
  "support": {
      "email": "a@bcd.io"
      "url": "www....",
      "phone": +1....
    },
  "metricDescription": {
    "track": "English description for metric track",
    "notify": "English description for metric notify en-US"
  }
}

```

- **Name:** The name of your application, limited to 26 characters.
- **Headline:** A short description of the main functionality of your application. The field has a 120 character limit.
- **Overview:** A detailed description of your app’s main purposes and benefits. There is no character limit.
- **Feature:** A list of your app’s main features and highlights. 
- **Website URL:** A link to redirect users to a landing page, "About Us" page, or your corporate website.
- **Support:** A link to the support channel can be an email, a ticket portal, or a phone number.
- **Additional information:** Details or user disclaimer about your application, such as region covered, type of billing, limited access, etc.  There is no character limit.
- **Video:** A video to feature on your product page. Videos are exciting resources to complement screenshots as an educational tool showing your app’s main benefits and features.
- **Metric description:**  Field describes each metric declared in the billingOptions field (found in the app's `manifest.json` file).

>⚠️ Warning
>
> The `metricDescription` is required only for applications whose pricing is based on one or more metrics. Please do not fill in this field if this is not the case.

The files in this folder must be available in English, Spanish, and Portuguese in the following paths: `public/metadata/messages/en-US.json`, `public/metadata/messages/es-AR.json` and `public/metadata/messages/pt-BR.json`, respectively.

These fiels are important since they are the first point of contact that merchants have with your app and decide if the app is the right solution for their business. To learn how you can write good copies to each of these fields, please refer to ther [Marketing Assets Guidelines](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-business-guidelines-marketing-assets#messages). 

### Step 3 - Publishing and deploying your app on the VTEX IO development platform

If you are comfortable with your new app and want to make your changes public in your account’s production workspace, follow the steps described in our guide on [Making your new app version publicly available](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-making-your-new-app-version-publicly-available).


## Next
Once your app is public available, you can share it in the VTEX App Store. To the next step follow [Submitting your app to the VTEX App Store](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-submitting-your-app-in-the-vtex-app-store)
