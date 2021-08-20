# Billing Options

The `billingOption` field is part of an app’s `manifest.json` file, which is where all the app’s essential information is kept, such as its name and version. 

We use the `billingOptions` field to define an app’s distribution on the platform and structure its pricing data, allowing the application usage to be public and, in some scenarios, even charged. 

Therefore, **structuring your app's `billingOption` field is a necessary step to distribute your application in the VTEX ecosystem**. An app without the `billingOptions` field in its `manifest.json` implies it is a **private** app and only visible and able to be installed in the account where it was published.

Below you will find more details on the properties that comprise this field.

## Properties

| Property | Type | Description | Valid example | 
| --------- | ----- | --------------- | ------- | 
| `type`  | `enum` | Defines how the app is charged. Possible values are: `free` (app is free of charge), `billable` (app charges according to one of its plans) or `sponsored` (app is meant to be used only by a [Sponsor account](https://vtex.io/docs/concepts/sponsor-account/) and its children). | `free` | 
| `support` | `object` | Provides a support request channel between the app’s user and its vendor. To know more, check out the `support` object section below. | `undefined` | 
| `availableCountries` | `array` | Defines the countries ID (ISO) where the app can be installed and where support is ensured by the vendor. | `["BRA", "USA", "GBR"]` or `["*"]` *(meaning that the app is available in any country)* | 
| `plans` | `array` | **Optional property.** Defines (in an object array) a predefined subscription plan. To know more, check out the `plans` array section below. | `undefined` | 

- **`support` object:**

| Property | Type | Description | Valid example | 
| -------- | ------- | --------- | -------- | 
| `email` | `string` | Email address where users can request support. | `example@example.com` | 
| `url` | `string` | **Optional property.** URL where users can request support. | `example.com/support` | 
| `phone` |  `string` | **Optional property.** Phone number (in full international format) where users can request support. | `+5521988887777` | 

Valid example of the object:

```json
"support": {
  "url": "https://example.com/support",
  "email": "example@example.com",
  "phone": "+5521988887777"
},
```

- **`plans` array:**

| Property | Type | Description | Valid example | 
| -------- | ------- | --------- | -------- | 
| `id` | `string` | Unique plan identifier containing one or more letters or numbers from the english alphabet. | `BRAplan23`, `planShipping` | 
| `currency` | `string` | A valid [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) currency code to be used for the app’s subscription value. Currently, only `BRL` and `USD` are supported. | `BRL`, `USD` | 
| `price` |  `object` | Contains subscription pricing values for the billable app. All values follow the same unit set in the `currency` prop. For more info, check out the `price` object section below. | `undefined` | 

Valid example of the object:

```json
"plans": [{
  "id": "BRAplan23",
  "currency": "BRL",
  "price": {...}  
}]
```

- **`price` object:**

| Property | Type | Description | Valid example | 
| -------- | ------- | --------- | -------- | 
| `subscription` | `number` | The subscription’s *monthly* price. | `19.99` | 
| `metrics` | `array` | Defines (in an object array) the criteria on which the variable fee will be based on, according to the app’s use. Only use this property if you also want to charge your app users according to the app usage (in addition to the subscription fee). To know more, check out the `metrics` object section below. | `undefined` | 

Valid example of the object:

```json
"price" {
  "subscription": 50,
  "metrics": [{...}]
}
```

- **`metrics` array:**

| Property | Type | Description | Valid example | 
| -------- | ------- | --------- | -------- | 
| `id` | `string` | Unique metric identifier (across all metrics within the plan) containing one or more *letters* or *numbers* from the english alphabet. | `CreditMetric23` | 
| `ranges` | `array` | Defines (in an object array) the range used to calculate the app’s use and the variable fee that users should be charged. To know more, check out the `ranges` object section below. | `undefined` | 
| `customURL` | `string` | Reliable `URL` address containing information on how to get the metric value. | `mycredit.com/app/3/metric-value` | 

Valid example of the object:

```json
{
  "id": "notificationSent",
  "ranges": [{...}],
  "customUrl": "https://metrics.com/_v/metric/billing/info"
}
```

- **`ranges` array:**

| Property | Type | Description | Valid example | 
| -------- | ------- | --------- | -------- | 
| `multiplier` | `number` | A positive number that is going to be multiplied by the metric value to calculate the price that will be charged. | `0.07`, `1.99`, `5` | 
| `exclusiveFrom` | `number` | A number that denotes the start of the range (but doesn't include that number itself in the range). | `0`, `100`, `33.33` | 
| `inclusiveTo` | `number` | A number that denotes the end of the range (including that number itself). | `100`, `500`, `999.99` |

Valid example of the object:

```json
"ranges": [{
  "exclusiveFrom": 0,
  "multiplier": 0.08
}]
```

Setting your app's billing model is a necessary step to distribute your app in the VTEX ecosystem. Without them, the visibility of your app is restricted to the account where it was published. Learn how to configure the `billingOptions` field, according to the desired context, in [Setting your app's billing model](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-setting-your-apps-billing-model). 

