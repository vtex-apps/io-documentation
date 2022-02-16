---
title: Internationalizing product prices
description: "Set the currency code and number of decimal places in which your store's product prices will be displayed for international users."
date: "2020-05-23"
tags: ["currency", "code", "decimal", "places", "prices", "internationalizing"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store-management/internationalizing-product-prices.md"
---

# Internationalizing product prices

Before globalizing your brand, it's crucial to first take care of your website's content internationalization. 

It goes without saying that new international users must be able to understand every text being displayed, navigate seamlessly and be able to conclude their purchases without being frustrated by misleading product price information due to the conversion of currencies.

With regards to this last example, VTEX IO overcomes the hurdles of a store’s internationalization process and allows you to **set the currency code and number of decimal places in which your store's product prices will be displayed**.

Through your store's [trade policies](https://help.vtex.com/tutorial/what-is-a-sales-policy--563tbcL0TYKEKeOY4IAgAE), you can set different currency codes for each locale.

## Step by step

1. Access your VTEX account's admin;
2. Using the sidebar, access the Trade Policy section;
3. Select the desired Trade Policy to which the configurations will be applied;
4. In the `Currency Code` field, set the international currency code used to display prices;
5. In the `Culture Info` field, select your store's native country and the website's native language.

![international-currency](https://user-images.githubusercontent.com/52087100/82942068-c8f56b00-9f6d-11ea-8346-77260c8ae3a0.png)

Once your changes are saved, VTEX IO will be able to understand that whenever a user's locale differs from the default one set in the `Culture Info` field, it is dealing with an international user.

Therefore, the currency code shown should follow currency code international standards (ISO standard). For these scenarios, the platform will display prices (including their decimal places) according to the international currency code set in the `Currency Code` field.

>ℹ️ The price's decimal places are displayed according to language selected in the `Currency Code` field, following the ISO standards. Therefore, the `Currency Decimal Places` field is not mandatory. You should only use it in scenarios where you desire to overwrite the decimal places defined by the ISO standards. 

Following the same logic, whenever a user's locale is the same as the default one set in the `Culture Info` field, VTEX IO will interpret that it is dealing with a local user and thereby the currency code won’t need to follow international standards - the commonly used currency symbol for that country will suffice.

To make this platform logic more tangible, imagine the following scenario: a Brazilian retailer sets the `Culture Info` field value to `Brasil(pt-BR)` and the `Currency Code` to `Real (BRL)` .

For international users, the product prices will be displayed using the `BRL` currency code but for local ones, meaning for user whose locale is the same as the one set in `Culture Info`, the `R$` currency code is enough.

>⚠️Remember that **the saved configuration will only be applied to the specifically selected trade policy**. To replicate these configurations in all of your store's trade policies, you must fill out the fields in each trade policy and save the changes.
