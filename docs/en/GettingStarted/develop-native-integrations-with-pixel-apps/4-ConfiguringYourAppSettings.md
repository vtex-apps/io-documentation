# 3. Configuring your app settings

When creating a native integration with a third party solution, it is essential to **link** it with the VTEX account for which you’re doing the integration. Without this link, you won't be able to transfer data between the store and the solution, rendering your Pixel app useless.

Such a link is always done through what we call **user identification**. Made available by the third party solution with which you will enable the integration, user identification is what grants permissions for using the service offered by it.

Think of Google Tag Manager, for example: to use it, you need to have an `ID` previously provided. That’s an example of a user identification, whose value is individual and untransferable, granting you all the needed permissions to actually the solution.

Therefore, the user identification is a key part of the proper functioning of your Pixel app, since it **ensures the integration based on permissions granted to each account**.

The step-by-step below will guide you through the necessary configuration to enable the Pixel app to receive different user identifications and to evaluate whether the integration is allowed or not:

1. Access the the app’s `manifest.json` file.
2. Change the  `vendor` field value  (`vtex`) to the name of the VTEX account in which you are working so that you'll be able to correctly publish the app later on.
3. Change the `name` and `title` field values with the name you wish to give your app. You can check the app-naming best practices [here](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-filling-the-application-form-for-development/#guidelines).
4. Create a new field called `settingsSchema` and declare in it a JSON Schema to receive the needed user identifications. For example:

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

Where:

- `title` is the Pixel app name.
- `type` is the JSON Schema type (this must always be filled in as `object`).
- `description` is an *optional property* that describes the new `settingsSchema` field.
- `properties` is the set of keys that defines the user identification. In the example above, the app user identification is `gtmId`. Possible keys for `properties` are: `title` (user identification title), `description` (user identification description), and `type` (property type to define how users should input their identifications). Notice that these keys will be displayed to the app's users.

If needed, you can also add more than one app user identification in the `properties` object. For example:

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
    "popupLayout": {
      "title": "Pop up layout",
      "type": "string",
      "default": "top",
      "enum": [
        "top",
        "bottomLeft",
        "right"
      ],
      "enumNames": [
        "Top",
        "Bottom left",
        "Right"
      ]
    },
  }
},
```

In the example above, we added a new app user identification called `popupLayout`. 

>ℹ️ Do not forget to learn more about [JSON Schema](http://json-schema.org/understanding-json-schema/) before building your app's `settingSchema` field.

