---
title: Submitting your app in the VTEX app store
description: "Learn how to submit your project to the VTEX App Store, the VTEX marketplace for plug-and-play solutions."
date: "2020-09-11"
tags: ["app-store", "app", "development", "publish"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/development/submitting-your-app-in-the-vtex-app-store.md"
---

#  Submitting your app in the VTEX app store

The [**VTEX App Store**](https://extensions.vtex.com/) is a marketplace for VTEX IO plug-and-play solutions. 

It can be used by any VTEX partners willing to **share their solutions** with other VTEX users so they can also **leverage their business**. 

As expected from something carrying the VTEX brand, the app store has a structured homologation process that makes developed apps available to the entire ecosystem.
 
The process comprises the following steps, along with required actions for each.

##  Step by step

Adding an app to the VTEX app store is based on four main steps:

1. Express your interest to our team
2. Sign our commercial agreement
3. Register as a VTEX App Store seller
4. Check out our business, design and engineering guidelines 
5. Send the app's data for validation
6. Wait for the App homologation

###  Step 1 - Expressing your interest

Fill out the [Application form](https://forms.gle/wpkXMxgSfCXwMPbs8) to **share your interest** in publishing your application or integration on the VTEX App Store.

The form will help our team to understand the best approach and prioritize the publication demands.

###  Step 2 - Signing our commercial agreement

If the form was correctly filled out and the team agrees that the application is suitable for the VTEX App Store, the next step is to sign a commercial agreement with VTEX.

This contract, provided by the VTEX team to you, will grant VTEX distribution rights over the app. In addition, it is going to sign your account up to the VTEX **Network Partner Program** if you are not already a member.

>ℹ️ *The [Network Partner Program](https://network.vtex.com/terms_of_use) provides access to a VTEX account, allowing you to test and develop new apps and have access to tech support from the VTEX partner team.*

### Step 3 - Registering as a VTEX App Store seller

The App Store is a **Marketplace**. Therefore, partners looking to distribute their apps should register as a  **seller** there. 

This [structure](https://help.vtex.com/tutorial/configuring-the-marketplace-between-vtex-stores--tutorials_6520) (seller - marketplace) configuration is done through the `vtex.app-store-seller` app.

Follow the steps below to register as a new seller on VTEX App Store:

1. Logged into the VTEX account in which you are working, run `vtex install vtex.app-store-seller` in your terminal.
2. Access the admin of the VTEX account in which you're working. 
3. In `Other`, access `Seller setup` and fill out the required fields.
4. Select the sales channel you intend to use to connect to the App Store.
5. Choose an affiliate ID, made up of 3 consonants:

![submitting-seller-1](https://user-images.githubusercontent.com/52087100/92964918-48d71080-f44b-11ea-8929-b744915e3fb0.png)

![submitting-seller-2](https://user-images.githubusercontent.com/52087100/92964922-4a083d80-f44b-11ea-886d-39eac7a3cee0.png)

After submitting the request to be a seller, you can check its `status` until our team approves it. This approval is required in order to complete the next steps and be able to successfully publish your app on the VTEX App Store.

### Step 4 - Checking out our business, design and engineering guidelines


### Step 5 - Sending the app data for validation

Once you've configured the app assets, it is time to submit the app's data for evaluation by the app store development team. First of all, you'll need to meet the following prerequisites:

- Have a [**GitHub**](https://github.com/) account (since your project evaluation during the homologation process is made through Pull Requests).
- [Publish your app on the VTEX IO development platform](https://vtex.io/docs/recipes/development/publishing-an-app/). Remember to publish the app in the VTEX account in which you are working and in a [workspace](https://vtex.io/docs/concepts/workspace/) that can be tested by the team.
- [Deploy your app on the VTEX IO development platform](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-making-your-new-app-version-publicly-available#step-6---deploying-the-app-stable-version).

With the first two prerequisites met, you're ready to send you app through to VTEX's homologation process:

1. Using your CLI, [log into the VTEX account](https://vtex.io/docs/recipes/development/vtex-io-cli-installation-and-command-reference/#command-reference) in which the app was published.
2. Access the folder containing your app.
3. Run `vtex submit`. You can also specify which version your want to submit by running `vtex submit {vendor}.{name}@{version}`.

After step 3, a GitHub repository will be automatically created and a Pull Request link will be displayed on your CLI.

>ℹ️ *You'll be added to the repository with your GitHub handle and will have read-only permissions to be able to follow your app's review process. Comments can be followed in the same repository and after performing adjustments, any new app version can be submitted following the step 2 above, thereby creating a new `branch` containing the new version in the same repository.*

![submitting-github-terminal](https://user-images.githubusercontent.com/52087100/92964915-483e7a00-f44b-11ea-8bbf-f8f4e8c4da32.png)

When a branch has the adjustments it needs, you should open a _Pull Request_ to the VTEX team.

![submitting-github-pr](https://user-images.githubusercontent.com/52087100/92964912-470d4d00-f44b-11ea-8c2b-e09a13093da6.png)

###  Step 6 - Waiting for the app homologation

Once the app data has been sent in the PR, our product team will validate it in order to approve and merge it.

This process, called homologation, will ensure that any published application has a clear value proposition, is safe, stable, aligned with VTEX's brand and business guidelines and is in compliance with the company's business, design and technology standards.

Therefore, the **3 main criteria** taken into account by the VTEX product team are:

- **Business**  - Whether the app has a business model with viable and sustainable pricing and accomplishes what it sets out to do.
- **UX**  - Whether the app offers a good user experience, following VTEX Styleguide rules.
- **Security and performance**  - Whether the app's performance is safe and efficient. 

You can find more details on how these criteria will be assessed in our [app development guidelines](). 

When an app fulfills the above-mentioned criteria, the PR will be approved and your new app version is ready to be released and made available in the VTEX app store. 

Notice the following: once everything is approved, a product (which effectively is your app) will be automatically created in your store catalog. Do not remove our change it - this product is what integrates your app to the VTEX App Store marketplace. 







