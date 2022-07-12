---
title: Querying B2B order statuses
description: "Find out how to securely share order statuses with your business customers."
date: "17/11/2020"
tags: ["order", "b2b", "status"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/consulting-b2b-order-statuses.md"
---

# Querying B2B order statuses

In a B2B business model, your company and your partners may need to share selected information, such as order statuses. This is necessary when you want to show the status of external orders — orders made outside VTEX — to customers on your ecommerce, for example.

For these scenarios, we recommend that you install and set up the [B2B Orders app](#installing-the-b2b-orders-app) in your VTEX account. By communicating with your Enterprise Resource Planning (ERP), this app allows your business’ customers to securely check their order status at any time they want.

> ⚠️ The B2B Orders app is not compatible with the [B2B Suite](https://developers.vtex.com/vtex-developer-docs/docs/vtex-b2b-suite) solution. Therefore, these instructions do not apply to stores using the B2B Suite. If you are using the B2B Suite, refer to the [B2B Orders History](https://developers.vtex.com/vtex-developer-docs/docs/vtex-b2b-orders-history) documentation instead.


Check the following sections for information on the [ERP API requirements](#erp-api-requirements) and on how to [install the B2B Orders app](#installing-the-b2b-orders-app) in your store.


## ERP API requirements

The B2B Orders app comes with a specific pattern for communicating with the ERP API. For the query to work properly, your ERP API must have different endpoints for each of the following scenarios:

- [Search order](#search-order)
- [Search order details](#search-order-details)
- [Search order documents](#optional-search-order-documents) [OPTIONAL] 

> ℹ If you have specific business needs which are not satisfied by the scenarios presented, you can customize the B2B Orders app.

The possible requests and response formats for each of the ERP API's required endpoints are presented below.


### Search order

By exposing the `POST` `api/v1/pedido/pesquisa` endpoint, it will be possible to search for external orders by filling one of the following objects: `porPeriodo`, `porCodigo` or `porNotaFiscal`.


#### Request format

| **Attribute** | **Type** | **Description** |
|---|---|---|
| `revendaId` | integer | Resale ID number. |
| `porCodigo` | string | Definition of order code or ID that can be used to filter the query. |
| ↳ `codigo` | string | Order code, such as the order ID, the client ID or the ERP order ID. |
| ↳ `tipo` | integer | Type of code that will be used in the query.<br><br>If you want to filter the query using `PedidoId` (web order number, which is the identification number of the order placed through the store’s website), the value should be `0`.<br><br>To filter the query using `PedidoClienteId` (identification number associated with the customer who made the purchase), the value should be `1`.<br><br>To filter the query using `PedidoErpId` (ERP order number), set the value to `2`. |
| `porPeriodo` | object | Definition of dates to filter the query. |
| ↳ `dataInicial` | string | Start date of the query. |
| ↳ `dataFim` | string | End date of the query. |
| `porNotaFiscal` | object | Definition of invoice data to filter the query. |
| ↳ `notaFiscal` | string | Invoice number. |
| ↳ `serieNotaFiscal` | string | Invoice serial number. |

#### Request body example

```json
{
  "revendaId": 55,
  "porCodigo": {
    "codigo": "1234",
    "tipo": 1
  },
  "porPeriodo": {
    "dataInicial": "2022-07-11T23:28:30Z",
    "dataFim": "2022-10-11T23:28:30Z"
  },
  "porNotaFiscal": {
    "notaFiscal": "987654321",
    "serieNotaFiscal": "123"
  }
}
```

#### Response format

| **Attribute** | **Type** | **Description** |
|---|---|---|
| `itens` | array of objects | Array of objects containing orders data. |
| ↳ | object | Object containing order data. |
|   ↳ `pedidoErpId` | string | ERP order number, which is the identification number of the order placed through the store ERP. |
|   ↳ `pedidoClienteId` | string | Identification number associated with the customer who made the purchase. |
|   ↳ `totalPedido` | number | Total value of the order. |
|   ↳ `status` | integer | Order status. |
|   ↳ `dataPedido` | string | Date of the order. |
|   ↳ `observacao` | string | Additional order information. |
|   ↳ `notaFiscal` | string | Invoice number. |
|   ↳ `serieNotaFiscal` | string | Invoice serial number. |



#### Response body example

```json
{
  "itens": [
    {
      "pedidoErpId": "12345",
      "pedidoClienteId": "10987",
      "totalPedido": 456,
      "status": 1,
      "dataPedido": "2022-10-11T23:28:30Z",
      "observacao": "",
      "notaFiscal": "987654321",
      "serieNotaFiscal": "123"
    }
  ]
}
```

### Search order details

By exposing the GET `api/v1/pedido?pedidoErpId={pedidoErpId}&revendaId={revendaId}` endpoint, it will be possible to fetch the details of a specific order directly from the ERP.

#### Request format

| **Attribute** | **Type** | **Description** |
|---|---|---|
| `pedidoErpId` | string | ERP order number, which is the identification number of the order placed through the store ERP. |
| `revendaId` | integer | Resale ID number. |

#### Request body example

```json
{
  "pedidoErpId": "12345",
  "revendaId": 2
}
```

#### Response format

| **Attribute** | **Type** | **Description** |
|---|---|---|
| `pedidoErpId` | string | ERP order number, which is the identification number of the order placed through the store ERP. |
| `status` | integer | Order status. |
| `itens` | array of objects | Array of objects containing information about each item in the order. |
| ↳ | object | Object containing information about an item. |
|   ↳ `partNumber` | string |  |
|   ↳ `descricaoDoProduto` | string | Product description. |
|   ↳ `quantidade` | number | Item quantity. |
|   ↳ `valorUnitario` | number | Price per item. |
|   ↳ `valorTotal` | number | Total value. |
|   ↳ `comissao` | number | Comission. |
| `revendaId` | integer | Resale ID number. |
| `clienteFinalId` | string | Customer's ID. |
| `clienteFinalCnpj` | string | Customer's CNPJ number. |
| `clienteFinalCpf` | string | Customer's CPF number. |
| `valorFrete` | number | Freight value. |
| `valorTotalPedido` | number | Total order value. |
| `dataPedido` | string | Date of the order. |
| `dataPrevisaoEntrega` | string | Delivery date. |
| `observacao` | string | Additional information. |
| `notaFiscal` | string | Invoice number. |
| `serieNotaFiscal` | string | Invoice serial number. |
| `linkTransportadora` | string | Carrier link. |
| `formattedAddres` | string | Address. |
| `zipcode` | string | ZIP code. |
| `methodPayment` | string | Payment method used in the order. |
| `corpname` | string | Corporate name. |
| `corpemail` | string | Corporate email. |
| `cityState` | string | City and state. |
| `methodPaymentInfo` | string | Information about the payment method used in the order. |
| `centrosDeDistribuicao` | array of objects | Array containing objects that represent each Distribution Center. |
| ↳ | object | Object containing information per Distribution Center. |
|   ↳ `distributionCenterPrefix` | string | Prefix of the Distribution Center. |
|   ↳ `itens` | array of objects | Array containing objects with order items information. |
|      ↳ | object | Object with order items information. |
|         ↳ `partNumber` | string | |
|         ↳ `descricaoDoProduto` | string | Product description. |
|         ↳ `quantidade` | number |  Item quantity. |
|         ↳ `valorUnitario` | number | Price per item. |
|         ↳ `valorTotal` | number | Total value. |
|         ↳ `comissao` | number | Comission. |
|   ↳ `valorFrete` | number | Freight value. |
|   ↳ `valorTotalCD` | number | Total delivery value including Distribution Center costs. |


#### Response body example

```json
{
  "pedidoErpId": "12345",
  "status": 0,
  "itens": [
    {
      "partNumber": "123",
      "descricaoDoProduto": "Beautifully handmade laptop case/sleeve made in the Nepal Himalaya. It can be slipped inside your backpack or carried alone with space for all your work bits and pieces!",
      "quantidade": 2.0,
      "valorUnitario": 22.0,
      "valorTotal": 44.0,
      "comissao": 4.0
    }
  ],
  "revendaId": 2,
  "clienteFinalId": "109",
  "clienteFinalCnpj": "55616766000197",
  "clienteFinalCpf": "48654007028",
  "valorFrete": 10.0,
  "valorTotalPedido": 58.0,
  "dataPedido": "2022-10-11T23:28:30Z",
  "dataPrevisaoEntrega": "2022-10-11T23:28:30Z",
  "observacao": "",
  "notaFiscal": "987654321",
  "serieNotaFiscal": "123",
  "linkTransportadora": "https://www.google.com/",
  "formattedAddres": "Quadra SHIN QI 4 Conjunto 3",
  "zipcode": "71510230",
  "methodPayment": "Credit Card",
  "corpname": "Knowledge Inc.",
  "corpemail": "qlrmrfuo@knowledgemd.com",
  "cityState": "BrasiliaDF",
  "methodPaymentInfo": "Credit Card",
  "centrosDeDistribuicao": [
    {
      "distributionCenterPrefix": "CD1",
      "itens": [
        {
          "partNumber": "123",
          "descricaoDoProduto": "Beautifully handmade laptop case/sleeve made in the Nepal Himalaya. It can be slipped inside your backpack or carried alone with space for all your work bits and pieces!",
          "quantidade": 2.0,
          "valorUnitario": 22.0,
          "valorTotal": 44.0,
          "comissao": 4.0
        }
      ],
      "valorFrete": 10.0,
      "valorTotalCD": 10.0
    }
  ]
}
```

### [OPTIONAL] Search order documents

By exposing the `GET` `api/v1/arquivospedido?pedidoErpId={pedidoErpId}&revendaId={revendaId}` endpoint, it will be possible to query the document files related to a given order by providing the related order number.

#### Request format

| **Attribute** | **Type** | **Description** |
|---|---|---|
| `pedidoErpId` | string | ERP order number, which is the identification number of the order placed through the store ERP. |
| `revendaId` | integer | Resale ID number. |

#### Request body example

```json
{
  "pedidoErpId": "12345",
  "revendaId": 2
}
```

#### Response format

| **Attribute** | **Type** | **Description** |
|---|---|---|
| `pedidoErpId` | string | ERP order number, which is the identification number of the order placed through the store ERP. |
| `itens` | array of objects | Array of objects containing information about each document in the order. |
| ↳ | object | Object containing information about a document. |
|    ↳ `tipoArquivo` | integer | Type of document. SegundaViaBoleto: 0, SegundaViaTransferencia: 1, Xml: 2, Danfe: 3, NumeroDeSerie: 4, GARE: 5, GNRE: 6, Outros: 7. |
|    ↳ `descricao` | string | Document description. |
|    ↳ `url` | string | Document URL. |


#### Response body example

```json
{
  "pedidoErpId": "12345",
  "itens": [
    {
      "tipoArquivo": 0,
      "descricao": "Boleto",
      "url": "https://www.google.com/"
    }
  ]
}
```

## Installing the B2B Orders app

Follow the steps below to install the B2B Orders app.

1. Using the terminal and the [Toolbelt](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installation-and-command-reference), [install](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-installing-an-app) the B2B Orders app in the desired workspace by running `vtex install vtex.omnichannel-order-status`.
2. In your browser, access your account's admin as in `https://{workspace}--{account}.myvtex.com/admin`. ️Remember to replace `{workspace}` and `{account}` with the workspace and account you are using.
3. Under **Account Settings**, go to **Apps **> **My apps**.
4. Look for the **B2B Order** app.
5. Click on `Settings` on the B2B Order app card.
6. Fill the following fields with the required information to communicate with the external service:
    * **Link endpoint**: the endpoint address of the desired service.
    * **Login**: access credentials of the external service.
    * **Token**: authentication token to access the service.
7. Click on `Save`.

![b2b-orders](https://user-images.githubusercontent.com/60782333/99416894-17aa0f00-28d8-11eb-8414-28ded9fc2d1e.png)

Once your changes are duly saved, a new tab, named **Orders B2B**, will be available in your client's menu on the **[My Account page](https://help.vtex.com/en/tutorial/how-does-my-account-work--2BQ3GiqhqGJTXsWVuio3Xh)**, as shown in the following image:

![client-view](https://user-images.githubusercontent.com/60782333/95912705-83e5a000-0d79-11eb-866c-f6f10832a36f.png)


Read our article [Understanding B2B Orders](https://help.vtex.com/en/tutorial/understanding-b2b-orders--1arpUseqasZZ45Lq7PgevO) for more information on the B2B Orders app.