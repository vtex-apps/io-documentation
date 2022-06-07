# 5. Listening to store events

Some services provided by third-party solutions may rely on store events. Events are notifications that a web application automatically broadcasts whenever a user performs an important action in a store, such as adding items to the shopping cart or accessing a product page.

For these scenarios, your Pixel app must be able to listen to the desired events and provide the required data to the third-party service in question.

## Step by step

1. Open the `react/index.tsx` file.
2. Write your script according to your Pixel app needs. Some store events you can use in your Pixel app are:

- `addToCart`- Triggered when a product is added to the cart.
- `removeItem` - Triggered when a product is removed from the cart
- `pageView` - Triggered on every loaded page view.
- `productImpression` - Triggered when product data is visible on the page currently being accessed by users.

>ℹ️ All the available event properties are written in **TypeScript**. Check them out [here](https://github.com/vtex-apps/pixel-app-template/blob/master/react/typings/events.d.ts).

Take the following example of an event implementation in the [Google Tag Manager Pixel app](https://github.com/vtex-apps/google-tag-manager/blob/master/react/index.tsx):


```ts
import { canUseDOM } from 'vtex.render-runtime'

import push from './modules/push'
import {
  Order,
  PixelMessage,
  ProductOrder,
  Impression,
  CartItem,
} from './typings/events'
import { AnalyticsEcommerceProduct } from './typings/gtm'

export default function() {
  return null
} // no-op for extension point

export function handleEvents(e: PixelMessage) {
  switch (e.data.eventName) {
    case 'vtex:pageView': {
      push({
        event: 'pageView',
        location: e.data.pageUrl,
        page: e.data.pageUrl.replace(e.origin, ''),
        referrer: e.data.referrer,
        ...(e.data.pageTitle && {
          title: e.data.pageTitle,
        }),
      })

      return
    }

    case 'vtex:productView': {
      const { selectedSku, productName, brand, categories } = e.data.product

      let price

      try {
        price = e.data.product.items[0].sellers[0].commertialOffer.Price
      } catch {
        price = undefined
      }

      const data = {
        ecommerce: {
          detail: {
            products: [
              {
                brand,
                category: getCategory(categories),
                id: selectedSku.itemId,
                name: productName,
                variant: selectedSku.name,
                price,
              },
            ],
          },
        },
        event: 'productDetail',
      }

      push(data)

      return
    }

    case 'vtex:productClick': {
      const { productName, brand, categories, sku } = e.data.product

      let price

      try {
        price = e.data.product.items[0].sellers[0].commertialOffer.Price
      } catch {
        price = undefined
      }

      const data = {
        event: 'productClick',
        ecommerce: {
          click: {
            products: [
              {
                brand,
                category: getCategory(categories),
                id: sku.itemId,
                name: productName,
                variant: sku.name,
                price,
              },
            ],
          },
        },
      }

      push(data)

      return
    }

    case 'vtex:addToCart': {
      const { items } = e.data

      push({
        ecommerce: {
          add: {
            products: items.map((sku: any) => ({
              brand: sku.brand,
              category: sku.category,
              id: sku.skuId,
              name: sku.name,
              price: `${sku.price}`,
              quantity: sku.quantity,
              variant: sku.variant,
            })),
          },
          currencyCode: e.data.currency,
        },
        event: 'addToCart',
      })

      return
    }

    case 'vtex:removeFromCart': {
      const { items } = e.data

      push({
        ecommerce: {
          currencyCode: e.data.currency,
          remove: {
            products: items.map((sku: any) => ({
              brand: sku.brand,
              id: sku.skuId,
              category: sku.category,
              name: sku.name,
              price: `${sku.price}`,
              quantity: sku.quantity,
              variant: sku.variant,
            })),
          },
        },
        event: 'removeFromCart',
      })

      return
    }

    case 'vtex:orderPlaced': {
      const order = e.data

      const ecommerce = {
        purchase: {
          actionField: getPurchaseObjectData(order),
          products: order.transactionProducts.map((product: ProductOrder) =>
            getProductObjectData(product)
          ),
        },
      }

      push({
        // @ts-ignore
        event: 'orderPlaced',
        ...order,
        ecommerce,
      })

      // Backwards compatible event
      push({
        ecommerce,
        event: 'pageLoaded',
      })

      return
    }

    case 'vtex:productImpression': {
      const { currency, list, impressions, product, position } = e.data
      let oldImpresionFormat: Record<string, any> | null = null

      if (product != null && position != null) {
        // make it backwards compatible
        oldImpresionFormat = [
          getProductImpressionObjectData(list)({
            product,
            position,
          }),
        ]
      }

      const parsedImpressions = (impressions || []).map(
        getProductImpressionObjectData(list)
      )

      push({
        event: 'productImpression',
        ecommerce: {
          currencyCode: currency,
          impressions: oldImpresionFormat || parsedImpressions,
        },
      })

      return
    }

    case 'vtex:userData': {
      const { data } = e

      if (!data.isAuthenticated) {
        return
      }

      push({
        event: 'userData',
        userId: data.id,
      })

      return
    }

    case 'vtex:cartLoaded': {
      const { orderForm } = e.data

      push({
        event: 'checkout',
        ecommerce: {
          checkout: {
            actionField: {
              step: 1,
            },
            products: orderForm.items.map(getCheckoutProductObjectData),
          },
        },
      })

      break
    }

    default: {
      break
    }
  }
}

function getPurchaseObjectData(order: Order) {
  return {
    affiliation: order.transactionAffiliation,
    coupon: order.coupon ? order.coupon : null,
    id: order.orderGroup,
    revenue: order.transactionTotal,
    shipping: order.transactionShipping,
    tax: order.transactionTax,
  }
}

function getProductObjectData(product: ProductOrder) {
  return {
    brand: product.brand,
    category: product.categoryTree?.join('/'),
    id: product.sku,
    name: product.name,
    price: product.price,
    quantity: product.quantity,
    variant: product.skuName,
  }
}

function getCategory(rawCategories: string[]) {
  if (!rawCategories || !rawCategories.length) {
    return
  }

  return removeStartAndEndSlash(rawCategories[0])
}

// Transform this: "/Apparel & Accessories/Clothing/Tops/"
// To this: "Apparel & Accessories/Clothing/Tops"
function removeStartAndEndSlash(category?: string) {
  return category?.replace(/^\/|\/$/g, '')
}

function getProductImpressionObjectData(list: string) {
  return ({ product, position }: Impression) => ({
    brand: product.brand,
    category: getCategory(product.categories),
    id: product.sku.itemId,
    list,
    name: product.productName,
    position,
    price: `${product.sku.seller!.commertialOffer.Price}`,
    variant: product.sku.name,
  })
}

function getCheckoutProductObjectData(
  item: CartItem
): AnalyticsEcommerceProduct {
  return {
    id: item.id,
    name: item.name,
    category: Object.keys(item.productCategories ?? {}).reduce(
      (categories, category) =>
        categories ? `${categories}/${category}` : category,
      ''
    ),
    brand: item.additionalInfo?.brandName ?? '',
    variant: item.skuName,
    price: item.sellingPrice / 100,
    quantity: item.quantity,
  }
}

if (canUseDOM) {
  window.addEventListener('message', handleEvents)
}
```
