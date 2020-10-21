---
title: Adicionado preço assíncrono no product-summary
description: "Tenha o preço mais atualizado sem ter que lidar com um aumento no tempo de resposta da página"
date: "21/10/2020"
tags: ["price", "simulation"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/edit/master/docs/pt/Recipes/layout/preco-assincrono.md"
---

# Adicionado preço assíncrono no product-summary

## Introdução

Para algumas lojas, é essencial ter o preço mais atualizado. Porém, uma vez que este preço é requisitado do lado do servidor, ocorre um aumento no tempo de resposta da página.

Esta receita mostra como manter o tempo de resposta solicitando o preço mais atualizado no lado do cliente.

![priceasync](https://user-images.githubusercontent.com/40380674/96735041-85265680-1391-11eb-80e9-2eb35607fd72.gif)

## Step by step

1. Tenha certeza que o servidor não está requisitando o preço mais atualizado. Basta configurar a prop `simulationBehavior` para `skip`.

```diff
"store.search": {
  "blocks": [
    "search-result-layout"
  ],
  "props": {
    "context": {
+     "simulationBehavior": "skip"
    }
  }
},
```

2. Adicione as seguintes **dependencias** arquivo `manifest.json` de sua store-theme:

```json
"vtex.product-summary": "2.x",
"vtex.product-price": "1.x"
```

3. Adicione a prop `isPriceAsync` no bloco `product-summary.shelf`. Configure seu valor para `true`.

```diff
"product-summary.shelf": {
  "props": {
+   "isPriceAsync": true
  },
  "children": [
    // other children
    "product-list-price#summary",
    "flex-layout.row#selling-price-savings",
    "product-installments#summary",
    "add-to-cart-button",
  ]
}
```

4. "Embrulhe" as informações de preço no `product-price-suspense`.

```diff
{
+ "product-price-suspense": {
+   "children": [
+     "product-list-price#summary",
+     "flex-layout.row#selling-price-savings",
+     "product-installments#summary",
+     "add-to-cart-button"
+   ]
+ },
  "product-summary.shelf": {
    "props": {
     "isPriceAsync": true
    },
    "children": [
      // other children
-     "product-list-price#summary",
-     "flex-layout.row#selling-price-savings",
-     "product-installments#summary",
-     "add-to-cart-button",
+     "product-price-suspense"
   ]
  }
}
```

E isto é tudo! Agora você pode ter o preço mais atualizado sem se preocupar com um aumento no tempo de resposta da página.
