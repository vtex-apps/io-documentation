# Configurações básicas para desenvolver no VTEX IO

Todo desenvolvimento no **VTEX IO** começa com o [**Toolbelt**](*https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-toolbelt*), nossa **CLI** (_Command Line Interface_) que permite fazer _Login_, desenvolver novos [_apps_](*https://vtex.io/docs/getting-started/desenvolva-componentes-usando-vtex-io-e-react/3/link*) e gerenciar as já instaladas.

## VTEX IO Toolbelt

**O Toolbelt conecta sua conta VTEX a plataforma de desenvolvimento VTEX IO.** Você pode: 

-Fazer _Login_ na sua conta VTEX. 

-Gerenciar [_workspaces_](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-workspace).

-Desenvolver novos apps. 

## Instalando o VTEX IO Toolbelt

Para instalar a CLI do VTEX IO, você precisa garantir que o seu computador tenha o [Node.js](https://nodejs.org/) e o [Yarn](https://yarnpkg.com/) instalados.

Em seguida, digite no terminal do seu computador:

```
$ yarn global add vtex
```

>ℹ️ **Para confirmar que a instalação ocorreu normalmente, você pode executar o comando `vtex`. Ele deverá mostrar um texto de ajuda com todos os comandos disponíveis.**

## Fazendo o Login

Com a [CLI](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installation-and-command-reference) do VTEX IO instalada, use o seguinte comando para acessar sua conta VTEX:

```
$ vtex login {ContaVTEX}
```

Após executar o comando, abrirá uma guia no seu navegador solicitando suas credenciais de acesso.

Quando estiver _logado_, você pode usar o comando `vtex whoami` para descobrir qual conta e *workspace* estão sendo usados pelo terminal.

![exemplo terminal logado](https://user-images.githubusercontent.com/52087100/61886028-517e2780-aed5-11e9-9398-b6d2f3909a50.png)
  
## Criando seu próprio *workspace*

Ao usar o VTEX IO, toda interação com uma conta acontece em um [***workspace***](*https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-workspace*).

Ao fazer *login* em uma loja, você está automaticamente no *workspace* master dela, ou seja, na versão disponível para o usuário final. Por isso, quando quiser testar uma nova configuração, o seu próprio *workspace* de desenvolvimento deve ser criado executando o comando:

```
$ vtex use {nomeexemplo}
```

Isso muda a sua conta para um *workspace* chamado `nomeexemplo` e o cria se não existir. Você pode mudar o nome de acordo com o desejado.

![vtex-use-nomeexemplo](https://user-images.githubusercontent.com/52087100/61886135-7ffc0280-aed5-11e9-983f-4a76615d0574.png)

>⚠️ **O `vtex use` faz com que todas as suas operações passem a ocorrer no _workspace_ definido no comando. Isso significa que é possível alternar suas operações para master apenas executando no Toolbelt `vtex use master`, por exemplo.**

Com o seu *workspace* de desenvolvimento criado, você pode navegar na sua loja executando:

`https://{{nomeexemplo}}-{{accountname}}.myvtex.com`

Onde `workspace` é o *workspace* que você acabou de criar (como `nomeexemplo`) e a `conta` (como `accountname`) é o nome da conta em que você está trabalhando.

**Pronto! Agora você já pode desenvolver sua loja no VTEX IO!**
