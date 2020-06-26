# Overwriting the Messages app

## Introduction

Messages is VTEX IO's key tool for your store's **internationalization**, since it's responsible for translating any website message (that is, website text content) for rendering. 

However, you may feel that some translations done by the app are not what you want them to be. Therefore, you may want to change the translated content to something more specific or representative of your store, such as a special login message for Spanish speaking users from Argentina. 

In the next section, we present you a step by step on how to overwrite a translation from your store's catalog, such as a product name or a product description, and text messages exported from an app.

## Step by step

1. [Install](https://vtex.io/docs/recipes/store/installing-an-app) the `vtex.admin-graphql-ide@3.x` app using your terminal.

2. Access the **GraphQL admin IDE** section of the desired account. You may find it in the admin's side-bar menu:

![overwriting-messages-adminsidebarmenu](https://user-images.githubusercontent.com/52087100/66516950-95d29a00-eab8-11e9-8cea-080fbdab84d5.png)

3. From the dropdown list, choose the `vtex.messages` app.
4. Write the following mutation command in the text box that is displayed:

```json
mutation Save($saveArgs: SaveArgsV2!) {
  saveV2(args: $saveArgs)
}
```

5. Then, click on  **Query Variables** at the bottom of the page. Now, your screen may look like the following:

![queryvariables](https://user-images.githubusercontent.com/60782333/85610649-8e92f280-b62d-11ea-9a5e-aa7ced1a1549.png)

6. To fill in the `Query Variables` box, check the next sections **according to your store's desired scenario** (*catalog* or *app* messages translations).
7. After adjusting your query, click on the play button to run the declared mutation. For both scenarios, the expected response is as follows:

```json
{
  "data": {
    "saveV2": true
  }
}
```
Once you receive the expected response, no further actions are needed on your part: you are ready to check out the desired changes in your store!

You also can confirm whether Messages properly saved the new translations or not by performing a query. To know further, check out the **Checking your changes** section.


### Catalog translations

Use the following example as a guide if you aim to translate text messages from your store's catalog, such as a product name or a product description.

```json
{
  "saveArgs": {
    "to": "pt-BR",
    "messages": [
      {
        "srcLang": "en-US",
        "srcMessage": "Original product name in English",
        "context": "543123",
        "targetMessage": "Nome do produto em português"
      }
    ]
  }
}
```

**These variables are flexible and must fit your store's given scenario**. The variables for the store catalog translations are as follows:

- `to`: target translation locale.
- `messages`: a list of the messages you want to translate, containing the following parameters:
    - `srcLang`: source message locale.
    - `srcMessage`: source message string.
    - `context`: ID of the product/brand/category that you want to translate. IDs can be found in your store's registration on the admin under Product > Catalog.
    - `targetMessage`: translated message string.

To better understand the full process of overwriting a product message translation, check the following gif:

![ProductTranslation](https://user-images.githubusercontent.com/60782333/85765724-c2811d00-b6ec-11ea-8ada-a9e688c36b86.gif)

### App messages translations

Use the following example as a guide if you aim to translate text messages exported from an app (declared in the app's `messages` folder).

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

**These variables are flexible and must match your store's desired scenario**. The variables for app message translations are as follows:

- `to`: target translation locale.
- `messages`: a list of the messages you want to translate, containing the following parameters:
    - `srcLang`: source message locale. This variable must contain the value `en-DV`, no matter which locale is rendered on the app's interface.
    - `srcMessage`: the `id` of your message string declared in the app's `messages` folder.
    - `context`: the name of the app in which the message is being overwritten.
    - `targetMessage`: translated message string.

To better understand the full process of overwriting an app message translation, check the following gif:

![AppMessageTranslation](https://user-images.githubusercontent.com/60782333/85605881-fbf05480-b628-11ea-8ea9-1dbf364f07fd.gif)

## Checking your changes

If you have already performed the desired mutations, you can check your changes through a query in the GraphQL IDE, **according to your store's desired scenario** (*catalog* or *app* messages translations).

### Checking catalog messages translations

1. In the **GraphQL admin IDE**, after choosing the `vtex.messages` app, write the following query command in the text box that is displayed:

```json
query GetTranslation($args2: TranslateArgs!) {
  translate(args: $args2) 
} 
```

2. Then, to fill in the `Query Variables` box, you must provide the following parameters:

- `from`: source message locale.
- `messages`: a list of the messages you want to check translations, containing the following parameters:
  - `content`: source message string. 
  - `context`: ID of the product/brand/category that you want to check the translation. IDs can be found in your store's registration on the admin under Product > Catalog.
- `to`: target translation locale.

Take the following example:

```json
{
  "args2": {
    "indexedByFrom": [
      {
      	"from": "en-US",
      	"messages": [
          {
            "content": "Original product name in English",
            "context": "543123"
          }
        ]
      }
    ],
    "to": "pt-BR"
  }
}
```

3. After adjusting your query, click on the play button to run it. The expected response is the translated message in the target locale. 

For the given example, the expected response is as follows:

```json
{
  "data": {
    "translate": [
      "Nome do produto em português"
    ]
  }
}
```

### Checking app messages translations

1. In the **GraphQL admin IDE**, after choosing the `vtex.messages` app, write the following query command in the text box that is displayed:

```json
query GetTranslation($args: TranslateWithDependenciesArgs!) {
  translateWithDependencies(args: $args)
} 
```

2. Then, to fill in the `Query Variables` box, you must provide the following parameters:

- `from`: source message locale.
- `messages`: a list of the messages you want to check translations, containing the following parameters:
  - `content`: the `id` of your message string declared in the app's `messages` folder.
  - `context`: the name of the app in which the message has been overwritten.
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

3. After adjusting your query, click on the play button to run it. The expected response is the translated message in the target locale. 

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
