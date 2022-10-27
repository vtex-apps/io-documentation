---
title: Creating a product availability form
description: "Make a product availability form available whenever your store's products are displayed as unavailable."
date: "2021-08-11"
tags: ["availability subscriber", "product availability", "form"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/edit/master/docs/en/Recipes/templates/creating-a-product-availability-form.md"
---

# Creating a product availability form

While browsing through a store's catalog, the user may feel disappointed if they are interested in a product not available for purchase at the moment.

To avoid frustration, you can make a product availability form available whenever your store's products are displayed as unavailable. Therefore, users can fill out a form linked to the product, expressing their interest in requesting the purchase as soon as the product is available again.

To set up the product availability form, follow the step-by-step below. 

>⚠️ This configuration does not include sending automatic e-mails to users. The product availability form only stores the user data filled out in the form to the store's Master Data entity. 



## Step by step

### Step 1 - Creating a Master Data entity

The first step is to create a new entity in the VTEX [Master Data module](https://help.vtex.com/tutorial/what-is-master-data--4otjBnR27u4WUIciQsmkAw?locale=en), responsible for creating database architectures for a store.

The new module’s entity will cover the set of user data filled in and sent in the availability form. Therefore, your first step is to [create a new Master Data entity](https://help.vtex.com/tutorial/creating-data-entity--tutorials_1265). 

It must be named  `AS` and contain the fields stated above to properly work with the form: 

| Field name | Field type |
| ------| ------ | 
| `skuId`  | `Integer` | 
| `name`   | `Text` | 
| `email`  | `Email` |
| `notificationSend` | `Boolean` |                                     |
| `createdAt`   | `Varchar 100` |
| `sendAt`     | `Varchar 100` |

### Step 2 - Creating the JSON Schema in Master Data

Once you created the entity to work with the form correctly, it is time to define how it will communicate with the availability form, which will happen through a [JSON schema](https://json-schema.org/understanding-json-schema/).

The JSON schema will be responsible for telling your form fields which data they must receive, i.e., which kind of input they should expect from users according to the Master Data entity's fields.

In addition to that, the schema will also be responsible for saving all user data fetched from the form in the Master Data's Entity  `AS` created in the previous step.

1.  Using a tool of your preference,  run the  Master Data's [Get Schemas](https://developers.vtex.com/reference/schemas#getschemas) API, replacing the  `data_entity_name`  value with `AS`;
2.  In the response, look for fields added previously to the entity and copy the structures in which these are being displayed. This will help you to create another JSON Schema for the form, including those fields now as properties;
3.  Run the Master Data's  [Save Schema by name](https://developers.vtex.com/reference/schemas#saveschemabyname)  API, pasting the schema structure copied in the second step in the request's body. Remember that this schema structure is using the entity fields, and you should replace them for the schema's properties as stated in the example below:

```JSON
{
  "title": "Person",
  "type": "object",
  "properties": {
    "skuID": {
      "type": "string",
      "title": "SKU ID",
      "description": "The SKU ID desired by user, which will be watched for changes in the product quantity."
    },
    "name": {
      "type": "string",
      "title": "User's name",
      "description": "The user's name."
    },
    "email": {
      "type": "string",
      "title": "User's email",
      "description": "The user's email."
    },
    "notificationSend": {
      "type": "string",
      "title": "Availability notification",
      "description": "Whether the availability notification has been already sent or not."
    },
    "createdAt": {
      "type": "string",
      "title": "Form creating.",
      "description": "Date when the form was created. e.g.: ISO (2011-10-05T14:48:00.000Z)."
    },
    "sendAt": {
      "type": "string",
      "title": "User notification",
      "description": "Date when the user was notified regarding the product availability. e.g.: ISO (2011-10-05T14:48:00.000Z)."
    }
  },  
  "v-security": {
    "publicWrite": [ "publicForWrite" ],
    "publicJsonSchema": true
  }
}
```

This will create the JSON Schema, which the Availability Subscriber block will use, a native component from Store Framework, to store the users’ data in the Master Data entity `AS`. 

### Step 3 - Configure the Availability Subscriber block

Lastly, it is time to configure the Availability Subscriber block to make your store render the native Store Framework component for an availability form. 

Access the  [Availability Subscriber app documentation](https://developers.vtex.com/vtex-developer-docs/docs/vtex-store-components-availabilitysubscriber)  and follow the step-by-step to complete its configuration.

Once the availability form is configured in your store, users interested in unavailable products will be able to share their e-mails using the component. 

The best part about it is that your store will receive this data and automatically save it in Master Data for subsequent communication actions.
