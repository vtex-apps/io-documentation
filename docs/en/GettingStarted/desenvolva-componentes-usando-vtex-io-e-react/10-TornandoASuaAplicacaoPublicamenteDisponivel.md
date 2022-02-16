# Tornando a sua aplicação publicamente disponível

Uma vez que você completou todos os passos anteriores e se sente confortável com as configurações feitas, é hora de aprender a tornar a sua app publicamente disponível, isso é, como **fazer com que a sua aplicação também seja usada por outros usuários além de você**. 

Antes de seguir com o fluxo de desenvolvimento da app, é importante primeiramente definir como será a sua distribuição: quem poderá instalar a sua app? Você cobrará pelo seu uso? Se sim, quanto ela custará para as contas interessadas?

As respostas para essas perguntas variam de acordo com o tipo de distrubuição escolhido para a aplicação. Na plataforma VTEX IO, uma app pode ser do tipo:

- **Privada** - Só pode ser instalada pela conta `vendor`, isso é, pela conta responsável pelo seu desenvolvimento e manutenção. 
- **Pública** - É disponibilizada para todo o ecossistema de contas que usam a plataforma VTEX, podendo ser cobrado um valor pelo seu uso ou não.

## Definindo a distribuição

A escolha entre privada ou pública deve ser tomada antes mesmo do lançamento da aplicação. 

Isso porque, dependendo do tipo escolhido, algumas configurações devem ser feitas no arquivo `manifest.json` da app antes que a sua distribuição aconteça. Afinal, são essas configurações no `manifest` que definirão quem poderá usar o componente, assim como se o seu uso será gratuito ou não. 

Para aprender como configurar corretamente o `manifest.json` da sua app, acesse a documentação sobre [Billing Options](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-billing-options/) e siga as instruções de acordo com o cenário desejado para o seu projeto. 

Depois de seguir os passos indicados, a sua aplicação estará pronta para ser devidamente distribuída! 

Lembre-se de que [*linkar*](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-linking-an-app) a app em que você está trabalhando não será suficiente: você também precisará lançá-la, publicá-la, tê-la instalada em workspace de produção para testes e, finalmente, validá-la para o *deploy*, como veremos a seguir:

## Lançando uma nova versão

Se você está certo de todas as mudanças feitas no workspace de desenvolvimento, é hora de lançar uma nova versão da sua app. 

Usando o seu terminal, acesse a pasta da sua app e execute o comando abaixo:

```sh
vtex release major
```

Ele será responsável por:

