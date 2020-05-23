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

Through your store's [trade policies](https://help.vtex.com/tutorial/what-is-a-sales-policy--563tbcL0TYKEKeOY4IAgAE), you can effortlessly internationalize your product values by simply having the [Store Components](https://vtex.io/docs/components/all/vtex.store-components@3.115.0/) app installed in your theme and running version **3.54.0** or higher.

## Step by step

1. Access your VTEX account's admin;
2. Using the sidebar, access the Trade Policy section;
3. Select the desired Trade Policy to which the configurations will be applied;
4. In the `Currency Code` field, set the international currency code used to display prices;
5. In the `Currency Decimal Places`, set the number of decimal places that your store’s prices will use;
6. In the `Culture Info` field, select your store's native country and the website's native language.

![international-currency](https://user-images.githubusercontent.com/52087100/82735893-93e1e200-9cfb-11ea-8c37-c2d224615b54.png)

Once your changes are saved, VTEX IO will be able to understand that whenever a user's locale differs from the default one set in the `Culture Info` field, it is dealing with an international user.

Therefore, the currency code shown should follow currency code international standards (ISO standard). For these scenarios, the platform will display prices with the international currency code set in the `Currency Code` field.

Following the same logic, whenever a user's locale is the same as the default one set in the `Culture Info` field, VTEX IO will interpret that it is dealing with a local user and thereby the currency code won’t need to follow international standards - the commonly used currency symbol for that country will suffice.

To make this platform logic more tangible, imagine the following scenario: a Brazilian retailer sets the `Culture Info` field value to `Brasil(pt-BR)` and the `Currency Code` to `Real (BRL)` .

For international users, the product prices will be displayed using the `BRL` currency code but for local ones, meaning for user whose locale is the same as the one set in `Culture Info`, the `R$` currency code is enough.

<div class="alert alert-info">
Note that <strong>the currency decimal places are independent of the user's locale</strong>. The number that is configured based on the chosen trade policy will be applied to all users that access the website.
</div>

<div class="alert alert-warning">
Remember that <strong>the saved configuration will only be applied to the specifically selected trade policy</strong>. To replicate these configurations in all of your store's trade policies, you must fill out the fields in each trade policy and save the changes.
</div>
