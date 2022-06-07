# 3. Configuring your app settings

When developing a Pixel app, you must define a way to identify whether or not a VTEX account has the necessary permissions to communicate with the third-party solution in question. Otherwise, sharing data between the store and the solution won't be possible.

This verification is generally performed via a user identification issued by the third-party solution. The user identification is an individual and untransferable value that identifies if you have the required permissions to use that solution. Think of the Google Tag Manager Pixel app: in order to use it, you must provide a user identification previously issued. 

In the following step by step, you'll learn how to make your Pixel app read the user identification and determine whether or not a user is allowed.

## Step by step

1. Open the `manifest.json` file.
2. Change the  `vendor` field value (`vtex`) to the name of the VTEX account in which you are working.
3. Change the `name` and `title` field values with the name you wish to give your app. Please refer to our [app-naming guidelines](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-filling-the-application-form-for-development/#guidelines).
4. Declare the `settingsSchema` field. This field will be used to receive the user identification information.
5. Inside the `settingsSchema` object, declare a JSON Schema containing the following fields:

- `title` - Pixel app name.
- `type` - JSON Schema type (this must always be filled in as `object`).
- `description` *(Optional)*  - Description of the `settingsSchema` field.
- `properties` - Set of keys that defines the user identification. Possible keys for `properties` are: `title` (user identification title), `description` (user identification description), and `type` (property type to define how users should input their identifications). Notice that these keys will be displayed to the app's users.

```json
"settingsSchema": {
  "title": "YOUR APP NAME",
  "type": "object",
  "properties": {
    "gtmId": {
      "title": "SAMPLE FIELD",
      "description": "Enter the ID (GTM-XXXX) from your Google Tag Manager",
      "type": "string"
    }
  }
},
```

If needed, you can also use the `properties` object to read the user preferences. Check the following example: 

```json
"settingsSchema": {
  "title": "YOUR APP NAME",
  "type": "object",
  "properties": {
    "gtmId": {
      "title": "SAMPLE FIELD",
      "description": "Enter the ID (GTM-XXXX) from your Google Tag Manager",
      "type": "string"
    },
    "allowCustomHtmlTags": {
        "title": "Allow Custom HTML tags",
        "description": "Beware that using Custom HTML tags can drastically impact the store's performance",
        "type": "boolean"
    }
  }
},
```

>ℹ️ Please refer to the [JSON Schema documentation](http://json-schema.org/understanding-json-schema/) while building your app's `settingSchema` field.

