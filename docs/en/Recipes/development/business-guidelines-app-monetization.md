---
title: App monetization
description: "App Store's business models are flexible and, thus, adaptable to different scenarios for marketing your app."
date: "2021-07-21"
tags: ["app-store", "app", "development", "homologation"]
version: " "
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/development/business-guidelines-app-monetization.md#paid-distribution"
---

# App monetization

App Store's business models are flexible and, thus, adaptable to different scenarios for marketing your app.

Currently, there are two models available: 
- [Free distribution](#free-distribution)
- [Paid distribution](#paid-distribution)

> ℹ️ The business model is defined in the `billingOptions` field of the app's `manifest.json` file. Check out our documentation on [Setting your app's billing model](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-setting-your-apps-billing-model) to learn how to set up the most suitable billing type.


## Free distribution
 
 Even with different monetization possibilities, you can offer your app for free, without installation costs for users. In this case, the fees for the app distribution through the VTEX App Store are defined in a business partnership with the VTEX team prior to the homologation of the app. 


 ## Paid distribution

 ### Fixed fee

 A simplified billing option, recommended for projects with low infrastructure costs in which you set a single monthly fee to distribute the application. Therefore, all users interested in using your software would pay the same amount, regardless of how long they use it. 

### Variable fee

Variable pricing based on metrics predefined in the application code. For example, for an SMS sender app, the billing metric could be the number of messages sent per user. 

### Hybrid fee
This is a more sophisticated billing model, in which fixed and variable prices can be combined into predefined metrics in the application code. Considering the example of the previous topic, in the Hybrid fee model, you would define a variable fee depending on the number of messages sent by users. 

## Revenue share

In all the scenarios presented above, a revenue-sharing fee will be applied to the app's pricing to commercialize it in the VTEX App Store:

Business model  | Amount | Billing
--------------- | ----------- | -------
Free distribution | Negotiable (in %) | Percentage to be defined in the trade agreement with the VTEX partner program.
Paid distribution | 25% |  Percentage charged on the total value of approved app orders.

> ℹ️  Your app's invoices will be available in the Billing module of the VTEX Admin. In this format, you, as the person responsible for the application, must issue an invoice so that VTEX can make the appropriate financial transfers following the split agreed upon in the business model. You can also track the app's sales using our Order Management System (OMS), which is integrated into the admin panel of your VTEX account.
