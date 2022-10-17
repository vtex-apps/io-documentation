---
title: Creating a Master Data CRUD app
description: "Step by step guide on how to build a CRUD app using Master Data and VTEX IO."
date: "2022-10-14"
tags: ["master-data", "builder", "app-development"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/development/creating-a-master-data-crud-app.md"
---

# Creating a Master Data CRUD app 

[Master Data](https://help.vtex.com/tutorial/master-data--4otjBnR27u4WUIciQsmkAw) is a powerful data base solution provided by VTEX to your store. You can use it in any VTEX IO app by connecting to the [Master Data API](https://developers.vtex.com/vtex-rest-api/reference/master-data-api-v2-overview), but this can become a repetitive task.

To improve your development experience, you can use the VTEX IO `masterdata` builder to create apps that use [Master Data v2](https://help.vtex.com/tutorial/master-data--4otjBnR27u4WUIciQsmkAw) features, such as saving new data and editing or deleting data, among others.

In this guide, you will learn how to create a Master Data CRUD app in VTEX IO.

## Before starting

Before you start coding your app, it is a good idea to review some concepts:
- Master Data
    - [Basic components](https://help.vtex.com/en/tutorial/master-data--4otjBnR27u4WUIciQsmkAw#basic-components).
    - [Architecture](https://developers.vtex.com/vtex-rest-api/docs/master-data-architecture).
    - [Starting to work with schemas](https://developers.vtex.com/vtex-rest-api/docs/starting-to-work-on-master-data-with-json-schema).
    - [Schema lifecycle](https://developers.vtex.com/vtex-rest-api/docs/master-data-schema-lifecycle).
- VTEX IO service development
    - [Developing services on VTEX IO](https://learn.vtex.com/docs/course-service-course-lang-en).

### Data structure

You will set up a VTEX IO service app according to [Master Data](https://help.vtex.com/tutorial/master-data--4otjBnR27u4WUIciQsmkAw) basic elements. 

Further along this guide, you will create a folder for each [data entity](https://help.vtex.com/en/tutorial/master-data--4otjBnR27u4WUIciQsmkAw#data-entities) that you want your app to interact with. And for each data entity you use in your project, you must create a corresponding [JSON schema](https://developers.vtex.com/vtex-rest-api/docs/starting-to-work-on-master-data-with-json-schema). See an example schema below:

```json
{
  "$schema": "http://json-schema.org/schema#",
  "title": "my_schema",
  "type": "object",
  "properties": {
    "string_field_example": {
      "type": "string"
    },
    "number_field_example": {
      "type": "number"
    },
    "boolean_field_example": {
      "type": "boolean"
    }
  },
  "required": [
    "number_field_example",
    "string_field_example"
  ],
  "v-default-fields": [
    "number_field_example",
    "string_field_example"
  ]
}
```

We recommend you consider your desired data structure in this context before starting to code your app. Make sure you have your data entities planned and schemas written.


## App setup

To create a [Master Data](https://help.vtex.com/tutorial/master-data--4otjBnR27u4WUIciQsmkAw) app, follow these steps:

1. Use the [VTEX IO CLI](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installation-and-command-reference) command `vtex init` to copy the [service-example](https://github.com/vtex-apps/service-example) boilerplate files to your computer.
2. Add the Master Data builder to your [manifest file](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-manifest).
```json
    …
    “masterdata”: “1.x”,
    …
```
3. Add the following [policies](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-policies) to your app’s `manifest.json` file:
```json
[{
    "name": "outbound-access",
    "attrs": {
        "host": "api.vtex.com",
        "path": "/api/*"
     }
},
{
    "name": "ADMIN_DS"
 }]
```
4. Create a folder named `masterdata` at the root of your app. This will be your Master Data configuration folder.
5. Create a folder with the name of your data entity inside the `masterdata` folder.
6. Create a  file named `schema.json` inside of your data entity folder. The result of steps 4 to 6 should look like this:
```
masterdata
 | --myEntity
       | --schema.json
```
7. Put the [JSON schema](https://developers.vtex.com/vtex-rest-api/docs/starting-to-work-on-master-data-with-json-schema) corresponding to the data entity in the `schema.json` file.
8. Run `vtex link` to make sure everything was set up correctly so far.
9. Run `vtex setup`. This command will generate all typescript typings for your data entity. The typings will be available to be imported from your app. You can find them in your `node/node_modules` folder.

> ⚠️
>
> If you are using a development environment, use `vtex setup -i`.

10. Change directory to the `node` folder of your app.
11. Run `yarn add @vtex/clients` to install the `clients` package.
12. Open the file `node/clients/index.ts` and add the following imports:
```ts
import { masterDataFor } from '@vtex/clients'
import { myEntity } from 'myStore.myApp' // Insert here the names of your data entity, store and app.
```

> ⚠️
>
> - You are importing your data entity typings from the app itself. Identify your app in the format `'{vendor}.{name}'`, according to the information in you `manifest.json`.
> - If your app does not recognize the generated typings import, see the solution presented in the [Typings](#typings) section below.

13. Still on the `node/clients/index.ts` file, you must create a new property for the `Clients` class, which declares a new available client. This represents the data entity you are working with. See this code example:
```ts
public get entity() {
  return this.getOrSet('entity', masterDataFor<myEntity>('entity'))
}
```
### Triggers

To configure [Master Data triggers](https://developers.vtex.com/vtex-rest-api/docs/setting-up-triggers-in-master-data-v2) in the app you created, follow these steps:
1. Create a folder named `triggers` inside your `masterdata/{dataEntity}` folder.
2. Create a JSON file inside the triggers folder.
3. Declare your triggers in the JSON file. They should be in an array in the same format described for the `v-triggers` field when [setting up Master Data v2 triggers](https://developers.vtex.com/vtex-rest-api/docs/setting-up-triggers-in-master-data-v2).

### Typings

Note that whenever you make changes to your data entity schema, you must regenerate the typescript typings.

To generate your data entity typescript typings you must run the command `vtex setup` at the root of your project. Also, before finish coding and release your app, you must run `vtex setup -i` so that the typings will not be tied to your development workspace.

> ℹ️
>
> If you run into issues with the data entity typings generation or import, try generating the typings again.

As described above, your generated data entity typings must be imported from the app itself, like this:
```ts
import { myEntity } from 'myStore.myApp' // Insert here the names of your data entity, store and app.
```

At this point, your app may not recognize the folder created by `vtex setup`, leading to an error in the code. If this happens to you, try these steps:
1. Delete the `node/node_modules` folder.
2. Run `yarn` to reinstall dependencies.
3. Run `vtex setup` to regenerate the typings.
4. Run `vtex link` to check if everything is ok.

### Data entities and schemas

You can set more than one data entity in you app. To do so, create one folder inside the `masterdata` folder for each data entity you wish to create. Each must have its own `schema.json` with a valid [JSON schema](https://developers.vtex.com/vtex-rest-api/docs/starting-to-work-on-master-data-with-json-schema).

Your app creates regular Master Data entities, which can be accessed via the [Master Data v2 endpoints](https://developers.vtex.com/vtex-rest-api/reference/master-data-api-v2-overview). The name of the entity created follows this pattern: `{vendor}_{appName}_{entityName}`.

> ⚠️
>
> Whenever you install or link a different version of your app, the Master Data builder cerates a new schema with the app’s name and version.

## Usage

Now that your app is set up, you can code Master Data functions, such as saving, editing, retrieving or deleting data.

> ℹ️
>
> You may use Master Data functions in your app’s `resolvers` or `middlewares`  folder.

Master Data functions are available via global context, with `ctx.clients.{entityName}.{function}()`. Below you can see more details on each function. These functions are equivalent to those performed by [Master Data v2 endpoints](https://developers.vtex.com/vtex-rest-api/reference/master-data-api-v2-overview).

### Get

The `get()` function returns a document by its ID. You may specify what fields you want to be returned. If you do not, all fields in the document will be returned.

#### Arguments

| **Argument** | **Required** | **Type** | **Description**                                                                                |
|--------------|--------------|----------|------------------------------------------------------------------------------------------------|
| `id`           | Yes          | String   | ID of the document you wish to retrieve.                                                       |
| `fields`       | No           | Array of strings    | List of the names of the fields you wish to be returned. If not sent, all fields are returned. |
#### Examples

Getting a complete document of the `Book` entity.
```ts
ctx.client.Book.get(id: 'sdfg3543df5g4h3d5fh47d')
```

Getting the name and release date of a given book from the `Book` entity.
```ts
ctx.client.Book.get(id: 'sdfg3543df5g4h3d5fh47d’, fields:['name', 'releaseDate'])
```

### Save

The `save()` function saves a new document to your data entity and returns the generated ID for that new document.


#### Arguments

This function’s arguments follow the format you described when setting up JSON schemas in your [data structure](#data-structure).
#### Example

Saving a new document to the `Book` data entity.
```ts
ctx.client.Book.save({
  name: 'Dom Quixote',
  releaseDate: 1605,
  author: 'Miguel de Cervantes'
})
```

### Update

The `update()` function an existing document by ID.

#### Arguments

| **Argument** | **Required** | **Type** | **Description**                                                                                |
|--------------|--------------|----------|------------------------------------------------------------------------------------------------|
| `id`           | Yes          | String   | ID of the document you wish to update.                                                       |
| `{document-data}`      | Yes           | Corresponding to the types declared in the schema    | This function’s arguments follow the format you described when setting up JSON schemas in your [data structure](#data-structure). Required fields apply even for partial updates. |
#### Example

Updating a document’s `rating` field in the `Book` entity.
```ts
ctx.client.Book.udpate(
  id: 'sdfg3543df5g4h3d5fh47d',
  {
    name 'Dom Quixote',
    rating: 4,5
  }
)
```
### Save or update

The `saveOrUpdate()` function updates an existing document by ID or creates a new document if you do not send an ID.

#### Arguments

| **Argument** | **Required** | **Type** | **Description**                                                                                |
|--------------|--------------|----------|------------------------------------------------------------------------------------------------|
| `id`           | No         | String   | ID of the document you wish to update. If you send an ID, the document is updated. Otherwise, a new document is created.                                                       |
| `{document-data}`      | Yes           | Corresponding to the types declared in the schema    | This function’s arguments follow the format you described when setting up JSON schemas in your [data structure](#data-structure). Required fields apply even for partial updates. |
#### Examples

Updating a document’s `rating` field in the `Book` entity.
```ts
ctx.client.Book.saveOrUpdate(
  id: ‘sdfg3543df5g4h3d5fh47d’,
  {
    name ‘Dom Quixote’,
    rating: 4,5
  }
)
```

Saving a new document to the `Book` data entity.
```ts
ctx.client.Book.saveOrUpdate({
  name: 'Dom Quixote',
  releaseDate: 1605,
  author: 'Miguel de Cervantes'
})
```

### Delete

The `delete()` function deletes a document by ID.
#### Arguments

| **Argument** | **Required** | **Type** | **Description**                                                                                |
|--------------|--------------|----------|------------------------------------------------------------------------------------------------|
| `id`           | Yes          | String   | ID of the document you wish to delete.                                                       |

#### Example

Deleting a document of the `Book` entity.
```ts
ctx.client.Book.delete(id: 'sdfg3543df5g4h3d5fh47d')
```

### Search

The `search()` function returns an array of documents that satisfy the criteria described in the arguments.

#### Arguments

| **Argument** | **Required** | **Type**         | **Description**                                                                                |
|--------------|--------------|------------------|------------------------------------------------------------------------------------------------|
| `page`         | Yes          | Integer          | Number of the page you wish to retrieve.                                                       |
| `pageSize`     | Yes          | Integer          | Number of documents that should be returned in each page.                                                |
| `fields`       | No           | Array of strings | Names of the fields you wish to be returned. If not sent, all fields are returned. |
| `where`        | No           | String           | Filtering condition.                                                                           |

#### Example

Searching names and release dates of all books by the author Miguel de Cervantes.
```ts
ctx.client.Book.search(
  pagination: {
    page: 1,
    pageSize: 10
  },
  fields: ['name', 'releaseDate'],
  where: 'name=Miguel de Cervantes'
)
```
