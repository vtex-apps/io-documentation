---
title: Creating a native form for your store users
description: "Learn how to display a 100% native form component which is integrated with VTEX Master Data."
date: "2020-04-09"
tags: ["form", "master-data", "store-form", "native"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/templates/creating-a-native-form-for-your-store-users.md"
---

# Creating a native form for your store users

Many brick and mortar stores assign the task of developing the brand's relationship with customers to their sales team, encouraging a closer relationship between customers and sales reps for any necessary support.

It goes without saying that this is not the case for online stores. Without a familiar face to accompany their navigation, as would be the case in a brick and mortar store, users can often feel helpless or the lack of **somewhere to voice their questions and suggestions**.

In such scenarios, forms become essential tools for an ecommerce store, as they **promote clear and direct communication** with customers.

A form may give a greater amount of information about your users, as well as more insight into satisfaction levels with the service being offered.
 
With VTEX IO Store Framework, your store can have a 100% native form component which is integrated with [**VTEX Master Data**](https://help.vtex.com/tutorial/what-is-master-data--4otjBnR27u4WUIciQsmkAw?locale=en).
  
## Step by step

### Step 1 - Creating the JSON Schema in Master Data

The first step is to create a [JSON schema](https://json-schema.org/understanding-json-schema/index.html) in VTEX Master Data to work with the native form.

The created schema will be responsible for telling your form fields which data they must receive i.e. which kind of input they should expect from users.

In addition, the schema will also be responsible for saving all user data fetched from the form in a Master Data's Data Entity.

You can create it using [Master Data v1](https://help.vtex.com/tutorial/what-is-master-data--4otjBnR27u4WUIciQsmkAw) or [Master Data V2](https://help.vtex.com/tutorial/master-data-v2--3JJ1mlzuo88w22gO0gy0QS).

#### Using Master Data v1

When creating the JSON Schema using Master Data v1, all properties needed for the schema must be previously created as fields in a Data Entity of your choosing.

To that end, we will use the admin's Master Data legacy interface:

1. Access the VTEX account's admin in which you are working and access its Master Data section;
2. [Create all required fields](https://help.vtex.com/tutorial/how-can-i-create-field-in-master-data--frequentlyAskedQuestions_1829?locale=en) in the desired Data Entity. If you do not need to add any extra fields, please move on to step 5 to create your schema;
3. Run the [`Get Schemas` API](https://developers.vtex.com/reference/schemas#getschemas), replacing the `data_entity_name` value with `CL`;
4. In the response, look for the schema named `mdv1`. This schema is automatically created based on the Master Data v1 existing fields. Find the fields added in step 2 and copy the structures in which these are displayed to the `mdv1` schema. This will help you in the next step when you'll create another JSON Schema for the form including those fields as properties;
5. Send a request to Master Data's [`Save Schema by name`](https://developers.vtex.com/reference/schemas#saveschemabyname) API, copying the following example in the request's body and using it as a default when making any required changes to the properties (according to your store’s scenario):
  
```json
{
  "title": "Person",
  "type": "object",
  "properties": {
    "firstName": {
      "type": "string",
      "title": "First Name",
      "description": "The person's first name."
    },
    "lastName": {
      "type": "string",
      "title": "Last Name",
      "description": "The person's last name."
    },
    "age": {
      "description": "Age in years which must be equal to or greater than zero.",
      "title": "Age",
      "type": "integer",
      "minimum": 0,
      "maximum": 120
    },
    "height": {
      "type": "number",
      "minimum": 0.3,
      "maximum": 2.9,
      "title": "Your height in meters",
      "multipleOf": 0.01
    },
    "emailAddress": {
      "type": "string",
      "format": "email",
      "title": "Email address"
    },
    "address": {
      "title": "Address",
      "type": "object",
      "properties": {
        "streetType": {
          "type": "string",
          "title": "Street Type",
          "enum": [
            "street",
            "road",
            "avenue",
            "boulevard"
          ]
        },
        "streetAddress": {
          "type": "string",
          "title": "Address"
        },
        "streetNumber": {
          "type": "integer",
          "title": "Street Number"
        }
      },
      "required": [
        "streetType", "streetAddress", "streetNumber"
      ]
    },
    "agreement": {
      "type": "boolean",
      "title": "Do you agree with the terms?"
    }
  },
  "required": [
    "firstName",
    "lastName",
    "agreement"
  ],
  "v-security": {
    "publicJsonSchema": true,
    "allowGetAll": false,
    "publicRead": [ "fieldExemple" ],
    "publicWrite": [ "fieldExemple" ],
    "publicFilter": [ "fieldExemple" ]
  }
}
```

>ℹ️ Bear in mind that the schema's language will define the form's default language as well.

When configuring the API to create the JSON Schema, remember to:

- Replace the `data_entity_name` value with the Master Data's Data Entity acronym in which you want to save the user data fetched from the form;
- Replace the `schema_name` value with a name of your choosing. The value defined will be the form's JSON Schema name.

>ℹ️ If you have difficulty in setting up the JSON Schema properties based on Master Data fields, remember to use the schema structure for Master Data's fields copied in step 4.

Once the API was executed successfully, the JSON Schema is ready and you can already create the form in your store's theme.

#### Using Master Data v2

When using Master Data v2, you will not need to previously create any field. Simply send a request to the Master Data [`Save Schema by name`](https://developers.vtex.com/reference/schemas#saveschemabyname) API, copying the following example in the request's body and using it as a default when making any required changes to the properties (according to your store’s scenario):

```json
{
  "title": "Person",
  "type": "object",
  "properties": {
    "firstName": {
      "type": "string",
      "title": "First Name",
      "description": "The person's first name."
    },
    "lastName": {
      "type": "string",
      "title": "Last Name",
      "description": "The person's last name."
    },
    "age": {
      "description": "Age in years which must be equal to or greater than zero.",
      "title": "Age",
      "type": "integer",
      "minimum": 0,
      "maximum": 120
    },
    "height": {
      "type": "number",
      "minimum": 0.3,
      "maximum": 2.9,
      "title": "Your height in meters",
      "multipleOf": 0.01
    },
    "emailAddress": {
      "type": "string",
      "format": "email",
      "title": "Email address"
    },
    "address": {
      "title": "Address",
      "type": "object",
      "properties": {
        "streetType": {
          "type": "string",
          "title": "Street Type",
          "enum": [
            "street",
            "road",
            "avenue",
            "boulevard"
          ]
        },
        "streetAddress": {
          "type": "string",
          "title": "Address"
        },
        "streetNumber": {
          "type": "integer",
          "title": "Street Number"
        }
      },
      "required": [
        "streetType", "streetAddress", "streetNumber"
      ]
    },
    "agreement": {
      "type": "boolean",
      "title": "Do you agree with the terms?"
    }
  },
  "required": [
    "firstName",
    "lastName",
    "agreement"
  ],
  "v-security": {
    "publicJsonSchema": true,
    "allowGetAll": false,
    "publicRead": [ "fieldExample" ],
    "publicWrite": [ "fieldExample" ],
    "publicFilter": [ "fieldExample" ]
  }
}
```

>ℹ️ Bear in mind that the schema's language will define the form default language as well.

When configuring the API to create the JSON Schema, remember to:

- Replace the `data_entity_name` value with the Master Data's Data Entity name in which you want to save the user data fetched from the form;
- Replace the `schema_name` value with a name of your choosing. The value defined will be the form's JSON Schema name.
Once the API was executed successfully, the JSON Schema is ready and you can already create the form in your store's theme.

>ℹ️ Notice that Master Data v2 doesn't have an interface yet, so all actions regarding the user form must be done through <a href="https://developers.vtex.com/reference/master-data-api-v2-overview">APIs</a>.

### Step 2 - Configure the Store Form app

Lastly, it's time to configure the Store Form app and the blocks it exports in order to make your store render the native Store Framework form component.

Access the [Store Form app documentation](https://developers.vtex.com/vtex-developer-docs/docs/vtex-store-form) and follow the step-by-step to complete its configuration.

Once the form is configured in your store's theme, users will be able to share their information using the component. And the best part is that your store will be able to receive this information and automatically save it in Master Data.
