---
title: Configuring a B2B environment
description: "Make your store's content available only to users of other customer stores using a B2B environment."
date: "02/19/2020"
tags: ["configuring", "b2b", "environment", "company"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/configuring-a-b2b-environment.md"
---

# Configuring a B2B environment

B2B (Business to Business) is an abbreviation used in ecommerce in reference to commercial transactions between companies.

In other words, B2B stores only sell their products to other businesses. Because of that, their environments require **user authentication**, since these are usually blocked, completely or partially, for anonymous users.

Follow the step by step below and learn how to make your store's content available only to users of other customer stores.

> ⚠️ If you are using the [B2B Suite](https://developers.vtex.com/vtex-developer-docs/docs/vtex-b2b-suite), keep in mind that none of the steps described in this article are compatible with that solution, since B2B Suite provides an alternative solution for access control on B2B stores by using [Storefront Permissions UI](https://developers.vtex.com/vtex-developer-docs/docs/vtex-storefront-permissions-ui). Following the instructions in this guide can cause issues with the B2B Suite implementation.

## Step by step

### Step 1 - Configuring the Challenge block

The key element that ensures the security of the displayed content is the **Challenge Trade Policy** block, responsible for checking if the store's user is allowed to browse the B2B environment.

Check out the [Challenge Trade Policy documentation](https://developers.vtex.com/vtex-developer-docs/docs/vtex-challenge-tp-condition/) to configure it correctly in your store and proceed to the next steps.

### Step 2 - Defining the Condition Rule

With the Challenge configured, it's time for you to define what the access criterion will be - in other words, the **condition rule** that will allow a user to browse your store.

To define the condition rule, you first need to choose which of your store's Trade Policy it will be applied to. Each Trade Policy must have its Condition Rule defined **individually**, since each one has its own catalog, price and logistics particularities.

Make sure you fully understand what the [Trade Policies](https://help.vtex.com/tutorial/what-is-a-sales-policy--563tbcL0TYKEKeOY4IAgAE) for VTEX stores are before performing the steps below:

1. Access the **Trade policies** section in the admin's sidebar;
2. Choose the desired Trade Policy. You can edit an existing one, by clicking on **Edit**, or [create one from scratch](https://help.vtex.com/faq/how-to-configure-a-new-trade-policy--frequentlyAskedQuestions_700), by clicking on **New Trade Policy**. 
3. In the **Condition Rule** field, define an access criterion of your choosing for the users who will access the trade policy in question. For example: if only logged in users can access store content, your **Condition Rule** could be something like `approved=true`.

![condition-rule](https://user-images.githubusercontent.com/52087100/74885765-24073880-5355-11ea-81ab-41b9449a718b.png)

>ℹ️ The value entered in the Condition Rule field can be any one of your choosing. Remember to choose an intuitive condition and a clear rule, since both will be added to Master Data later for the user's verification to be successful.

### Step 3 - Updating the user form in Master Data

In this last step, you will create a link between the Condition Rule and the user profiles you want to have access to the store.

In other words, you will add a **field in the profile forms** of the users in question (through the admin's Master Data). That field is able to indicate whether the user is qualified to browse your store, according to the criterion you set forth.

1. Access **Master Data** from the admin's sidebar;
2. In the **Profile System** box, click on the settings icon;
3. Select the option **Data structure** inside the **Configurations** box;
4. Once in the new window, access the **Data Entities** tab;
5. In the customer's Data Entity, [create a user field](https://help.vtex.com/tutorial/how-can-i-create-field-in-master-data--frequentlyAskedQuestions_1829#dynamic-storage). According to the previous example, we could create a Boolean type `approved` field, with two possible options: `true` (logged in) and `false` (not logged in)
6. [Add the newly created field](https://help.vtex.com/tutorial/how-can-i-create-field-in-master-data--frequentlyAskedQuestions_1829#dynamic-storage) to the forms of the target user in order to verify and grant access to these customers.

After completing all the steps, your store is ready to focus on selling to other businesses.
