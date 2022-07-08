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

| Attribute | Type | Description |
|---|---|---|
| `revendaId` | integer | Resale ID number. |
| `porCodigo` | string | Definition of order code or ID that can be used to filter the query. |
| ↳ `codigo` | string | Order code, such as the order ID, the client ID or the ERP order ID. |
| ↳ `tipo` | integer | Type of code that will be used in the query.<br><br>If you want to filter the query using PedidoId (web order number, which is the identification number of the order placed through the store’s website), the value should be `0`.<br><br>To filter the query using PedidoClienteId (identification number associated with the customer who made the purchase), the value should be `1`.<br><br>To filter the query using PedidoErpId (ERP order number), set the value to `2`. |
| `porPeriodo` | object | Definition of dates to filter the query. |
| ↳ `dataInicial` | string | Start date of the query. |
| ↳ `dataFim` | string | End date of the query. |
| `porNotaFiscal` | object | Definition of invoice data to filter the query. |
| ↳ `notaFiscal` | string | Invoice number. |
| ↳ `serieNotaFiscal` | string | Invoice serial number. |

#### Request format

```json
{
  "revendaId": number,
  "porCodigo": {
    "codigo": string,
    "tipo": number (PedidoId: 0, PedidoClienteId: 1, PedidoErpId: 2)
  },
  "porPeriodo": {
    "dataInicial": Date,
    "dataFim": Date
  },
  "porNotaFiscal": {
    "notaFiscal": string,
    "serieNotaFiscal": string
  }
}
```

#### Response format

```json
{
  "itens": [
    {
      "pedidoErpId": string,
      "pedidoClienteId": string,
      "totalPedido": number,
      "status": number,
      "dataPedido": Date,
      "observacao": string,
      "notaFiscal": string,
      "serieNotaFiscal": string,
    }
  ]
}
```

### Search order details

By exposing the GET `api/v1/pedido?pedidoErpId={pedidoErpId}&revendaId={revendaId}` endpoint, it will be possible to fetch the details of a specific order directly from the ERP.

| **Attribute** | **Type** | **Description** |
|---|---|---|
| `pedidoErpId` | string | ERP order number, which is the identification number of the order placed through the store ERP. |
| `revendaId` | integer | Resale ID number. |

#### Request format

```json
{
  pedidoErpId: string
  revendaId: number
}
```

#### Response format

```json
{
  "pedidoErpId": string,
  "status": 0,
  "itens": [
    {
      "partNumber": string,
      "descricaoDoProduto": string,
      "quantidade": decimal number,
      "valorUnitario": decimal number,
      "valorTotal": decimal number,
      "comissao": decimal number
    }
  ],
  "revendaId": 2,
  "clienteFinalId": string,
  "clienteFinalCnpj": string,
  "clienteFinalCpf": string,
  "valorFrete": decimal number,
  "valorTotalPedido": decimal number,
  "dataPedido": Date,
  "dataPrevisaoEntrega": Date,
  "observacao": string,
  "notaFiscal": string,
  "serieNotaFiscal": string,
  "linkTransportadora": string,
  "formattedAddres": string,
  "zipcode": string,
  "methodPayment": string,
  "corpname": string,
  "corpemail": string,
  "cityState": string,
  "methodPaymentInfo": string,
  "centrosDeDistribuicao": [
    {
      "distributionCenterPrefix": string,
      "itens": [
        {
          "partNumber": string,
          "descricaoDoProduto": string,
          "quantidade": decimal number,
          "valorUnitario": decimal number,
          "valorTotal": decimal number,
          "comissao": decimal number
        }
      ],
      "valorFrete": decimal number,
      "valorTotalCD": decimal number
    },
    {
      "distributionCenterPrefix": string,
      "itens": [
        {
          "partNumber": string,
          "descricaoDoProduto": string,
          "quantidade": decimal number,
          "valorUnitario": decimal number,
          "valorTotal": decimal number,
          "comissao": decimal number
        }
      ],
      "valorFrete": decimal number,
      "valorTotalCD": decimal number
    }
  ]
}
```

### [OPTIONAL] Search order documents

By exposing the `GET` `api/v1/arquivospedido?pedidoErpId={pedidoErpId}&revendaId={revendaId}` endpoint, it will be possible to query the document files related to a given order by providing the related order number.

| **Attribute** | **Type** | **Description** |
|---|---|---|
| `pedidoErpId` | string | ERP order number, which is the identification number of the order placed through the store ERP. |
| `revendaId` | integer | Resale ID number. |

#### Request format

```json
{
  pedidoErpId: string
  revendaId: number
}
```

#### Response format

```json
{
  "pedidoErpId": string,
  "itens": [
    {
      "tipoArquivo": number (SegundaViaBoleto: 0, SegundaViaTransferencia: 1, Xml: 2, Danfe: 3, NumeroDeSerie: 4, GARE: 5, GNRE: 6, Outros: 7),
      "descricao": string,
      "url": string
    },
    {
      "tipoArquivo": number,
      "descricao": string,
      "url": string
    }
  ]
}
```

## Installing the B2B Orders app

Follow the steps below to install the B2B Orders app.

1. Using the terminal and the [Toolbelt](https://vtex.io/docs/recipes/development/vtex-io-cli-installation-and-command-reference/), [install](https://vtex.io/docs/recipes/store/installing-an-app/) the B2B Orders app in the desired workspace by running `vtex install vtex.omnichannel-order-status`.
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