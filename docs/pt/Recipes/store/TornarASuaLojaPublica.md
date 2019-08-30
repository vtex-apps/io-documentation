---
title: Tornar a sua loja pública
description: "Se você deseja tornar a sua nova loja publicamente disponível, linká-la não será suficiente. Aprenda nesta recipe o passo a passo para fazer com que as suas novas configurações finalmente sejam disponibilizadas ao usuário final."
date: "30/08/2019"
tags: ["release", "loja", "promover", "produção", "master", "workspace", "pública", "disponível", "usuário-final"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/pt/Recipes/store/TornarASuaLojaP%C3%BAblica.md"
---

# Tornar a sua loja pública
 
Se você está seguro das configurações feitas por você e deseja que a sua nova versão da loja fique disponível para todo e qualquer usuário, [linkar]() a store theme app em que você está trabalhando não será suficiente: ela também precisará ser lançada, ter seu workspace posto em modo de produção e promovido para master.
 
## Lançamento
 
Se você está seguro de todas as configurações feitas no seu workspace de desenvolvimento, é hora de lançar uma nova versão da app, isso é, uma nova versão do tema da loja.
 
Vamos usar o comando `vtex release` para lançar a nova versão dentro do `manifest.json`  da app de acordo com a nomenclatura de versionamento semântico, atualizando seu `CHANGELOG.md`, atribuindo etiquetas (commits tags) e enviando as alterações feitas para o seu repositório remoto.
 
Você deve executar `vtex release major stable` no seu terminal para automaticamente lançar a sua nova versão em um ambiente stable da conta. Alternativamente, também é possível ajustar seu release de formas diferentes, executando `vtex release {major/minor/patch}  {stable/beta}`.
 
Os comandos acima também irão publicar a app no registro da conta em que você está trabalhando. Isso irá permitir que ela não exista somente no seu ambiente local e possa ser instalada para testes por você e outros usuários com acesso à conta.
 
## Modo de produção
 
Uma vez que a app já foi instalada e testada, você já pode colocar o seu workspace em modo de produção usando o comando abaixo:
 
`vtex workspace production true`
 
A partir desse momento, nenhuma alteração no código é mais permitida, uma vez que o workspace está pronto para receber tráfego e ser acessado abertamente.
 
## Workspace master
 
Promover um workspace para master significa tornar disponível todas as mudanças feitas nele para o usuário final, ou seja, finalmente tornar sua nova loja disponível para o público.
 
Você pode promover seu workspace em modo de produção para master usando o seguinte comando:
 
`vtex workspace promote`
 
<div class="alert alert-info">
O status de um workspace que se encontra em master é <code>production true</code>.
</div>