- Atualizar o versionamento nos arquivos `CHANGELOG.md` e `manifest.json` de acordo com a [semântica esperada](https://semver.org/).
- Criar um *commit* de lançamento.
- Criar um repositório no GitHub para a aplicação.

Caso você deseje lançar uma versão **Beta**, execute o comando `vtex release major beta` no seu terminal. Ele irá executar as mesmas ações que o comando anterior, com a diferença que você estará lançando uma versão *beta* da sua aplicação ao invés de *stable*. 

<div class="alert alert-warning">
Não se esqueça de fazer login na conta VTEX desejada antes de lançar a nova versão para que o <code>vendor</code> da app seja a conta em que você está trabalhando. 
</div>

## Publicando na plataforma VTEX IO

Uma vez que a aplicação foi lançada, ela deve ser devidamente instalada para ter as suas configurações testadas por você. Contudo, não é possível instalar uma aplicação existente apenas no seu ambiente local de trabalho.

<div class="alert alert-info">
Note que, ao lançar a sua app no passo 2 acima, você não a vinculou à plataforma VTEX IO. O comando anterior apenas automatizou ações para o seu correto versionamento.
</div>

Por isso, devemos agora publicar a aplicação na plataforma! Usando o seu terminal, acesse a pasta da aplicação e execute o comando abaixo:

```sh
vtex publish
``` 

O comando transformará a sua app em uma ***release candidate version***, fazendo com que ela consiga ser instalada por meio do Toobelt para fins de testes.

<div class="alert alert-warning">
Você deve sempre estar logado na conta VTEX desejada para a publicação da app. Certifique-se que o <code>vendor</code> da app é igual à conta em que você está trabalhando.
</div>

Caso a sua app não tenha o campo `billingOptions` configurado, usuários com acesso à conta VTEX responsável pela publicação também conseguirão instalar a aplicação por meio do Admin, na seção **Apps**.

## Instalando em um workspace de produção

Com a sua app pronta para ser instalada, você deve criar um workspace de produção para testar as configurações e possíveis comportamentos. 

Usando o seu terminal, execute o seguinte comando (substituindo as chaves pelo nome desejado ao seu novo workspace):

```sh
vtex use {WorkspaceName} --production
```

<div class="alert alert-warning">
A partir deste momento, nenhuma mudança no código da sua app é mais recomendada. Isso porque um workspace de produção está apto para receber tráfego de usuários, isso é, ser acessado por outras pessoas além de você. Caso você deseje executar alguma mudança no código, você deve trabalhar nas novas configurações a partir de um workspace de desenvolvimento e, em seguida, seguir os passos deste artigo novamente.
</div>

Para instalar a aplicação no novo workspace, execute o comando abaixo substituindo as chaves pelos valores reais do seu cenário:

```sh
vtex install {appVendor}.{apNname}@{appVersion}
```

## Validando o deploy 

É hora de validar a sua *release candidate version*!

É recomendável que você primeiramente execute um [teste A/B nativo](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-running-native-ab-testing) entre o novo workspace de produção e o workspace Master da sua loja para testar a estabilidade da app. 

<div class="alert alert-warning">
Se você está trabalhando com uma versão beta e todas as suas configurações já foram devidamente testadas, é recomendável que você retorne ao segundo passo deste artigo para lançar a versão não beta da aplicação e, em seguida, seguir novamente o passo a passo detalhado.
</div>

Uma vez satisfeito com os resultados obtidos, acesse a pasta da aplicação no seu terminal e execute o seguinte comando para publicar a sua *release candidate version* como uma versão *stable*:

```sh
vtex deploy
```

A execução do comando fará com que a nova versão *stable* da app seja automaticamente instalada em todas as contas que já haviam instalado anteriormente a versão *release candidate*.

## Passos extras

### Promovendo o seu workspace para Master

Promover para Master o workspace de produção no qual a aplicação foi instalada é fundamental para renderizá-la para os usuários finais da sua loja, aqueles que vão realmente interagir com o componente desenvolvido. 

Por isso, se você deseja usar a app desenvolvida na loja em você está trabalhando, é necessário executar mais um passo no seu processo de desenvolvimento.

Usando o seu terminal, faça log in na sua conta VTEX e certifique-se de estar usando o workspace de produção usado nos passos anteriores. Em seguida, execute o comando abaixo:

```sh
vtex workspace promote
```

<div class="alert alert-info">
O status de um workspace Master é <code>production true</code>. Ao receber essa resposta do seu terminal, a sua aplicação já estará disponível para os usuários da sua loja.
</div>

### Enviando a sua aplicação para a VTEX App Store

Incorporando o novo componente no tema da sua loja VTEX ou não, é possível que você ainda queira adicionar a app desenvolvida no catálogo de aplicações da VTEX App Store. 

A [VTEX app store](https://extensions.vtex.com/) é um *marketplace* para soluções *plug&play*, podendo ser usado por qualquer conta VTEX interessada em deixar as suas soluções à disposição de outras contas do ecossistema também. 

Para disponibilizar a sua app, confira a documentação [Submitting an app in the VTEX app store](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-submitting-your-app-in-the-vtex-app-store/).

---

**Pronto**! Ao finalizar estes passos, a aplicação terá sido lançada, publicada, testada, validada e finalmente se tornado pública para todos os seus usuários. 

Durante esta track, você aprendeu todos os passos necessários para desenvolver do zero uma aplicação de front usando React, GraphQL, CSS e a plataforma de desenvolvimento VTEX IO. 

Para entender mais sobre as possibilidades de desenvolvimento da plataforma, não se esqueça de acessar o restante da nossa [documentação](https://developers.vtex.com/vtex-developer-docs/docs/welcome)!

