---
title: Disabling automatic translation
description: "Find out how to disable automatic translation in your store."
date: "11/01/2021"
tags: ["translation", "disable", "messages"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store-managements/disabling-automatic-translation.md"
---

# Disabling automatic translation

Automatic translation is handled by the Messages app.

>ℹ️ *Messages is a standalone application responsible for providing message translations for rendering. It aggregates all the translation services in the VTEX platform, regardless of the app nature (backend or frontend) and the actor responsible for that translation (e.g., app definition, automatic translation service, or overwritten messages via APIs).*

By default, the Messages app enables messages not manually translated to be automatically translated.

When deciding which translation it should render, the Messages app first processes overwritten translations defined via API requests at an account-level.

>ℹ️ *Follow [this link](https://developers.vtex.com/vtex-developer-docs/docs/storefront-content-internationalization) to learn how to overwrite storefront messages.*

>ℹ️ *Follow [this link](https://developers.vtex.com/vtex-developer-docs/docs/catalog-internationalization) to learn how to overwrite messages from the catalog.*

If no account-level translation is found, the Messages app goes through the storefront app translations (defined within the `/messages` folder).

>ℹ️ *Follow [this link](https://vtex.io/docs/getting-started/desenvolva-componentes-usando-vtex-io-e-react/7/) to learn how to set translatable messages in your React component.*

Finally, if no specific translation is still not found, then the Messages app falls back to the automatic translation service.

To disable the automatic translation service, check the following section.

## Step by step

1. Access the admin.
2. Go to *Account Settings > My apps*.
3. Search for the VTEX Messages app.
4. Uncheck the following checkbox: **Enable Automatic Translations**.
5. Save your changes.

That's it! Now, messages that don't have custom translations won't be automatically translated anymore.
