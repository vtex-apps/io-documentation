# Translating storefront content

A message is any website text content set as translatable, and Messages is the VTEX IO app responsible for providing message translations for rendering.

As a background, it's important to know that every text set as translatable during the development of a storefront component is automatically translated either by the *storefront app's definitions* (declared in the app's `/messages` folder) or by the *automatic translation service* (when the storefront app doesn't include any specific translation of a message).

However, considering literal translations and cultural factors, some translations might be unsatisfactory. 

Hence, you may want to overwrite a translation provided by the automatic translation service or by the app's definitions with a more specific or representative content of your store. 

For example, you may want to set a special login message for Spanish speaking users from Argentina. 

Considering this case, in the following step by step, we'll teach you how to overwrite a storefront message with exclusive content for your store through the Messages app.

## Step by step

Follow this step by step if you aim to translate text messages exported from an app (declared in the app's `messages` folder).

1. [Install](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-installing-an-app) the `vtex.admin-graphql-ide@3.x` app using your terminal.

2. Access the **GraphQL admin IDE** section of the desired account. You may find it in the admin's side-bar menu:

![overwriting-messages-adminsidebarmenu](https://user-images.githubusercontent.com/52087100/66516950-95d29a00-eab8-11e9-8cea-080fbdab84d5.png)

3. From the dropdown list, choose the `vtex.messages` app.
4. Write the following mutation command in the text box that is displayed:

```
mutation Save($saveArgs: SaveArgsV2!) {
  saveV2(args: $saveArgs)
}
```

5. Then, click on  *Query Variables* at the bottom of the page. Now, your screen may look like the following:

![queryvariables](https://user-images.githubusercontent.com/60782333/85610649-8e92f280-b62d-11ea-9a5e-aa7ced1a1549.png)


6. To fill in the *Query Variables* box, you must provide the following parameters:

- `to`: target translation locale.
- `messages`: a list of the messages you want to translate, containing the following parameters:
    - `srcLang`: source message locale. This variable must contain the value `en-DV`, no matter which locale is rendered on the app's interface.
    - `srcMessage`: the `id` of your message string declared in the app's `messages` folder.
    - `context`: the name of the storefront app that declared the message being overwritten.
    - `targetMessage`: the desired translation for the message string.

Take the following example:
 
```json
{
  "saveArgs": {
    "to": "en-US",
    "messages": [
      {
        "srcLang": "en-DV",
        "srcMessage": "store/search.placeholder",
        "context": "vtex.store-components@3.x",
        "targetMessage": "My personalized Search message"
      }
    ]
  }
}
```

>⚠️ In VTEX IO, translations of storefront components are kept in a `/messages` folder inside the app's root folder. For example, the English translation of the `search.placeholder` message from the `store-components` app is declared [here](https://github.com/vtex-apps/store-components/blob/master/messages/en.json#L2). Hence, in this example, we just overwrote this message with "My personalized Search message" through the Messages app.

7. After adjusting your query, click on the play button to run the declared mutation. The expected response is as follows:


```json
{
  "data": {
    "saveV2": true
  }
}
```

8. (Optional) If you want to check your changes on the GraphQL IDE, check the " Checking your changes" section.

Now, no further actions are needed on your part. Once you receive the expected response, you are ready to check out the desired changes in your store!

To better understand the full process of overwriting an app message translation, check the following gif:

![AppMessageTranslation](https://user-images.githubusercontent.com/60782333/85605881-fbf05480-b628-11ea-8ea9-1dbf364f07fd.gif)

## Checking your changes

If you have already performed the desired mutations, you can check your changes through a query in the GraphQL IDE.

1. In the **GraphQL admin IDE**, after choosing the `vtex.messages` app, write the following query command in the text box that is displayed:

```
query GetTranslation($args: TranslateWithDependenciesArgs!) {
  translateWithDependencies(args: $args)
} 
```

2. Then, click on  *Query Variables* at the bottom of the page.

3. To fill in the *Query Variables* box, you must provide the following parameters:

- `from`: source message locale.
- `messages`: a list of the messages you want to check translations, containing the following parameters:
  - `content`: the `id` of your message string declared in the app's `messages` folder.
  - `context`: the name of the storefront app that declared the message being overwritten.
- `to`: target translation locale.
- `depTree`: the dependency tree as in `"[{\"id\": \"{context}\"}]"`.

Take the following example:

```json
{
"args": {
    "indexedByFrom": [
      {
      	"from": "en-DV",
      	"messages": [
          {
            "content": "store/search.placeholder",
            "context": "vtex.store-components@3.x"
          }
        ]
      }
    ],
    "to": "en-US",
    "depTree": "[{\"id\": \"vtex.store-components@3.x\"}]"
  }
}
```

4. After adjusting your query, click on the play button to run it. The expected response is the translated message in the target locale. 

For the given example, the expected response is as follows:

```json
{
  "data": {
    "translateWithDependencies": [
      "My personalized Search message"
    ]
  }
}
```
