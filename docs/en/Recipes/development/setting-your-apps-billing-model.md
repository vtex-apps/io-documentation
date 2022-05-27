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
- Register the use of metrics.
- Register metric data.

For more information, please refer to the [`billingOptions` documentation](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-billing-options).

### Step by step

#### Step 1 - Setting the app's pricing

##### Setting the app as free

1. Open your app in any code editor of your preference.
2. Open the `manifest.json` file.
3. Add the `billingOptions` field to your app's `manifest.json` file with the `type` property set as `free`.
4. Provide a support channel for the app users, using the `support` property.
5. Define in which countries the new app can be made available using the `availableCountries` property, as shown in the example below:

```json
  "billingOptions": {
    "type": "free",
    "availableCountries" : ["*"]
  }
```

According to the specified countries, your app can be installed in any VTEX account by any admin user of it.

>ℹ️ The `*` value stands for all countries.

##### Setting the app as charged

 When you decide to charge for your app, you will need to add more properties to the `billingOptions` field to set the desired **billing template**. 
  
There are three possible billing templates on the VTEX IO platform:
 
- **Fixed Subscription** - Charges a fixed monthly amount.
- **Fixed Subscription + Variable Rate** - Charges a fixed monthly amount and a variable rate according to the use of the app.
- **Variable Subscription + Variable Rate** - Charges a different amount per month according to the use of the app, in addition to a variable rate also defined according to its use.

###### Fixed Subscription

1. Open your app code in your code editor.
2. Open the `manifest.json` file.
3. Create the `billingOptions` field in the app's `manifest.json` file.
4. Set the `type` property as `billable`.
5. Provide a support channel for the app users, using the `support` property.
6. Specify to which countries the new app will be available using the `availableCountries` property.
7. Establish a subscription plan for your app with the `plan` property and its child properties: `id` (establishing a plan identifier), `currency` (choosing the currency code to be applied according to the ISO), `price`, and `subscription` (both defining the subscription price). 

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

>ℹ️ This billing model only allows a single subscription plan to be created for the app.

###### Fixed subscription + variable rate

1. Open your app code in your code editor.
2. Open the `manifest.json` file.
3. Create the `billingOptions` field in the app's `manifest.json` file.
4. Set the `type` property as `billable`.
5. Provide a support channel for the app users, using the `support` property.
6. Define in which countries the new app will be made available using the `availableCountries` property.
7. Establish a subscription plan for your app with the `plan` property and its child properties: `id` (establishing a plan identifier), `currency` (choosing the currency code to be applied according to the ISO), `price`, `metrics`, and `subscription` (all three of them defining the subscription price). 
8. In the `metrics` array, establish your metric's `id` and also the use range of the app to apply the metric for the extra charge (`ranges`).

>ℹ️ Note: by using this billing model, you can set one or more metrics (`metrics`) to calculate the variable rate as you want.

Example of an app with only one metric:

```json
  "billingOptions": {
    "type": "billable",
    "support": {
      "email": "support@com.br"
    },
    "availableCountries": ["*"],
    "plans": [{
      "id": "PlanBRL",
      "currency": "BRL",
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

Reading the above code, we understand that:

-   Fore more than  `0`  (`exclusiveFrom: 0`) SMSs sent  _and_  less or equal than  `2000`  (`inclusiveTo: 2000`), each SMS sent costs  `R$ 0.07`;
-   Fore more than  `2000`  (`exclusiveFrom: 2000`) SMSs sent  _and_  less or equal than  `4000`  (`inclusiveTo: 4000`), each SMS sent costs  `R$ 0.06`;
-   Fore more than  `4000`  (`exclusiveFrom: 4000`), each SMS sent costs  `R$ 0.05`.

According to this metrics, the extra variable rate will be charged as follows:

- For 1500 SMSs sent =  US$ 30.00 *(1500 x R$ 0.07 = R$ 105.00 = US$ 30.00)*
- For 3500 SMSs sent  = US$ 60.00 *(3500 x R$ 0.06 = R$ 210.00 = US$ 60.00)*
- For 7000 SMSs sent = US$ 100.00 *(7000 x R$ 0.05 = R$ 350.00 = US$ 100.00)*

Example of an app with more than one metric:

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

Notice that the `metrics` property is key to this model. It is responsible for defining, within its array, how the additional variable rate will be calculated for the subscription plan to which it is linked (`plans`). 

When you finish entering the desired metrics in the `billingOptions` field, you must also add them on the VTEX. It is a fundamental step for the platform to correctly charge for the use of your application. To add the desired metrics:

1. Add `vtex.billing:save-metrics` to the `policies` field of the app's `manifest.json` file. If the field does not yet exist in the file, create it.
2. Make a POST call to the endpoint `https://app.io.vtex.com/vtex.billing/v0/{account}/{workspace}/_v/billing-metrics` with the following body:

