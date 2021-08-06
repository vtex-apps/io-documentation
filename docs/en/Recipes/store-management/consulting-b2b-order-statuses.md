---
title: Consulting B2B order statuses
description: "Find out how to securely share order statuses with your business customers."
date: "17/11/2020"
tags: ["order", "b2b", "status"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/consulting-b2b-order-statuses.md"
---

# Consulting B2B order statuses

In a B2B business model, your company and your partners may need to share selected information, such as order statuses. 

For these scenarios, we recommend that you install and set up the *B2B Orders* app in your VTEX account. 

By communicating with your *Enterprise resource planning (ERP)*, this app allows your business customers to securely check their order status at any time they want.
 
For more information on how to set up the *B2B Orders* app and its related external APIs to the ERP, check the following section.

## Step by step

1. Using the terminal and the [Toolbelt](https://vtex.io/docs/recipes/development/vtex-io-cli-installation-and-command-reference/), [install](https://vtex.io/docs/recipes/store/installing-an-app/) the *B2B Orders* app in the desired workspace by running `vtex install vtex.omnichannel-order-status`.

2. In your browser, access your account's admin as in `https://{workspace}--{account}.myvtex.com/admin`.

>⚠️ *Remember to replace the values between the curly brackets according to your scenario.*

3. Under `Account Settings`, go to `Apps > My apps`. Look for the *B2B Orders* app and install it.
4. Click on `Settings` to set up the necessary information for communicating with the desired service. That is:

- **Link endpoint** - the endpoint address of the desired service.
- **Login** - credentials for accessing the service.
- **Token** - authentication token for accessing the service.

![b2b-orders](https://user-images.githubusercontent.com/60782333/99416894-17aa0f00-28d8-11eb-8414-28ded9fc2d1e.png)

>⚠️ *So that the *B2B Orders* app can properly work, your ERP API must have different endpoints for each of the following scenarios: search orders, search order details, and search order documents. To learn more about it, check the [ERP API requirements](#erp-api-requirements) section.*

5. Save your changes.

Once your changes are duly saved, a new option, namely **Orders B2B**, will be available in your client's menu, as in the following image:

![client-view](https://user-images.githubusercontent.com/60782333/95912705-83e5a000-0d79-11eb-866c-f6f10832a36f.png)

## ERP API requirements

To facilitate its implementation, the *B2B Orders* app comes with a well-defined pattern for communicating with the ERP API.

This pattern implies that your company's ERP API has different endpoints for each of the following scenarios: 

- [Search order](#search-order).
- [Search order details](#search-order-details).
- [[OPTIONAL] Search order documents](#search-order-documents).

>⚠️ *For specific needs, not satisfied by the scenarios presented, you might need to customize the B2B Orders app.*

In the following, we present the possible requests and response format for each one of the ERP API's related endpoints.

### Search order

By exposing the `POST` `api/v1/pedido/pesquisa` endpoint, your company's client will be able to search for orders in the ERP by filling one of the following objects: `porPeriodo`, `porCodigo` or `porNotaFiscal`.

#### Request format

```
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

```
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


By exposing the `GET` `api/v1/pedido?pedidoErpId={pedidoErpId}&revendaId={revendaId}` endpoint, your company's client will be able to consult the details of a specific order directly from the ERP.

#### Request format

```
{
  pedidoErpId: string
  revendaId: number
}

```

#### Response format

```
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
  "notaFiscal": string",
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

By exposing the `GET` `api/v1/arquivospedido?pedidoErpId={pedidoErpId}&revendaId={revendaId}` endpoint, your company's client will be able to consult the document files related to a given order by providing the related order number.

#### Request format

```
{
  pedidoErpId: string
  revendaId: number
}

```

#### Response format

```
{
  "pedidoErpId": string,
  "itens": [
    {
      "tipoArquivo": number (SegundaViaBoleto: 0, SegundaViaTransferencia: 1, Xml: 2, Danfe: 3, NumeroDeSerie: 4, GARE: 5, GNRE: 6, Outros: 7),
      "descricao": string,
      "url": string"
    },
    {
      "tipoArquivo": number,
      "descricao": string,
      "url": string"
    }
  ]
}

```
