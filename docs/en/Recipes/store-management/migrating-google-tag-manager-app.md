## Migrating Google Tag Manager app from major 2.x to major 3.x 

Version 3.x of [VTEX’s Google Tag Manager (GTM) app](https://developers.vtex.com/vtex-developer-docs/docs/vtex-google-tag-manager) tracks the entire user’s journey through the store, from viewing a product to purchasing it, via events triggered by the variable `ecommerceV2`. 

New and rearranged properties were added to the product schema to represent on the events and to track the user's journey and keep product information consistent across all areas of the store.

| GTM 3.x property | Type |
| -------- | ------- | 
| `id`  | Renewed property | 
| `variant`  | Renewed property | 
| `name`   | Renewed property | 
| `quantity`  | Unchanged property | 
| `price`  | Unchanged property| 
| `category`  | Unchanged property | 
| `brand`  | Unchanged property | 
| `dimension1`  | New property | 
| `dimension2`  | New property | 
| `dimension3`  | New property | 

> ℹ️
> 
> For more details on these properties, go to the section [Product schema](#product-schema)



Follow the steps below to update the GTM container and fetch the data from the `ecommerceV2` variable.

## Before you start
For Google Analytics (GA) to read the data from the variable `ecommerceV2`, you will need a GA variable for the store’s checkout responsible for tracking the Checkout and Order Placed pages.

Create the store's checkout variable by following the step **For the store’s checkout** in the [Setting up Google Tag Manager documentation](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-setting-up-google-tag-manager#creating-variables).


## Step by step

### Creating `ecommerceV2`

1. Log in to your [GTM account](https://tagmanager.google.com) and click on the GTM container you want to work with.
2. Click on **Variables**, and click on’ New’ in the **User-Defined Variables** section.
3. Replace the `Untitled Variable` value with `ecommerceV2`.
4. Click on **Variable Configuration** box.
5. Then, on **Page Variables**, click on **Data Layer Variable**.
6. In the `Data Layer Variable Name` field, type `ecommerceV2`.
7. Click on `Save`:

![ecommercev2-variable](https://user-images.githubusercontent.com/67270558/137797960-9287770e-6e77-4088-b6ce-a7c4a0f0187c.png)


### Using the `ecommerceV2` variable on the Google Analytics tag

1. Open the [store’s checkout variable](#before-you-start) by clicking on **Variables** and in the **User-Defined Variables** section select it.
2. Click on the **Variable Configuration** box and expand the **More Settings** menu.
3. Then, click on **Ecommerce** and check the **Enable Enhanced Ecommerce Feature** option. 
4. Disable **Use data layer** option and, on the **Read data from variable** field, select `{{ecommerceV2}}`. 
5. Click on `Save,` and you should have a variable as the example below:


After executing the steps described, your Google Tag Manager container is ready to support the GTM 3.x major. [Check your Google Analytics](https://support.google.com/analytics/answer/1009692?hl=en) to see the impact on the results.


### Updating Google Tag Manager settings
After installing the Google Tag Manager app 3.x major, you must update the app's settings to guarantee that previous data won't be be lost after the upgrade. To update the app's settings:

1. Access the following link: `https://{myaccount}.myvtex.com/admin/apps/vtex.google-tag-manager@3.3.1/setup/`. Do not forget to change the value in brackets for your account name.
2. In the field **Google Tag Manager**, type the GTM ID.
> ℹ️ Info
>  
>  To find your store’s GTM ID, first, you need a container to the Tag Manager account. If you do not have one follow the [create a new account and container tutorial](https://support.google.com/tagmanager/answer/6103696?hl=en#install) and after find the GTM ID in The Container ID column of the container.

3. Click on `SAVE`.

#### Product schema 

To make the product information consistent across all store areas and help capture the entire user's journey on the store, [Google Tag Manager 3.x.](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-migrating-google-tag-manager-app) includes Enhanced Ecommerce properties to the product data schema as events. These properties enable stores to provide additional information, such as product printing, promotion, and sales data.


| Prop name | Description |
| --------------- | --------------- |
| id | Product ID - Previously SKU ID. |
| variant | SKU ID - Previously SKU Name. The variant of the product, e.g., Rebel pink. |
| name | Product Name - Previously Product Name or SKU Name.| 
| quantity | Product quantity |
| price | Product price. |
| category | Product category, e.g., Apparel. |
| brand	| Product brand. |
| dimension1 | Product Reference ID. |
| dimension2 | SKU Reference ID. |
| dimension3 | SKU Name (does not include the Product Name). |

The `dimension1`, `dimension2`, `dimension3` properties are custom dimensions that you can use to collect and analyze data that Google Analytics does not automatically create. 

For more information about custom dimensions and Enhanced Ecommerce, refer to [Custom dimensions and metrics](https://support.google.com/analytics/answer/2709828?hl=en&ref_topic=2709827#configuration&zippy=%2Cin-this-article) and [Google Enhanced ecommerce official guide](https://developers.google.com/analytics/devguides/collection/analyticsjs/enhanced-ecommerce#ecommerce-data) respectively.


## Related Resources

- [VTEX Google Tag Manager (GTM) app](https://developers.vtex.com/vtex-developer-docs/docs/vtex-google-tag-manager)
- [Setting up Google Tag Manager](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-setting-up-google-tag-manager)
