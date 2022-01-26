---
title: Marketing Assets
description: "Your application's storefront in the VTEX App Store is composed of marketing assets. 
You must provide all assets when submitting the app for review in the homologation process."
date: "2021-07-22"
tags: ["app-store", "app", "development", "Marketing assets"]
version: " "
git: " "
---
# Marketing assets

Your application's storefront in the VTEX App Store is composed of marketing assets. 

You must provide all assets when submitting the app for review in the homologation process. 

## Metadata structure 

All marketing assets are included in the application via their metadata. To be properly read by our system, they must have the following folder and file structure:

![marketing-assets-structure](https://user-images.githubusercontent.com/67270558/126642568-48a27412-fd3c-4b15-b5c3-15ab43a1bf4b.png)

Find more details about each of the folders in the topics below.

### Images

The Images folder is where the images of your application are stored, including its icon and screenshots that might help users during the implementation process. 

### Icon
Your app icon is the first point of contact between the software you are offering and the retailers browsing the VTEX App Store. 

It expresses the visual identity of your application and helps reinforce your brand in our environment. When building the graphic icon, it must follow the criteria below:
- PNG format
- Saved under the name `icon` in the Images folder.
- Minimum resolution of 1024 x 1024 pixels.
- 1:1 ratio.
- Transparent background.
- Square image, without rounded corners.
- Icon size should not exceed 75% of the total space available.

![icon-measurements](https://user-images.githubusercontent.com/67270558/126643069-18ead453-ce79-44d6-847b-e9e4f1a378c4.png)

### Screenshots
Screenshots allow users to view how the application will behave, either in the admin panel or in the storefront itself. Therefore, they are one of the features that hold the greatest appeal during the decision to install the app.

It is required to include at least one screenshot of your application in the metadata, but we strongly suggest that you add at least three to five images, following the criteria below:

- PNG format.
- Saved in the Screenshots subfolder (`/images/screenshots`).
- Application-focused capture, with no extra elements in the image that could distract the user.

> ⚠️ Screenshots from the admin environment are likely to include the side menu and the VTEX account name. Similarly, screenshots from the storefront often include the browser's navigation bar and tabs. Please pay particular attention to these elements and remove them from your application screenshots before submission. 

> ℹ️ You can add specific screenshots for mobile and desktop users. Categorize the screenshots saving them into sub-folders for each device, considering your target audience. You can save them in the following paths: `public/metadata/images/screenshots/mobile` and `public/metadata/images/screenshots/desktop`. 

## Licenses

The Metadata Licenses folder contains the terms and conditions of your application, which are essential to establish the direct business relationship between you, the developer, and the retailer that installs the app.

In this document, you should include topics such as support, any external costs, and the like.

> ⚠️ It is required to offer the terms and conditions for your application in three languages: English, Spanish and Portuguese. They should be available in the paths `public/metadata/licenses/en-US.md`, `public/metadata/licenses/es-AR.md`, and `public/metadata/licenses/en-BR.md`, respectively.

## Messages

The information contained in the Messages folder is the main marketing resource to commercialize the app since it defines the app's name, description, main features, and other essential characteristics. 

Due to its importance, such information must be available in English, Spanish, and Portuguese in the following paths `public/metadata/messages/en-US.json`, `public/metadata/messages/es-AR.json` and `public/metadata/messages/pt-BR.json`, respectively. 


The base template for structuring this file is as follows: 
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
    "additionalInformation": "Additional information\\nYou can also write new lines here\\n\\n\\nIt should work just like the overview",
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

### Name – Required 

Define the name of your application, limited to 26 characters. This name will act as a public title for the app and will be visible to all users browsing the VTEX App Store. 

> ℹ️ When defining the name of the application, be clear and objective about the service it offers. 

### Headline – Required

In the `headline` field, you should provide a short description of the main functionality of your application. 

As with the title, be objective about the benefits that your extension offers for retailers. Avoid repeating the application name here, and do not write long and abstract descriptions — the field has a 120 character limit.

> ℹ️ Together with the icon and the `name` field, the headline is one of the assets that will be shown to all users visiting the VTEX App Store. Therefore, it has a big impact on the amount of traffic your page will receive. Be careful when writing it, because it is essential for the commercial success of your extension.

![icons-names-headlines](https://user-images.githubusercontent.com/67270558/126645261-cb63697d-a90f-4b28-9de4-f9be98c3faa7.png)
_Examples of icons, names and headlines of eight apps in the VTEX App Store._

### Overview – Required

Overview is the first content block on the product page in the VTEX App Store. This is the first information about your app that retailers will see after clicking it. 

Use the overview to describe in detail the main purposes and benefits of your software, complementing the information in the headline.

> ℹ️ There is no size limit for this block, but we recommend keeping it between 250 and 400 characters long. You can add line breaks by typing `\\\\n` or start new paragraphs by typing `\\\\n\\\\n`.

![overview](https://user-images.githubusercontent.com/67270558/126645655-c86f0611-453a-4d6e-9e9e-0918ffda562d.png)

### Features – Required 

The `features` block appears next to the `overview` and provides a list of your application's features. 

Use this section to highlight which tasks can be performed on your extension. Write clear, concise and brief texts, with bullet points to enable quick reading.

![features](https://user-images.githubusercontent.com/67270558/126646658-32eb95f9-c27c-4b92-8445-eeece446b415.png)


### Website URL – Required 
Your website URL will be displayed in the sidebar of the product page. It is an interesting feature to present your solution in more depth to retailers browsing the VTEX App Store. 

Enter a valid URL in this field to direct them to a landing page, "About Us" page, or your corporate website.

### Support – Required
Below the `websiteURL`, also in the sidebar of the product page, the link to the support channel to be declared in this field is displayed.
It is required to include a support channel, be it an email, a ticket portal, or a phone number.

![support](https://user-images.githubusercontent.com/67270558/126646365-b55aec8f-5a7d-427f-ace8-254762053dbf.png)
_Your website and support URLs will be displayed in the sidebar of your app’s PDP. Check out a live example [here](https://apps.vtex.com/vtex-google-shopping/p)._ 


### Additional information – Optional
You can add additional information to your metadata using the Additional information feature. Use this space to provide more specific details about your application, using the same rules as for the overview field.

![aditional-information](https://user-images.githubusercontent.com/67270558/126645927-de0289c1-4fcb-4e50-bebf-99cdc6feafc7.png)
_Additional information is an optional field to add observations about the use of your app. Check out a live example [here](https://apps.vtex.com/vtex-google-shopping/p)._ 

### Video – Optional
In this field, you can add the public URL of a video you want to feature on your product page. Videos are interesting resources to complement screenshots as an educational tool.

We recommend that you make a video showing the main benefits and features of your app.

![video](https://user-images.githubusercontent.com/67270558/126647428-2f98cb36-9e31-4d2b-9375-0767dc74ef94.png)
_Use a public URL to have your video added next to the overview in the PDP. Check out a live example [here](https://apps.vtex.com/cliqueretire-ebox/p)._

### Metric description – Required/Optional
The `metricDescription` is required only for applications whose pricing is based on one or more metrics. If this is not the case, please do not fill in this field.

For each metric declared in the `billingOptions` field (found in the app's `manifest.json` file), you must include a simple description of how it works. This description will be read by the extension buyer and will help them understand what each metric does and how it will impact the application billing.


