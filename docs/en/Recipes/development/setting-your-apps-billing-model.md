---
title: Setting your app's billing model
description: "Define who can install your app and if its usage will be charged and, if so, how much it will cost for the interested accounts."
date: "2021-03-30"
tags: ["billing", "model", "app", "distribution", "monetization", "change"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/edit/master/docs/en/Recipes/development/setting-your-apps-billing-model.md"
---

# Setting your app's billing model

Once your app has been developed and is ready to go live, it's time to think about its distribution. In this step, you must define who will be allowed to install your app, whether your app will be paid or not, and how much it will cost if so.

When preparing your app for distribution, you must first establish if your new app will be private or public on the VTEX IO platform. 
- **Private apps** can only be installed by their `vendor` account  (i.e., the account responsible for the app's development and maintenance). 
- **Public apps** are available to all accounts of the VTEX IO ecosystem. These apps can be charged or not. 

## Setting the app as private

Take the following steps to make your app private:

### Step by step

1. Open your project in any code editor of your preference.
2. Open the `manifest.json` file and remove the `billingOptions` field.

Without `billingOptions`, VTEX IO will understand that the app in question should not be made available to any account other than the one specified in the `vendor` field of the `manifest.json` file. 

## Setting the app as public

When making your app public available to the entire VTEX IO ecosystem, you must set up the `billingOptions` field in the app's [`manifest.json`](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-manifest) file. In this context, you will need to:

- Define whether or not the app will be charged.
- Register the use of metrics _(Only for apps with a variable pricing strategy)_.
- Register the `metrics` data _(Only for apps with a variable pricing strategy)_.

For more information, please refer to the [`billingOptions` documentation](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-billing-options).

### Step 1 - Setting the app's pricing strategy

A public app can be charged or not. Take the following steps according to your scenario.

#### Setting the app as free

1. Open your app in any code editor of your preference.
2. Open the `manifest.json` file.
3. Add the `billingOptions` field to your app's `manifest.json` file and set the `type` property as `free`.
5. Set up the `support` property to provide a support channel for the app users.
6. Set up the `availableCountries` property to define in which countries the app will be available.

```json
  "billingOptions": {
    "type": "free",
    "support": {
        "email": "support@com.br",
        "url": "https://support.com/hc/requests",
      },
    "availableCountries" : ["*"]
  }
```

>ℹ️ The `*` value stands for all countries.

#### Setting the app as charged

1. Open your app in any code editor of your preference.
2. Open the `manifest.json` file.
3. Create the `billingOptions` field in the app's `manifest.json` file and set the `type` property as `billable`.
4. Set up the `support` property to provide a support channel for the app users.
5. Set up the `availableCountries` property to define in which countries the app will be available.

```json
  "billingOptions": {
    "type": "billable",
    "support": {
        "email": "support@com.br",
        "url": "https://support.com/hc/requests",
      },
    "availableCountries" : ["*"]
  }
```

7. Now, choose one of the following billing options and follow the procedures corresponding to your selection.
  - [**Fixed subscription**](#fixed-subscription) - Charges a fixed subscription price per month. This billing model only allows a single subscription plan to be created for the app.
  - [**Fixed subscription + Variable rate**](#fixed-subscription--variable-rate) - Charges a fixed subscription price plus a variable charge based on the app's usage.
  - [**Variable subscription + Variable rate**](#variable-subscription--variable-rate) - Charges a variable subscription price plus a variable rate based on the app's usage.

##### Fixed subscription

Establish a subscription plan for your app by setting up the `plan` property and its child properties: 
- `id`: Plan identifier.
- `currency`: Currency code following the ISO.
- `price.subscription`: Subscription price.

For example:

```json
    "billingOptions": {
      "type": "billable",
      "support": {
        "email": "support@com.br",
        "url": "https://support.com/hc/requests",
      },
      "availableCountries": ["*"],
      "plans": [{
        "id": "PlanBRL",
        "currency": "BRL",
        "price": {
          "subscription": 100
        }
      }]
    }
```

##### Fixed subscription + variable rate

1. Establish a subscription plan for your app by setting up the `plan` property and its child properties:
  - `id`: Plan identifier.
  - `currency`: Currency code following the ISO.
  - `price.subscription`: Subscription price.
  - `price.metrics`: An array specifying the metric's id and the ranges related to the app's usage and associated extra charge. Notice that you can set one or more metrics to calculate the variable rate.

<details>
  <summary>Example of an app with a fixed subscription price plus a variable rate that considers only one metric</summary>

```json
  "billingOptions": {
    "type": "billable",
    "support": {
      "email": "support@com.br"
    },
    "availableCountries": ["*"],
    "plans": [{
      "id": "PlanUSD",
      "currency": "USD",
      "price": {
        "subscription": 50,
        "metrics": [{
          "id": "smsSent",
          "ranges": [{
              "exclusiveFrom": 0,
              "inclusiveTo": 2000,
              "multiplier": 0.07
            },
            {
              "exclusiveFrom": 2000,
              "inclusiveTo": 4000,
              "multiplier": 0.06
            },
            {
              "exclusiveFrom": 4000,
              "multiplier": 0.05
            }
          ]
        }]
      }
    }] 
  }
```

From the previous example, we have:

- Each SMS costs `US$ 0.07` when more than `0` (`exclusiveFrom: 0`) SMSs _and_ less than or equal to `2000` (`inclusiveTo: 2000`) SMSs have already been sent.
- Each SMS costs `US$ 0.06` when more than `2000` (`exclusiveFrom: 2000`) _and_ less than or equal to `4000` (`inclusiveTo: 4000`) SMSs have already been sent.
- Each SMS costs `US$ 0.05` when more than `4000` (`exclusiveFrom: 4000`) SMSs have already been sent.

Therefore, the extra variable rate would be charged as follows:

- For 1500 SMSs =  US$ 30.00 *(1500 x US$ 0.07 = US$ 30.00)*
- For 3500 SMSs = US$ 60.00 *(3500 x US$ 0.06 = US$ 60.00)*
- For 7000 SMSs = US$ 100.00 *(7000 x US$ 0.05 = US$ 100.00)*

</details>

<details>
  <summary>Example of an app with a fixed subscription price plus a variable rate that considers more than one metric</summary>

```json
    "billingOptions": {
      "type": "billable",
      "support": {
        "url": "https://support.com/hc/requests",
        "email": "support@com.br",
        "phone": "+5521988887777"
      },
      "availableCountries": ["USA", "GBR", "BRA", "ESP"],
      "plans": [{
          "id": "PlanUSD",
          "currency": "USD",
          "price": {
            "subscription": 50,
            "metrics": [{
                "id": "myCredits",
                "ranges": [{
                    "exclusiveFrom": 0,
                    "multiplier": 1,
                    "inclusiveTo": 100
                  },
                  {
                    "exclusiveFrom": 100,
                    "multiplier": 0.7
                  }],
                "customUrl": "https://my.com/_v/metric/billing/info"
              },
              {
                "id": "myCredit2",
                "ranges": [{
                  "exclusiveFrom": 0,
                  "multiplier": 0.5
                }],
                "customUrl": "https://my.com/_v/metric/billing/info"
              }
            ]
          }
      }]
    }  
```
</details>

2. Create the `policies` field in the app's `manifest.json` file and add the `vtex.billing:save-metrics` as its child.
3. Make a POST request to `https://app.io.vtex.com/vtex.billing/v0/{account}/{workspace}/_v/billing-metrics` with the following body:

```
{
 metric_id: {metricId},
 value: {metricAmount},
}
```

Remember to remove the curly brackets from the endpoint and body replacing them with real values according to your own scenario.
- `account` - VTEX account responsible for the app development and maintenance.
- `Workspace` - Workspace being used for the app development.
- `metricId` - ID of the metric specified in the `billingOptions` field.
- `metricAmount` - Use of metrics for billing. For example: if your metric consists of charging for each SMS sent, the `metricAmount` should be equal to 1.

##### Variable subscription + variable rate 

1. Establish a subscription plan for your app by setting up the `plan` property and its child properties:
  - `id`: Plan identifier.
  - `currency`: Currency code following the ISO.
  - `price.subscription`: Subscription price.
  - `price.metrics`: An array specifying the metric's id and the ranges related to the app's usage and associated extra charge. Notice that you can set one or more metrics to calculate the variable rate.
2. Repeat the previous step to create a new subscription plan. This new plan will be a new object inside the `plan` array.
  
<details>
  <summary>Example of an app with a variable subscription and variable rate</summary>

```json
    "billingOptions": {
      "type": "billable",
      "support": {
        "url": "https://support.com/hc/requests",
        "email": "support@com.br",
        "phone": "+5521988887777"
      },
      "availableCountries": ["GBR", "BRA", "ESP"],
      "plans": [{
          "id": "PlanBRL",
          "currency": "BRL",
          "price": {
            "subscription": 50,
            "metrics": [{
                "id": "myCredits",
                "ranges": [{
                    "exclusiveFrom": 0,
                    "multiplier": 1,
                    "inclusiveTo": 100
                  },
                  {
                    "exclusiveFrom": 100,
                    "multiplier": 0.7
                  }
                ],
                "customUrl": "https://my.com/_v/metric/billing/info"
              },
              {
                "id": "myCredit2",
                "ranges": [{
                  "exclusiveFrom": 0,
                  "multiplier": 0.5
                }],
                "customUrl": "https://my.com/_v/metric/billing/info"
              }
            ]
          }
        },
        {
          "id": "PlanUSD",
          "currency": "USD",
          "price": {
            "subscription": 50,
            "metrics": [{
                "id": "myCredits",
                "ranges": [{
                    "exclusiveFrom": 0,
                    "multiplier": 1,
                    "inclusiveTo": 100
                  },
                  {
                    "exclusiveFrom": 100,
                    "multiplier": 0.7
                  }
                ],
                "customUrl": "https://my.com/_v/metric/billing/info"
              },
              {
                "id": "myCredit2",
                "ranges": [{
                  "exclusiveFrom": 0,
                  "multiplier": 0.5
                }],
                "customUrl": "https://my.com/_v/metric/billing/info"
              }
            ]
          }
        }
      ]
    }
  }
```

</details>
  
3. Create the `policies` field in the app's `manifest.json` file and add the `vtex.billing:save-metrics` as its child.
4. Make a POST request to `https://app.io.vtex.com/vtex.billing/v0/{account}/{workspace}/_v/billing-metrics` with the following body:

```
{
 metric_id: {metricId},
 value: {metricAmount},
}
```

Remember to remove the curly brackets from the endpoint and body replacing them with real values according to your own scenario.
- `account` - VTEX account responsible for the app development and maintenance.
- `Workspace` - Workspace being used for the app development.
- `metricId` - ID of the metric specified in the `billingOptions` field.
- `metricAmount` - Use of metrics for billing. For example: if your metric consists of charging for each SMS sent, the `metricAmount` should be equal to 1.

### Step 2 - Register the use of `metrics`  (Only for apps with a variable pricing strategy)

If you opted for a pricing strategy with a variable rate, you must guarantee that your metrics are being registered and updated over time. Not registering the metric values or updating them correctly means the app's users will not be charged the right value.

VTEX App Store provides the APIs and the infrastructure to register and keep the app's metric data. However, the app is responsible to guarantee that these values are correctly updated over time.


To explain how to register these metric values, we will use the SMS Sender app as an example. If your app does not have any metric item, there's no need to register.

**SMS Sender `billingOptions` example** (*manifest.json*)

This app has an item that is charged according to a metric value. That metric charges `BRL 0.07` (defined in `multiplier`) for *each* metric used:

```json
{
  ...
  "billingOptions": {
    ...
    "plans": [
      {
        ...
        "price": {
          "metrics": [
            {
              "id": "smsSent",
              "ranges": [
                {
                  "exclusiveFrom": 0,
                  "multiplier": 0.07
                }
              ]
            }
          ]
        }
      }
    ]
  }
  ...
}
```

### Step 3 - Registering the `metrics` data (Only for apps with a variable pricing strategy)

The app's metric values consumption must be registered in order to users be charged correctly.

1. Create a client for the `billing` app or complement it with the `saveBillingMetric` method:

```ts
import {AppClient, IOContext, InstanceOptions} from '@vtex/api'

const routes = {
  billingMetrics: `/_v/billing-metrics`,
}

export class BillingApp extends AppClient {
  public constructor(ioContext: IOContext, opts?: InstanceOptions) {
    super('vtex.billing@0.x', ioContext, opts)
  }

  public saveBillingMetric = (billingMetric: {
    metric_id: string
    value: number
  }) =>
    this.http.post(routes.billingMetrics, billingMetric, {
      metric: 'save-billing-metric',
    })
}
```

2. Call the `saveBillingMetric` method whenever you need to add (it is accumulative) a new quantity in the metric value:

```ts
async function saveSMSBillingMetric(
  {clients: {billingApp}, vtex: {logger}}: ServiceContext<Clients>,
  res: SMSInfo,
) {
  try {
    await billingApp.saveBillingMetric({
      metric_id: 'smsSent', // metric_id is defined in the app's billingOptions
      value: 1, // value is a whole/integer number that you want to register. This is accumulative.
    })
  } catch (e) {
    // That was an error trying to save the metric value
  }
}
```
After the steps above, you are all set. Now VTEX App Store will use all the saved billing metrics, registered by the method `saveBillingMetric`, according to each month to charge the app's users. It is not necessary to inform the date associated with each metric record because it will be used is implicitly defined. 

Each time a metric is saved, it is also recorded the date for each registry, and by the end of the month/cycle, it is known what metrics will be charged within a given date interval.

>ℹ️ You can [contact the VTEX support team](https://help.vtex.com/tutorial/opening-tickets-to-vtex-support--16yOEqpO32UQYygSmMSSAM) to get more information about the contracts and accounts that have installed your app.
