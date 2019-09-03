---
title: Configurar o rastreamento de busca do Google Analytics
description: "Analise os principais termos buscados na sua loja e aprenda mais sobre o comportamento do seu usuário configurando o rastreamento de busca do Google Analytics."
date: "30/08/2019"
tags: ["google-analytics", "busca", "pesquisa", "rastreio", "rastreamento", "tracking"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/pt/Recipes/store/ConfigurarORastreamentoDeBuscaDoGoogleAnalytics.md"
---


# Configurar o rastreamento de busca do Google Analytics

Os relatórios em gráfico gerados pela ferramenta de rastreio de busca do Google Analytics ajudam o lojista a analisar as buscas realizadas pelos seus usuários, mensurando os principais termos buscados no site. 

Para acionar esse rastreamento, é necessário que o seu Analytics seja corretamente configurado para traduzir a URL de busca em dados relevantes sobre o comportamento de cada usuário. 

Siga o passo a passo abaixo e configure a tracking de busca para a sua loja:

**1.** No Google Analytics da conta desejada, clique em **Administrador** no canto inferior esquerdo da sua tela.

**2.** Acesse **Configurações da vista da propriedade**.

**3.** Ative a flag **Acompanhamento da pesquisa no site** e preencha o campo **Parâmetro de consulta** com  `_q,rest`.

**4.** Ative a flag **Categorias da pesquisa interna** e preencha o campo **Parâmetro de categoria** com  `_c`.

![search-tracking PT](https://user-images.githubusercontent.com/52087100/63991237-46fb1300-cabd-11e9-86c0-fc378a0e855b.png)

**5.** Clique em **Save**.  