```api
{
 metric_id: {metricId},
 value: {metricAmount},
}
```

In which: 

- `account` - VTEX account responsible for the app development and maintenance.
- `Workspace` - Workspace being used for the app development.
- `metricId` - ID of the metric you want to add to the platform. The identifier must be the same set in the `billingOptions` field.
- `metricAmount` - Use of metrics for billing. For example: if my metric consists of charging for each SMS sent, the `metricAmount` should be equal to 1.

>⚠️ Remember to remove the curly brackets from the endpoint and body, replacing them with real values according to your own scenario.

###### Variable subscription + variable rate 

1. Open your app code in your code editor.
2. Open the `manifest.json` file.
3. Create the `billingOptions` field in the app's `manifest.json` file.
4. Set the `type' property to `billable`;
5. Provide a support channel for the app users, using the `support' property;
6. Define in which countries the new app can be distributed using the `availableCountries` property;
7. Establish a subscription plan for your app with the `plan` property and its child properties: `id` (establishing a plan identifier), `currency` (choosing the currency code to be applied according to the ISO), `price`, `metrics`, and `subscription` (all three of them defining the subscription price). 
8. In the `metrics` array, establish your metric's `id` and also the use range of the app to apply the metric for the extra charge (`ranges`).
9. Declare a new array for the `plans` property, using its sub-properties to set up what the new subscription plan will be.

>ℹ️ The metrics stated in step 6 refer to the subscription plan created in the previous step (5). Since we want the subscription value to be variable, that is, change according to the use of the app, we need to create another array for `plans`, indicating new `id`, `currency` and `price`.

10. Repeat step 6 for the new plan: define the `metrics` property array according to the required charge for app usage.

For example: 

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

>ℹ️ Note that this billing model works the same as the previous one (Fixed Subscription + Variable Rate), stating one or more metrics to define the value of the additional variable rate. The difference is that, in this case, we want the subscription to be variable as well, change according to the use of the app. To do this, we add an array of the `plans` property.

Notice that the `metrics` property is key to this model. It is responsible for defining, within its array, how the additional variable rate will be calculated for the subscription plan to which it is linked (`plans`). 

When you finish declaring the metrics you want in the `billingOptions` field, you must add them on VTEX. It is a fundamental step for the platform to charge for the use of your application. To add the desired metrics:

1. Add `vtex.billing:save-metrics` to the `policies` field of the app's `manifest.json` file. If the field does not exist in the file yet, create it.
2. Make a POST call to the endpoint `https://app.io.vtex.com/vtex.billing/v0/{account}/{workspace}/_v/billing-metrics` with the following body:

```api
{
 metric_id: {metricId},
 value: {metricAmount},
}
```

In which: 

- `account` - VTEX account responsible for app development and maintenance.
- `workspace` - Workspace being used by the app development.
- `metricId` - ID of the metric you want to add to the platform. The identifier must be the same set in the `billingOptions` field.
- `metricAmount` - Use of metrics for billing. For example: if my metric consists of charging for each SMS sent, the `metricAmount` should be equal to 1.

>⚠️ Remember to remove the curly brackets from the endpoint and body, replacing them with real values according to your own scenario.

#### Step 2 - Registering the use of metrics

If the app's `billingOptions` has one or more items that are charged according to a metric value, the app itself must register and update the metric values over time. Not registering the metric values or updating them correctly means the app's users will not be charged the right value.

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

#### Step 3 - Registering metric data

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
