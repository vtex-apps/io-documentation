# Cleaning cart data on log out

The VTEX shopping cart default behavior is to keep the cart alive until an order is placed. When this happens, a new cart is created. If a business rule requires a new cart every time a user logs out, we can use the [Session Watcher](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-collecting-user-session-data) to clear cart information.

> ℹ️
>
> It is not possible to get a brand new cart, but we can repurpose the current cart by removing any existing information on it. 

This document will guide you on how to use the [Session Watcher app](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-collecting-user-session-data) to clean up an existing cart during logout.


## Clients

VTEX IO Service Context gives you access to external clients. Clients are additional services with methods that give you access to different core applications. Here is a list of out-of-the-box client services available.

- `apps`
- `assets`
- `billing`
- `billingMetrics`
- `builder`
- `events`
- `id`
- `licenseManager`
- `masterdata`
- `messagesGraphQL`
- `metadata`
- `registry`
- `router`
- `segment`
- `settings`
- `session`
- `tenant`
- `vbase`
- `workspaces`
- `catalogGraphQL`
- `paymentProvider`

You can always extend your App Clients if you need to give it access to external or internal providers.

## Checkout Client
The VTEX IO Service Context does not have an out-of-the-box checkout client. The following steps will guide you on this setup of a client from our internal APIs.

1. Create a new `./node/clients/checkout.ts` file where you can keep all the methods for the `Checkout` class. This class will extend **JanusClient** (VTEX’s internal router), you can import it from `@vtex/api`. It should look like the example below. Types are also imported from `@vtex/api`.
```javascript
import type { InstanceOptions, IOContext } from ‘@’vtex/api’
import { JanusClient } from ‘@vtex/api’

export class Checkout extends JanusClient {
    constructor(context: IOContext, options?: InstanceOptions) {
        super(context, { …options })
    }
}
```


2. These internal APIs are going through `portal.vtexcommercestable.com.br/api/*`, which means we need to declare it as an `outbound-access` in our `manifest.json` file under "policies".


```json
"policies": [
    {
        "name": "outbound-access",
        "attrs": {
            "host": "portal.vtexcommercestable.com.br",
            "path": "/api/*"
        }
},
```


The same thing is required if you're accessing an external endpoint. Always add the `host` and `path` as an `outbound-access`.

> ⚠️
>
> Do not use protocol in the `host` (http, https). The `host` does not support wildcard within the address. It can be either fixed `host` or only ` *` , never both. The `path` supports wildcard.

3. Now that you have an initial class setup, you can let your application know that it exists. Do this by importing it to the `Clients` constructor under `./node/clients/index.ts`


```javascript
import { IOClients } from ‘@vtex/api’

import { Checkout } from ‘@vtex/api’

// Extend the default IOClients implementation with our own custom clients.
export class Clients extends IOClients {
    public get checkout() {
        return this.getOrSet(‘checkout’, Checkout)
    }
}
```


The checkout client will now be available to our handler, just like the others.
```json
{
    "name": "outbound-access",
    "attrs": {
        "host": "portal.vtexcommercestable.com.br",
        "path": "/checkout/changeToAnonymousUser/*"
}
```

4. Now you need to create your methods. The first thing you need is to change our `orderForm` (shopping cart) to anonymous. This will erase the `clientProfileData`, but will not remove the items from the cart, which will be done in another moment.

This method uses a path starting with `/checkout`, which means we need to include it to our policy by creating a new `outbound-access` entry.
Back to`checkout.ts`, add a new public method inside the `Checkout` class.
```javascript
public changeToAnonymous = (orderFormId: string) => {
    return this.http.getRaw(`/checkout/changeToAnonymousUser/${orderFormId}`, {
        metric ‘change-to-anonymous’,
    })
}
```


> ℹ️
>
> `JanusClient` gives you access to `http` and its methods. This example uses `getRaw`, which will return the entire response, including `httpCode`, headers, etc. If you do not need it, you can use only `get` instead. This `metric` property is used for logging, it is not not strictly necessary.

5. Create the other methods, `orderForm`, and `updateItems`, as shown below.

```javascript
public orderForm = (orderFormId: string) => {
    return this.http.post(
        `/api/checkout/pub/orderForm/${orderFormId}`,
        { expectedOrderFormSections: [‘items’] },
        {
            metric: ‘get-orderForm’,
        }
    )
}

public updateItems = (orderFormId: string, orderItems: any) => {
    return this.http.post(
        `/api/checkout/pub/orderForm/${orderFormId}/items/update`,
        { orderItems } ,
        {
            Metric: ‘update-orderForm-items’,
        }
    )
}
```


### Clear Cart handler
Back to `./resolvers/index.ts` load the checkout client from the context of our method `clearCart` and expose both `orderFormId` and `email` from the request body.

The logical flow is:

![Cart cleaning app logical flow](https://user-images.githubusercontent.com/47991446/165640268-97a65125-0e82-4ccc-aa89-f01afcd5cd9a.png)

You should have code similar to the example below.

```javascript
/* eslint-disable no-console */
import { json } from ‘co-body’

export const resolvers = {
    Routes: {
        clearCart: async (ctx: Context) => {
            Const {
                req,
                clients: { checkout },
            } = ctx

            const body: any = await json(req)
            const email = body?.authentication?.storeUserEmail?.value ?? null
            const orderFormId = body?.checkout?.orderFormId?.value ?? null

            console.log(‘clearCart =>’, body)

            ctx.set(‘Content-Type, ‘application/json’)
            ctx.set(‘Cache-Control’, ‘no-cache, no-store’) 

            const res = {
                public: {
                    demo: {
                        value: email ? ‘User Authenticated’ : ‘User not authenticated’,
                    },
                },
            }

            // If user is not authenticated, and we have an orderFormId
            if (!email && orderFormId) {
                // Get the current orderForm data
                const orderform: any await checkout.orderForm(orderFormId)

                // Only if we have a user assigned to this orderForm
                if (orderForm?.clientProfileData?.email) {
                    // Change to anonymous
                    await checkout.changeToAnonymous(orderFormId).catch((err) => {
                        if (err.response.status >= 400) {
                            console.log(‘Cart response error =>’, err.response.statusText)
                        } else {
                            console.log(‘Cart response all good =>’, err.response.status)
                        }
                    })

                    /*
                    * To remove items from the cart
                    * If we have items in the cart
                    */
                    if (orderForm?.items?.length) {
                        // Create a orderItems array with the item position and new quantity set to 0
                        const orderItems = orderForm.items.map((_: any, index: number) => {
                            return {
                                index,
                                quantity: 0,
                            }
                        })

                        // Update the cart items with the new quantity
                        await checkout.updateItems(orderFormId, orderItems).catch((err) => {
                            console.log(‘Error removing all items =>’, err)
                        })
                    }
                }
            }
            
            ctx.response.body = res
            ctx.response.status = 200
        },
    },
}
```

> ⚠️
>
> Don't forget to change the vendor in your `./manifest.json` file.

To link the app, run this command:
```
vtex link
```

If you wish, you can [download this complete example](https://drive.google.com/file/d/18Lr6-H5nm8ljPrS1945WNQAAkvFtQPYs/view?usp=sharing) 
