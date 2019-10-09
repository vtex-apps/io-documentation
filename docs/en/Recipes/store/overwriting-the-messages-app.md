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

```
mutation Save($save: SaveArgs!){
  save(args: $save)
}
```

5. Then, click on  __Query variables__ at the bottom of the page. 
6. **According to your store's scenario**, write the following variables into the text box:

```
{
  "save": {
    "to": "en-US",
    "messagesByProvider": [{
      "provider": "vtex.login@2.x",
      "messages": [{
        "id": "store/login.signIn",
        "content": "Welcome! Please log in "
      }]
    }]
  }
}
```

Note that the variable values `to`, `provider`, `id` and `content` will tell the Messages app where and what the message change will be. Therefore, **these variables are flexible and must fit your store's desired scenario**. The variables are as follows:

- `to`: where the message is located. 
- `provider`: App message provider. 
- `id`: message ID.
- `content`: message content itself. 

Following the given example above, your admin should look similar to this: 

![overriding-messages-interface](https://user-images.githubusercontent.com/52087100/66517040-bdc1fd80-eab8-11e9-8082-ab0c4bdc640e.png)

Finally, click on the play button to run the declared mutation. 

![overwriting-messages-play](https://user-images.githubusercontent.com/52087100/66517074-d29e9100-eab8-11e9-9d30-2fd4e91d4de1.png)

The expected response is as follows:

```
{
  "data": {
    "save": true
  }
}
```

Now, no other actions are needed on your part. Once you receive the expected response, you are ready to check out the desired changes in your store!
