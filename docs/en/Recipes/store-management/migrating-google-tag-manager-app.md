## Migrating Google Tag Manager app from major 2.x to major 3.x 

Version 3.x of VTEX’s Google Tag Manager (GTM) app, tracks the entire user’s journey through the store, from viewing a product to purchasing it, via events triggered by the variable `ecommerceV2`. 

Follow the steps below to update the GTM container and fetch the data from the `ecommerceV2` variable.

## Product schema changes

To make the product information consistent across all store areas and help capture the entire user's journey on the store, we have included new properties and rearranged a few of them to the new schema used to represent the events.

- Properties of the new schema:

> 🆕 - New property | 🔁 - Renewed property | ⏸ - Unchanged property

| Prop name     | Description   |
| ------------- | ------------- | 
| 🔁 `id`| Product ID - Previously SKU ID | 
| 🔁 `variant`| SKU ID - Previously SKU Name|
| 🔁 `name`| Product Name - Previously Product Name or SKU Name| 
| ⏸ `quantity`| Product Quantity  |
| ⏸ `price`| Product Price  |
| ⏸ `category`| Product Brand  |
| ⏸ `brand`| Product Quantity  |
| 🆕 `dimension1`| Product Reference ID  |
| 🆕 `dimension2`| SKU Reference ID   |
| 🆕 `dimension3`| SKU Name (does not include the Product Name)  |

### Creating `ecommerceV2`

1. Log in to your [GTM account](https://tagmanager.google.com) and click on the GTM container you want to work with.
2. Click on **Variables**, and click on’ New’ in the **User-Defined Variables** section.
3. Replace the `Untitled Variable` value with `ecommerceV2`.
4. Click on **Variable Configuration** box.
5. Then, on **Page Variables**, click on **Data Layer Variable**.
6. In the `Data Layer Variable Name` field, type `ecommerceV2`.
7. Click on `Save`:

![ecommercev2-variable](https://user-images.githubusercontent.com/67270558/137797960-9287770e-6e77-4088-b6ce-a7c4a0f0187c.png)

### Creating a Google Analytics Variable for the store’s checkout

For Google Analytics (GA)  to read the data from the variable `ecommerceV2`, you will need a GA variable for the store’s checkout responsible for tracking the Checkout and Order Placed pages.

To create the variable, follow the step in [Setting up Google Tag Manager](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-setting-up-google-tag-manager#creating-variables),  **Google Analytics variables** > **For the store’s checkout**.


### Using the `ecommerceV2` variable on the Google Analytics tag

1. Once you have a [variable for the store’s checkout](#creating-a-google-analytics-variable-for-the-stores-checkout), open it by clicking on **Variables** and in the **User-Defined Variables** section select it.
2. Click on the **Variable Configuration** box and expand the **More Settings** menu.
3. Then, click on **Ecommerce** and check the **Enable Enhanced Ecommerce Feature** option. 
4. Disable **Use data layer** option and, on the **Read data from variable** field, select `{{ecommerceV2}}`. 
5. Click on `Save,` and you should have a variable as the example below:


After executing the steps described, your Google Tag Manager container is ready to support the GTM 3.x major. [Check your Google Analytics](https://support.google.com/analytics/answer/1009692?hl=en) to see the impact on the results.

