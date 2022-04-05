---
title: Submitting your app to the VTEX app store
description: "Learn how to submit your project to the VTEX App Store, the VTEX marketplace for plug-and-play solutions."
date: "2020-09-11"
tags: ["app-store", "app", "development", "publish"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/development/submitting-your-app-in-the-vtex-app-store.md"
---

#  Submitting your app to the VTEX App Store

To share your solutions in the VTEX App Store, you must follow our homologation process:
 
1. Check out our business, design and engineering guidelines.
2. Send the app's data for validation.
3. Wait for the App homologation.

## Before you start

Before submitting your app to the VTEX App Store, you must be a registered VTEX App Store developer. For more information, check [this guide.](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-becoming-a-registered-vtex-app-store-developer)

##  Step by step

### Step 1 - Checking out our business, design and engineering guidelines

To submit and publish your app on VTEX App Store, you must follow our business, design and engineering guidelines. These guidelines guarantee the standard of quality, viability and usability of all apps made available to our tenants through the VTEX App Store, so it is important that you are aware of them before submitting your extension for the homologation process. You can check in [Business guidelines](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-business-guidelines-vtex-app-store), [Design guidelines](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-design-guidelines), [Engineering guidelines](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-engineering-guidelines).

### Step 2 - Sending the app data for validation

Once you've configured the app assets, it is time to submit the app's data for evaluation by the app store development team. First of all, you'll need to meet the following prerequisites:

- Have a [**GitHub**](https://github.com/) account (since your project evaluation during the homologation process is made through Pull Requests).
- [Publish your app on the VTEX IO development platform](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-publishing-an-app/). Remember to publish the app in the VTEX account in which you are working and in a [workspace](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-workspace/) that can be tested by the team.
- [Deploy your app on the VTEX IO development platform](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-making-your-new-app-version-publicly-available#step-6---deploying-the-app-stable-version).

With the first two prerequisites met, you're ready to send you app through to VTEX's homologation process:

1. Using your CLI, [log into the VTEX account](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installation-and-command-reference/#command-reference) in which the app was published.
2. Access the folder containing your app.
3. Run `vtex plugins add submit` plugin in the [VTEX CLI](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installation-and-command-reference).

> ⚠️ Warning 
> 
> The `vtex plugins add submit` plugin will only work if the VTEX IO CLI is updated to version 3.x that has a plugin-based architecture. Check out the [Updating VTEX IO'S CLI](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-update) and [Managing plugins documentation](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-plugins) for more information.

4. Then, run `vtex submit`. You can also specify which version your want to submit by running `vtex submit {vendor}.{name}@{version}`.

After step 4 , a GitHub repository will be automatically created and a Pull Request link will be displayed on your CLI.

>ℹ️ Info
>
> You'll be added to the repository with your GitHub handle and will have read-only permissions to be able to follow your app's review process. Comments can be followed in the same repository and after performing adjustments, any new app version can be submitted following the step 2 above, thereby creating a new `branch` containing the new version in the same repository.

![submitting-github-terminal](https://user-images.githubusercontent.com/52087100/92964915-483e7a00-f44b-11ea-8bbf-f8f4e8c4da32.png)

When a branch has the adjustments it needs, you should open a _Pull Request_ to the VTEX team.

![submitting-github-pr](https://user-images.githubusercontent.com/52087100/92964912-470d4d00-f44b-11ea-8c2b-e09a13093da6.png)

###  Step 3 - Waiting for the app homologation

Once the app data has been sent in the PR, our product team will validate it in order to approve and merge it.

This process, called homologation, will ensure that any published application has a clear value proposition, is safe, stable, aligned with VTEX's brand and business guidelines and is in compliance with the company's business, design and technology standards.

Therefore, the **3 main criteria** taken into account by the VTEX product team are:

- **Business**  - Whether the app has a business model with viable and sustainable pricing and accomplishes what it sets out to do.
- **UX**  - Whether the app offers a good user experience, following VTEX Styleguide rules.
- **Security and performance**  - Whether the app's performance is safe and efficient. 

You can find more details on how these criteria will be assessed in our [Homologation requirements for the VTEX App Store](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-homologation-requirements-for-vtex-app-store). 

When an app fulfills the above-mentioned criteria, the PR will be approved and your new app version is ready to be released and made available in the VTEX app store. 

Notice the following: once everything is approved, a product (which effectively is your app) will be automatically created in your store catalog. Do not remove our change it - this product is what integrates your app to the VTEX App Store marketplace. 

## Related resources

- [App monetization](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-business-guidelines-app-monetization)
- [Marketing guidelines](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-business-guidelines-marketing-assets)
- [User experience guidelines](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-design-guidelines)
- [Engineering guidelines](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-engineering-guidelines)
