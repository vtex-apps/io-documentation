# Configurações básicas para desenvolver no VTEX IO

Todo desenvolvimento no VTEX IO começa e termina com o [**VTEX IO CLI**](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-VTEX IO CLI/), a interface de linha de comando do VTEX IO (do inglês, *Command-line Interface*). 

**O VTEX IO CLI funciona como uma ponte de comunicação entre a sua conta VTEX e a plataforma de desenvolvimento VTEX IO**. Através dele, você será capaz de fazer login na sua conta VTEX, gerenciar [*workspaces*](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-workspace/) e desenvolver novos apps.

## Instalando o VTEX IO CLI

Para instalar a CLI do VTEX IO, você deve garantir que o [Node.js](https://nodejs.org/) e o [Yarn](https://yarnpkg.com/) estejam corretamente instalados na sua máquina. 

Em seguida, execute no seu terminal:

```sh
yarn global add vtex
```

Para mais instruções e detalhes sobre a instalação do Toobelt, acesse a documentação [Instalando a CLI do VTEX IO e referência de comandos](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installation-and-command-reference/).

## Fazendo login na sua conta VTEX

Assim que o VTEX IO CLI for instalado, execute o comando a seguir para fazer login na sua conta VTEX:

```sh
vtex login {conta}
```

Após executar este comando, uma guia no seu navegador será aberta, solicitando as credenciais de acesso da sua conta VTEX.

<div class="alert alert-warning">
O valor em chaves (<code>{conta}</code>) deve ser substituído pelo nome da conta VTEX na qual você está trabalhando.
</div>

Você pode executar em seguida o comando `vtex whoami` para confirmar a conta VTEX e o workspace sendo utilizado pelo VTEX IO CLI. 

![VTEX IO CLI-whoami](https://user-images.githubusercontent.com/52087100/61886028-517e2780-aed5-11e9-9398-b6d2f3909a50.png)

## Criando um workspace de desenvolvimento

Qualquer e todo desenvolvimento no VTEX IO acontece por meio de um [***workspace***](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-workspace/). 

Os ***workspaces* funcionam como *branches* do GitHub***, de modo que qualquer ação de desenvolvimento é feita em uma área de trabalho específica, separada das demais. 

Os *workspaces* permitem, portanto, que você desenvolva e teste as suas alterações sem nenhum risco de interferir nos aplicativos ativos ou no trabalho de outros desenvolvedores.

Ao fazer login na sua conta VTEX, você está automaticamente vinculado ao *workspace* Master, ou seja, você está *logado* na versão da loja disponível para o usuário final.

Você deve então [criar um workspace de desenvolvimento](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-creating-a-development-workspace/) para começar a criar a sua aplicação do zero. 

Usando o seu terminal, execute o seguinte comando:

```sh
vtex use examplename
```

Isso mudará a sua conta para um *workspace* de desenvolvimento chamado `examplename`. Lembre-se de substituir este valor de acordo com o nome desejado por você!

![workspace-examplename EN](https://user-images.githubusercontent.com/52087100/63979000-30899300-ca8e-11e9-9d9d-234e31ac45f7.png)

Depois de fazer login na sua conta VTEX e criar o seu próprio *workspace* de desenvolvimento, você está pronto para começar a desenvolver o seu componente usando React e VTEX IO!
