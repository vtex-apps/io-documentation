---
title: Submitting your app in the VTEX app store
description: "Learn how to submit your project to the VTEX App Store, the VTEX marketplace for plug-and-play solutions."
date: "2020-09-11"
tags: ["app-store", "app", "development", "publish"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/adding-new-docs/docs/en/Recipes/development/submitting-an-app-in-the-vtex-app-store.md"
---

#  Submitting your app in the VTEX app store

The [**VTEX App Store**](https://extensions.vtex.com/) is a marketplace for VTEX IO plug-and-play solutions. 

It can be used by any VTEX partners willing to **share their solutions** with other VTEX users so they can also **leverage their business**. 

As expected from something carrying the VTEX brand, the app store has a structured homologation process that makes developed apps available to the entire ecosystem.
 
The process comprises the following steps, along with required actions for each.

##  Step by step

Adding an app to the VTEX app store is based on four main steps:

1. Express your interest to our team.
2. Sign our commercial agreement.
3. Register as a VTEX App Store seller.
4. Configure the app assets.
5. Send the app's data for validation;
6. App homologation.

###  Step 1 - Expressing your interest

Fill out the [Application form](https://forms.gle/wpkXMxgSfCXwMPbs8) to **share your interest** in publishing your application or integration on the VTEX App Store.

The form will help our team to understand the best approach and prioritize the publication demands.

###  Step 2 - Signing the commercial agreement

If the form was correctly filled out and the team agrees that the application is suitable for the VTEX App Store, the next step is to sign a commercial agreement with VTEX.

This contract, provided by the VTEX team to you, will grant VTEX distribution rights over the app. In addition, it is going to sign your account up to the VTEX **Network Partner Program** if you are not already a member.

<div class="alert alert-info">
The <a href="https://network.vtex.com/terms_of_use">Network Partner Program</a> provides access to a VTEX account, allowing you to test and develop new apps and have access to tech support from the VTEX partner team. By default, membership requires a monthly fee, but in scenarios where the development aims to add an app to the App Store, the fee can be waived for at least 6 months.
</div>

### Step 3 - Registering as a VTEX App Store seller

The App Store is a **Marketplace VTEX**. Therefore, partners looking to distribute their apps should register as a  **seller** there. 

This [structure](https://help.vtex.com/tutorial/configuring-the-marketplace-between-vtex-stores--tutorials_6520) (seller - marketplace) configuration is done through the `vtex.app-store-seller`  app.

Follow the steps below to register as a new seller on VTEX App Store:

1. Logged into the VTEX account in which you are working, run `vtex install vtex.app-store-seller` in your terminal.
2. Access the admin of the VTEX account in which you're working. 
3. In `Other`, access `Seller setup` and fill out the required fields.
4. Select the sales channel you intend to use to connect to the App Store.
5. Choose an affiliate ID, made up of 3 consonants:

![submitting-seller-1](https://user-images.githubusercontent.com/52087100/92964918-48d71080-f44b-11ea-8929-b744915e3fb0.png)

![submitting-seller-2](https://user-images.githubusercontent.com/52087100/92964922-4a083d80-f44b-11ea-886d-39eac7a3cee0.png)

After submitting the request to be a seller, you can check its `status` until our team approves it. This approval is required in order to complete the next steps and be able to successfully publish your app on the VTEX App Store.

### Step 4 - Configuring the app assets

To publish and homologate your app on VTEX's App Store, it must have a basic metadata structure as shown below:

![submitting-assets](https://user-images.githubusercontent.com/52087100/92964911-4674b680-f44b-11ea-905f-1bed5db2589a.png)

#### App messages

The messages that an app exports include its most important data, such as its name, public name, short description and full description, among others.

Therefore, the following files are mandatory when publishing your app: `public/metadata/messages/en-US.json`, `public/metadata/messages/pt-BR.json`, `public/metadata/messages/es-AR.json`.

Each of the above encompasses their language locale (English, Portuguese, Spanish) and must adhere to the following model:

```json
{
  "name": "Order Tracker",
    "headline": "Headline Order Tracker",
  "overview": "Tracks all orders\\nSecond line\\n\\nThird line\\n\\n\\n\\n\\nFourth line",
  "features": [
    "First feature",
    "Second feature",
    "Third feature",
    "Fourth feature"
  ],
    "additionalInformation": "Additional information\\nYou can also write new lines here\\n\\n\\nIt should work just like overview",
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

The following fields will comprise the app's product page:

-   `name` (mandatory): App's title, as VTEX App Store users will see it. Limited to 26 characters.
-   `headline` (mandatory): Objective description, highlighting the app's main benefit to users. Limited to 120 characters.
-   `overview` (mandatory): Product page's first part, comprising the app's description. Insert `\\n` for each line break and `\\n\\n` for each new paragraph.
-   `features` (mandatory): list of `strings`, where each element highlights one of app's functionalities.
-   `additionalInformation` (optional): last section of the product page that contains additional information on the app. Follows the same format as the `overview` field.
-   `video` (optional): Valid URL linking to a video that will be displayed on the product page in order to introduce the app.
-   `websiteURL` (mandatory): Valid URL linking to the app's developer portal.
-   `support` (mandatory): Three contact options are possible (email, URL or phone), of which, at least email or URL are mandatory.

####  App icon

The icon is another important element that needs to be configured as it expresses the app's visual identity on the VTEX App Store. It must adhere to the following criteria: 

-   `png` format.
-   Minimum size of **1024 x 1024px**.
-   Proportion of **1:1**.
-   **transparent** background.
-   **square** form without rounded edges.
    
Try to keep the icon's edges limited to 75% of the squares total width, without filling in the entire space, as the following example highlights:

![submitting-assets-icon](https://user-images.githubusercontent.com/52087100/92964904-44125c80-f44b-11ea-8172-810ac823a0a0.png)

#### App screenshots 
    
Screenshots are important for clients to visually perceive how your app will behave, whether in the admin dashboard or storefront itself. They are also useful when explaining the app's configuration process (if there is any), in addition to details on how it operates. 

The screenshots from the `public/metadata/images/screenshots/desktop` folder are mandatory and must be in **`png`** format.

You can include specific screenshots to display to users that access the App Store using a mobile device, by simply adding these screenshots to the `public/metadata/images/screenshots/mobile` folder.

#### App Licenses

The apps' terms and conditions must be added to the following files: `public/metadata/licenses/en-US.md`, `public/metadata/licenses/pt-BR.md`, `public/metadata/licenses/es-AR.md`. 

The terms and conditions are **mandatory** in at least one of the three languages. If the app is released outside Brasil, the terms and conditions in English must be made available in `public/metadata/licenses/en-US.md`.

#### App billing

The app billing should be defines in the app's `manifest.json` file, using the `billingOptions` object. For more details on this object and instructions on how to charge your app users, you can access the [Billing Options documentation](https://www.notion.so/VTEX-Fluxo-de-Publica-o-na-App-Store-7b37a14db36c46b88d2ce29291048944#91050246d35f42889a140e102f74c8b0). 

### Step 5 - Sending the app data for validation

Once you've configured the app assets, it is time to submit the app's data for evaluation by the app store development team. First of all, you'll need to meet the following prerequisites:

- Have a [**GitHub**](https://github.com/) account (since your project evaluation during the homologation process is made through Pull Requests).
- [Publish your app on the VTEX IO development platform](https://vtex.io/docs/recipes/development/publishing-an-app/). Remember to publish the app in the VTEX account in which you are working and in a [workspace](https://vtex.io/docs/concepts/workspace/) that can be tested by the team.

With the first two prerequisites met, you're ready to send you app through to VTEX's homologation process:

1. Using your CLI, [log into the VTEX account](https://vtex.io/docs/recipes/development/vtex-io-cli-installation-and-command-reference/#command-reference) in which the app was published.
2. Access the folder containing your app.
3. Run `vtex submit`. You can also specify which version your want to submit by running `vtex submit {vendor}.{name}@{version}`.

After step 3, a GitHub repository will be automatically created and a Pull Request link will be displayed on your CLI.

<div class="alert alert-info">
You'll be added to the repository with your GitHub handle and will have read-only permissions to be able to follow your app's review process. Comments can be followed in the same repository and after performing adjustments, any new app version can be submitted following the step 2 above, thereby creating a new `branch` containing the new version in the same repository. 
</div>

![submitting-github-pr](https://user-images.githubusercontent.com/52087100/92964912-470d4d00-f44b-11ea-8c2b-e09a13093da6.png)

When a branch has the adjustments it needs, you should open a _Pull Request_ to the VTEX team.

![submitting-github-terminal](https://user-images.githubusercontent.com/52087100/92964915-483e7a00-f44b-11ea-8bbf-f8f4e8c4da32.png)

###  Step 6 - App homologation

Once the app data has been sent in the PR, our product team will validate it in order to approve and merge it.

This process, called homologation, will ensure that any published application has a clear value proposition, is safe, stable, aligned with VTEX's brand and business guidelines and is in compliance with the company's business, design and technology standards.

Therefore, the 3 main criteria taken into account by the VTEX product team are:

- Business  - Whether the app has a business model with viable and sustainable pricing and accomplishes what it sets out to do.
- UX  - Whether the app offers a good user experience, following VTEX Styleguide rules.
- Security and performance  - Whether the app's performance is safe and efficient. 

When an app fulfills the above-mentioned criteria, the PR will be approved and your new app version is ready to be released and made available in the VTEX app store. 

Notice the following: once everything is approved, a product (which effectively is your app) will be automatically created in your store catalog. Do not remove our change it - this product is what integrates your app to the VTEX App Store marketplace. 







