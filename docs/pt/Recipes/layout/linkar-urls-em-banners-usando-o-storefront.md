---
title: Linkar URLs em banners usando o Storefront
description: "Linkar URL em banners pode ser uma grande oportunidade de influenciar a navegação do usuário! Confira o quão rápido e fácil é linkar URLs nos banners da sua loja usando o Storefront."
date: "30/08/2019"
tags: ["storefront", "url", "banner", "link", "linking", "url-interna", "url-externa", "redirecionamento"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/pt/Recipes/layout/LinkarURLsEmBannersAtrav%C3%A9sDoStorefront.md"
---

# *Linkar* URLs em *banners* usando o Storefront

É possível configurar um *banner* da sua loja para que ele tenha redirecionamento de página, isso é, para que ele leve o usuário a qualquer endereço desejado por você. Para isso, basta associar o *banner* a qualquer URL externa ou interna (da própria loja) seguindo os passos abaixo: 

## URL interna

**1.** Acesse o módulo **CMS**.

**2.** Clique em **Storefront**.

**3.** Selecione o bloco **Carrossel** e escolha o *banner* que terá seu conteúdo editado.

**4.** Mantenha o *toggle* **Rota externa** inativo e no campo `URL interna`, copie e cole a URL interna desejada.

<img width="1150" alt="linkar-url-banners-image1" src="https://user-images.githubusercontent.com/52087100/64047940-8f124800-cb46-11e9-8b24-27fd07d8daa1.png">

**5.** Clique em **Salvar**.

<div class="alert alert-warning">
Os campos <code>Página alvo do banner</code> e <code>Parâmetros</code> foram <i>deprecados</i>. Portanto, apenas o valor preenchido no campo <code>URL interna</code> será considerado para o link de URL interna.
</div>
 
## URL externa

**1.** Acesse o módulo **CMS**.

**2.** Clique em **Storefront**.

**3.** Selecione o bloco **Carrousel** e escolha o *banner* que terá seu conteúdo editado.

**4.** Clique no *toggle* **Rota externa** e no campo `URL (externa)`, copie e cole a URL externa desejada.

<img width="1150" alt="link-url-banners-imagem2" src="https://user-images.githubusercontent.com/52087100/64047954-9a657380-cb46-11e9-9088-b7010abab8c4.png">

**5.** Clique em **Salvar**.
