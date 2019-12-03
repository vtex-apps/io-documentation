---
title: Overwriting the Messages app
description: "Learn how to override Messages and replace message content translated by the app with your own."
date: "10/09/2019"
tags: ["messages", "messages-app", "overwriting", "overwrite", "translation"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/overwriting-the-messages-app.md"
---

# Overwriting the Messages app

## Introduction

Messages is VTEX IO's key tool for your store's **internationalization**, since it's responsible for translating any website message (that is, website text content) for rendering. 

However, you may feel that some translations done by the app are not what you want them to be and therefore wish to change the translated content to something more specific or representative of your store, such as a special login message for Spanish speaking users from Argentina.

This recipe will show you how to overwrite the Messages app and easily create new message content through your store's admin.

## Step by step

1. [Install](https://vtex.io/docs/recipes/store/installing-an-app) the `vtex.admin-graphql-ide@3.x` app using your terminal.

2. Access the **GraphQL admin IDE** section of the desired account. You may find it in the admin's side-bar menu:

![overwriting-messages-adminsidebarmenu](https://user-images.githubusercontent.com/52087100/66516950-95d29a00-eab8-11e9-8cea-080fbdab84d5.png)

3. From the dropdown list, choose the `vtex.messages` app.
4. Write the following mutation command in the text box that is displayed:

```graphql
mutation Save($args: SaveArgsV2!) {
  saveV2(args: $args)
}
```

5. Then, click on  __Query variables__ at the bottom of the page. 
6. **According to your store's scenario**, write the following variables into the text box:

### For the store's catalog translations

```json
{
  "args": {
    "to": "en-US",
    "messages": [
      {
        "srcLang": "pt-BR",
        "srcMessage": "Bem vindo! Faça seu Login.",
        "targetMessage": "Welcome! Please, log in. ",
        "context": "vtex.login@2.x"
      }
    ]
  }
}
```

**These variables are flexible and must fit your store's given scenario**. The variables for the store catalog translations are as follows:

- `to`: target translation locale.
- `srcLang`: source message locale.
- `srcMessage`: source message string.
- `targetMessage`: message translation string.
- `context`: message translation context. This variable is not mandatory and only serves to give Messages the context desired for the translation, since the same word can have different meaning depending on the language. If you want o use this variable, you'll have to add, between 3 parenthesis, the desired context to the product name, in the admin's catalog. I.e:  `Mouse (((rodent)))`. The desired value will therefore not be displayed next to the product name and will only be used to the catalog translation.

### For app messages translation:

```json
{
  "args": {
    "to": "en-US",
    "messages": [
      {
        "srcLang": "en-DV",
        "srcMessage": "store/login.signIn",
        "targetMessage": "Welcome! Please log in ",
        "context": "vtex.login@2.x"
      }
    ]
  }
}
```

**These variables are flexible and must match your store's desired scenario**. The variables for app message translations are as follows:

- `to`: target translation locale.
- `srcLang`: source message locale. This variable must contain the value `en-DV`, no matter which locale is rendered on the app's interface.
- `srcMessage`: source message string.  
- `targetMessage`: message translation string.
- `context`: message translation context, meaning the name of the app in which the Messages are being overwritten.

Following the given example above, your admin should look similar to this:

![recipe-messages-overwriting](https://user-images.githubusercontent.com/52087100/68410089-eb0cd480-0166-11ea-89bf-217aa7994b91.png)

Finally, click on the play button to run the declared mutation.

The expected response is as follows:

```json
{
  "data": {
    "saveV2": true
  }
}
```

Now, no other actions are needed on your part. Once you receive the expected response, you are ready to check out the desired changes in your store!
