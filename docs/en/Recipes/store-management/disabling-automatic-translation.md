---
title: Disabling automatic translation
description: "Find out how to disable automatic translation in your store."
date: "11/01/2021"
tags: ["translation", "disable", "messages"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store-management/disabling-automatic-translation.md"
---

# Disabling automatic translation

Automatic translation is enabled by default in the Messages app, a standalone application that provides message translations for rendering.

The Messages app aggregates all the translation services in the VTEX platform, regardless of the app nature (backend or frontend) and the actor responsible for that translation (e.g., app definition, automatic translation service, or overwritten messages via APIs).

When deciding which translation the store should display, the Messages app first processes translations defined via API requests at an account-level. Then, if there's no account-level translation, the Messages app goes through storefront app translations (defined within the `/messages` folder). Finally, if no custom translation is found, the Messages app falls back to the automatic translation service.

>ℹ️ Follow [this link](https://developers.vtex.com/vtex-developer-docs/docs/storefront-content-internationalization) to learn how to overwrite storefront messages.

>ℹ️ Follow [this link](https://developers.vtex.com/vtex-developer-docs/docs/catalog-internationalization) to learn how to overwrite messages from the catalog.

>ℹ️ Follow [this link](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-1-developing-storefront-apps-using-react-and-vtex-io) to learn how to set translatable messages in your React component.

To disable the Messages' automatic translation service, check the following section.

## Step by step

1. Access the admin.
2. Go to *Account Settings > My apps*.
3. Search for the VTEX Messages app.
4. Uncheck the following checkbox: **Enable Automatic Translations**.

![Messages Interface](https://user-images.githubusercontent.com/52087100/104200375-586d6280-5407-11eb-8016-199f5e8f2d3e.png)

5. Save your changes.

That's it! Now, messages that don't have custom translations won't be automatically translated anymore.
