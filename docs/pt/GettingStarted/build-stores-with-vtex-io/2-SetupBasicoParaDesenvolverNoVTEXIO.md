# _Setup_ básico para desenvolver no VTEX IO

Todo desenvolvimento no VTEX IO começa com o [**Toolbelt**](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-toolbelt), nossa CLI (_Command Line Interface_) que permite fazer _login_, desenvolver novas [apps](https://vtex.io/docs/getting-started/desenvolva-componentes-usando-vtex-io-e-react/3/) e gerenciar as já instaladas.

**O Toolbelt funciona como uma ponte de comunicação entre a sua conta VTEX e a plataforma de desenvolvimento VTEX IO.** Através dele, você será capaz de fazer _login_ em sua conta VTEX, gerenciar [_workspaces_](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-workspace) e desenvolver novos apps.


## Instalando o VTEX IO Toolbelt

Para instalar a CLI do VTEX IO, é necessário que o seu computador tenha o [Node.js](https://nodejs.org/) e o [Yarn](https://yarnpkg.com/) corretamente instalados.

Em seguida, execute no terminal do computador:

```
$ yarn global add vtex
```

>ℹ️ **Para confirmar que a instalação ocorreu normalmente, você pode executar o comando `vtex`. Ele deverá mostrar um texto de ajuda com todos os comandos disponíveis.**

## _Login_

Com a [CLI](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installation-and-command-reference) do VTEX IO instalada, use o comando abaixo para acessar sua conta VTEX:

```
$ vtex login {ContaVTEX}
```

Depois de executar o comando, abrirá uma janela do seu navegador solicitando suas credenciais VTEX.

>ℹ️ O valor em chaves **({conta})** deve ser substituído pelo nome da conta VTEX na qual você está trabalhando.

Quando estiver *logado*, você pode usar o comando `vtex whoami` para confirmar a conta e *workspace* utilizados pelo terminal.

![exemplo terminal logado](https://user-images.githubusercontent.com/52087100/61886028-517e2780-aed5-11e9-9398-b6d2f3909a50.png)
  
## Criando um *workspace*

Qualquer desenvolvimento utilizando o VTEX IO, acontece através de um [***workspace***](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-workspace).

Ao fazer *login* em uma conta VTEX, você está automaticamente no *workspace* Master, ou seja, na versão disponível para o usuário final. 

Então, quando for testar uma nova configuração, [crie um *workspace* de desenvolvimento](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-creating-a-development-workspace) para começar sua aplicação.

Utilizando o terminal, execute o comando

```
$ vtex use {nomeexemplo}
```

Isso muda a sua conta para um *workspace* chamado `nomeexemplo`. Substitua o valor de acordo com o nome desejado.

![vtex-use-nomeexemplo](https://user-images.githubusercontent.com/52087100/61886135-7ffc0280-aed5-11e9-983f-4a76615d0574.png)

>⚠️ **O `vtex use` faz com que todas as suas operações passem a ocorrer no _workspace_ definido no comando. Isso significa que é possível alternar suas operações para master executando no Toolbelt `vtex use master`, por exemplo.**

Com o *workspace* de desenvolvimento criado, você pode navegar na sua loja executando:

`https://{{nomeexemplo}}-{{accountname}}.myvtex.com`

Onde o valor `workspace` é o *workspace* que você acabou de criar (como `nomeexemplo`) e o valor `conta` é o nome da conta em que você está trabalhando.

Pronto! Agora você pode desenvolver utilizando React e VTEX IO.
