---
title: Enabling Order Form optimization for your Store
description: "PWA is a sort of web app used to natively promote certain advantageous features to users, such as offline functionalities. This recipe will help you find out how to enable notices that prompt users to install your store's PWA."
date: "11/11/2019"
tags: ["performance", "order-form", "store"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store-management/enabling-order-form-optimization.md"
---

# Enabling Order Form optimization for your Store

## Introduction

Every VTEX IO store uses the `orderForm` to record information regarding the current user session, mainly information about items added into the `cart`, which will be used during checkout. In order for the components in a store's pages to have access to information in the `orderForm`, there is an `OrderFormProvider` in the top-level of every page that exposes this information to everything you see in a store created with Store Framework. This `OrderFormProvider` component is not exposed as a block and is part of the core Store Framework. It's implementation can be found at [`vtex.store-resouces`](https://github.com/vtex-apps/store-resources). Two important native VTEX components consume this information and depend on this `OrderFormProvider` to function properly: `minicart` and `buy-button`.

Along with the efforts in course to bring VTEX Checkout into IO, a **new** `OrderFormProvider` was created and the `OrderFormProvider` from `vtex.store-resources` is now **legacy**. This new `OrderFormProvider` is already used by `minicart.v2`, our new and flexible Minicart, `add-to-cart-button`, our new Buy Button which is not included in `vtex.store-components`, the new `checkout-cart` and all future native blocks and components that will be developed.

To make sure we keep backwards-compatibility in Store Framework, while adding this new provider into the core framework, we kept **both** the legacy and the new one, so now every store by default will be using **two** `OrderFormProvider`s. Unfortunately, this does not come with a performance cost, since this means every store is now fetching **two** `orderForm`s in every render. To avoid this unnecessary overhead for stores that don't need both providers, there is a `Enable Order Form optimization` setting available in the Site Editor that disables the legacy `OrderFormProvider`, using just the new one. Enabling this should result in a smoother navigation experience.

:warning: Use this setting with caution, since it may cause problems in your store if any of its components still need the legacy `orderFormProvider` to function. If your store already uses `minicart.v2` and `add-to-cart-button`, and there are no custom components that depend on the legacy provider, there should be no issues.

Find out how to enable this setting in the steps below.

## Step-by-step

1. In the desired account's admin, access **CMS** and select the **Store**.

![store-settings](https://user-images.githubusercontent.com/27777263/76884738-e8c92e00-685c-11ea-8448-599ae595cf35.png)

2. In the **Advanced** tab, toggle the **Enable orderForm optimization** button.

![enabling-pwa](https://user-images.githubusercontent.com/27777263/76884611-b5869f00-685c-11ea-9999-c867b5500771.png)

3. Save your changes.
