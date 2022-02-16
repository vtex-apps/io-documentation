# Translating catalog content

In this step-by-step, we teach you how to overwrite an automatic message translation from the Catalog, such as a product name or a product description, with a more specific and representative content of your store.

As a background, catalog messages are translatable text strings related to the catalog of a store, saved as external data in the [Catalog API](https://developers.vtex.com/reference/catalog-api-overview).
 
>ℹ️ The Catalog API is one of the multiple REST APIs that compose the VTEX Administrative panel. This particular API is responsible for manipulating a store’s sales channels, categories, brands, products, SKUs, and specifications.

The following list contains the settings from the Catalog API that are internally set as translatable. Meaning that given a locale, an automatic translation fetched from the *automatic translation service* is available.

- **Category:** name, keywords (similar words), page title (tag title), meta tag description, and the URL slug (cross-border stores only).
- **Brand:** name, keywords (similar words), page title (tag title), meta tag description, and the URL slug (cross-border stores only).
- **Product:** name, keywords (substitute words), page title (tag title), description, short description, meta tag description, and the URL slug (cross-border stores only).
- **SKU** name.
- **[SKU or product specification](https://help.vtex.com/en/tracks/catalog-101--5AF0XfnjfWeopIFBgs3LIQ/2NQoBv8m4Yz3oQaLgDRagP):** name, description, and values.
- **[Category group](https://help.vtex.com/en/tutorial/creating-category-groups--tutorials_246)** name.

However, we understand that considering literal translations and cultural factors, you may want to overwrite automatic translations with specific and representative content of your store. 

This is possible via the `catalog-graphql` app, which is the GraphQL interface of the Catalog API.

## Step by step

Follow this step by step if you aim to translate text messages from your store's catalog.

1. [Install](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-installing-an-app) the `vtex.admin-graphql-ide@3.x` app using your terminal.

2. Access the **GraphQL admin IDE** section of the desired account. You will find it in the admin's side-bar menu:

![catalog](https://user-images.githubusercontent.com/52087100/66516950-95d29a00-eab8-11e9-8cea-080fbdab84d5.png)

3. From the dropdown list, choose the `vtex.catalog-graphql` app.
4. Click on  *Query Variables* at the bottom of the page.
5. According to your scenario, check the following sections ([category](#category), [brand](#brand), [product](#product), [SKU](#SKU), [SKU or product specification](#SKU-or-product-specification), [specification values](#specification-values)) for orientations on how to fill in the main text box and the *Query Variables* section.
6. After adjusting your query, click on the play button to run the declared mutation. The expected response is a boolean value indicating `true`.

Now, no further actions are needed on your part. Once you receive the expected response, you are ready to check out the desired changes in your store!

Check the following gif of the complete process of overwriting automatic translations of a product:

![catalog](https://user-images.githubusercontent.com/60782333/89960323-1a300500-dc15-11ea-89a0-bbd5d6494d64.gif)

## Category

### Mutation

Fill in the main text box with the following mutation command:

```
mutation translate($args:CategoryInputTranslation, $locale:Locale){
  translateCategory(category:$args,locale:$locale)
}
```

### Query Variables

According to the following example and the following explanations, fill in the *Query Variables* section with the desired translations of each parameter.

```json
{
  "args":{
    "id": "3",
    "name": "Elêtronicos",
    "title": "Casa - Elêtronicos",
    "description": "Esta é a descrição da categoria Eletrônicos",
    "keywords": [
        "eletronicos",
        "utensílios"
    ],
    "linkId": "eletronicos"
  },
  "locale": "pt-BR" 
}
```

  - `id`: the category ID. Every category in your store has a unique ID that can be found under *Catalog* > *Categories* in the admin.
  - `name`: category name.
  - `title`: category page meta title.
  - `description`: detailed description about the category.
  - `keywords`: an object containing the translations of **each** substitute word of the category.
  - `linkId`: the `textLink` (unless your store is a cross-border one, it must **not** be translated).
  - `locale`: target translation locale.

>ℹ️ If your store is a cross-border one, keep in mind that the `linkId` is the slug used to build the category URL. Hence, an alias with the translated URL slug of this category will be automatically created in the <a href="https://developers.vtex.com/vtex-developer-docs/docs/rewriter">Rewriter</a> app for the binding associated to the target locale. The alias is stored in the `resolveAs` field of its related internal route in the Rewriter app. For example: a category registered under the `eletronics` slug as in `http://{storename}.com/us/eletronics/d`, could have its slug translated to `eletronicos` for the `pt-BR` binding, as in `http://{storename}.com/br/eletronicos/d`.

## Brand

### Mutation

Fill in the main text box with the following mutation command:

```
mutation translate($args:BrandInputTranslation, $locale:Locale){
  translateBrand(brand:$args,locale:$locale)
}
```

### Query Variables

According to the following example and the following explanations, fill in the *Query Variables* section with the desired translations of each parameter.

```json
{
  "args":{
    "id": "2000057",
    "name": "Calvin Klein",
    "text": "Esta é uma descrição da marca.",
    "siteTitle": "Calvin Klein",
    "keywords": "calvin klain"
  },
  "locale": "pt-BR" 
}
```

  - `id`: the brand ID. Every brand in your store has a unique ID that can be found under *Catalog* > *Brands* in the admin.
  - `name`: brand name.
  - `text`: brand description (meta tag description).
  - `siteTitle`: brand page title (tag title).
  - `keywords`: an object containing the translations of **each** substitute word of the brand.
  - `locale`: target translation locale.

## Product

### Mutation

Fill in the main text box with the following mutation command:

```
mutation translate($args:ProductInputTranslation, $locale:Locale){
  translateProduct(product:$args,locale:$locale)
}
```

### Query Variables

According to the following example and the following explanations, fill in the *Query Variables* section with the desired translations of each parameter.

```json
{
  "args":{
    "id": "45",
    "name": "Câmera Retrô",
    "description": "Esta é uma descrição genérica deste produto.",
    "shortDescription": "Esta é uma breve descrição genérica deste produto.",
    "title": "Câmera Retrô - Store Components",
    "metaTagDescription": "Compre os melhores produtos em nossa loja",
    "linkId": "black-steel-film-camera",
    "keywords": [
      "lomografia",
      "vintage"]
 },
  "locale": "pt-BR" 
}
```

  - `id`: the product ID. Every product in your store has a unique ID that can be found under *Catalog* > *Products and SKUs* in the admin.
  - `name`: product name.
  - `description`: product description.
  - `shortDescription`: additional short description.
  - `title`: page title (tag title)
  - `metaTagDescription`: description (meta tag description).
  - `keywords`: an object containing the translations of **each** substitute word of the product.
  - `linkId`: the `textLink` (unless your store is a cross-border one, it must **not** be translated).
  - `locale`: target translation locale.
 
>ℹ️ If your store is a cross-border one, keep in mind that the `linkId` is the slug used to build the product URL. Hence, an alias with the translated URL slug of this product will be automatically created in the <a href ="https://developers.vtex.com/vtex-developer-docs/docs/rewriter">Rewriter</a> app for the binding associated to the target locale. The alias is stored in the `resolveAs` field of its related internal route in the Rewriter app. For example: a product registered under the `blue-top-retro-camera` slug as in `http://{storename}.com/us/blue-top-retro-camera/p`, could have its slug translated to `camera-retro-azul` for the `pt-BR` binding, as in `http://{storename}.com/br/camera-retro-azul/p`.

## SKU

### Mutation

Fill in the main text box with the following mutation command:

```
mutation translate($args:SKUInputTranslation, $locale:Locale){
  translateSKU(sku:$args,locale:$locale)
}
```

### Query Variables

According to the following example and the following explanations, fill in the *Query Variables* section with the desired translations of each parameter.

```json
{
  "args":{
    "id": "46",
    "name": "Mixer Retro - Marrom"
  },
  "locale": "pt-BR" 
}
```

  - `id`: the SKU ID. Every product in your store has a unique ID that can be found under *Catalog* > *Products and SKUs* in the admin.
  - `name`: the SKU name.
  - `locale`: target translation locale.

## SKU or product [specification](https://help.vtex.com/en/tracks/catalog-101--5AF0XfnjfWeopIFBgs3LIQ/2NQoBv8m4Yz3oQaLgDRagP)

### Mutation

Fill in the main text box with the following mutation command:

```
mutation translate($args:FieldInputTranslation, $locale:Locale){
  translateField(field:$args,locale:$locale)
}
```

### Query Variables

According to the following example and the following explanations, fill in the *Query Variables* section with the desired translations of each parameter.
 
```json
{
  "args":{
    "fieldId": "31",
    "name": "Cor"
  },
  "locale": "pt-BR" 
}
```

  - `fieldId`: the product or SKU specification field ID. Every product or SKU specification in your store has a unique ID that can be found following this [orientation for SKU specifications](https://help.vtex.com/en/tracks/catalog-101--5AF0XfnjfWeopIFBgs3LIQ/6UjLHdAT5YLuflki10SXLr?locale=en) or this [orientation for product specifications](https://help.vtex.com/en/tracks/catalog-101--5AF0XfnjfWeopIFBgs3LIQ/4fcdmJzQ6QYA9zWf3bLWin).
  - `name`: the specification name.
  - `locale`: target translation locale.

## [Specification](https://help.vtex.com/en/tracks/catalog-101--5AF0XfnjfWeopIFBgs3LIQ/2NQoBv8m4Yz3oQaLgDRagP) values

### Mutation

Fill in the main text box with the following mutation command:

```
mutation translate($args:FieldValueInputTranslation, $locale:Locale){
  translateFieldValues(fieldValues:$args,locale:$locale)
}
```

### Query Variables

According to the following example and the following explanations, fill in the *Query Variables* section with the desired translations of each parameter.

```json
{
  "args": {
    "fieldId": "31",
    "fieldValuesNames":[
        {
          "id":"91",
          "name":"Azul"
        },
        {
          "id": "92",
          "name": "Vermelho"
      }
    ]
  },
  "locale": "pt-BR"
}
```

  - `fieldId`: the product or SKU specification field ID. Every product or SKU specification in your store has a unique ID that can be found following this [orientation for SKU specifications](https://help.vtex.com/en/tracks/catalog-101--5AF0XfnjfWeopIFBgs3LIQ/6UjLHdAT5YLuflki10SXLr?locale=en) or this [orientation for product specifications](https://help.vtex.com/en/tracks/catalog-101--5AF0XfnjfWeopIFBgs3LIQ/4fcdmJzQ6QYA9zWf3bLWin).  
  - `fieldValuesNames`: an object containing:
      - `id`: the specification value ID.
      - `name`: the specification value name.
  - `locale`: target translation locale.

⚠️ *Specification values ID can be found by running the following query:*

```        
query{
  fieldValues(fieldId:"24"){
    fieldValueId
    value
  }
}
```

*Where `fieldId` is the specification ID found following this [orientation for SKU specifications](https://help.vtex.com/en/tracks/catalog-101--5AF0XfnjfWeopIFBgs3LIQ/6UjLHdAT5YLuflki10SXLr?locale=en) or this [orientation for product specifications](https://help.vtex.com/en/tracks/catalog-101--5AF0XfnjfWeopIFBgs3LIQ/4fcdmJzQ6QYA9zWf3bLWin).*

## Category group

### Mutation

Fill in the main text box with the following mutation command:

``` 
mutation translate($args: GroupInputTranslation, $locale:Locale) {
  translateGroup(group: $args, locale:$locale)
}
```

### Query Variables

According to the following example and the following explanations, fill in the Query Variables section with the desired translations of each parameter.

```
{
  "args":{
    "groupId": "14",
    "name": "Cores"
  },
  "locale": "pt-BR" 
}
```

- `groupId`: the category group ID.
- `name`: the category group name.
- `locale`: target translation locale.

⚠️ *Category group IDs can be found by running the following query:*

```
query{
  groupsByCategory(categoryId:1){
    id
    name
  }
}
```

*Where `categoryId` is the ID of the category related to that group.*
