# Configuração básica para desenvolver no VTEX IO

Todo desenvolvimento no [VTEX IO](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-what-is-vtex-io) 
começa com a nossa CLI (*Command Line Interface*).  

A CLI possibilita a comunicação entre a loja VTEX e a plataforma de desenvolvimento VTEX IO, permitindo que você faça login, 
desenvolva novos aplicativos e gerencie os que já estão instalados.

## Instalando o VTEX IO CLI  

> ! Para instalar a CLI do VTEX IO, você precisa garantir que o seu computador tenha o [Node.js](https://nodejs.org/en/download/) e o [Yarn](https://yarnpkg.com/) 
instalados.

Selecione o sistema operacional do seu computador e siga os passos para fazer a instalação.

* Windows
  - descrição da instalação

* MAC OS
  - descrição da instalação

* Linux
  - descrição da instalação

Abra o terminal no seu computador e digite o comando `yarn global add vtex`

```
$ yarn global add vtex
```

> Para confirmar se a instalação ocorreu normalmente, execute o comando `vtex`. Será exibido um texto de ajuda com todos os comandos disponíveis.

## Fazendo login na conta VTEX

Após instalação da CLI do VTEX IO, acesse sua conta VTEX usando o comando `vtex login`

```
$ vtex login {account-name}
```
Uma janela será exibida no navegador solicitando suas credenciais. Depois de fazer o login, use o comando `vtex whoami` para descobrir qual conta e *workspace* estão sendo usados pelo terminal.

![](https://user-images.githubusercontent.com/52087100/61886028-517e2780-aed5-11e9-9398-b6d2f3909a50.png)

## Criando seu próprio *workspace*

No VTEX IO, toda interação com uma conta acontece em um *workspace*.

Ao fazer login em uma loja, você está automaticamente no *workspace master* dela, ou seja, na versão disponível para o usuário final. Por isso, quando for testar uma nova configuração, o seu próprio *workspace* de desenvolvimento deve ser criado usando o comando `vtex use`.
```
$ vtex use {nomeexemplo}
```
Esse comando muda o seu VTEX IO CLI para um *workspace* existente chamado `nomeexemplo` ou cria um novo se ele não existir.

![vtex-use-nomeexemplo](https://user-images.githubusercontent.com/52087100/61886135-7ffc0280-aed5-11e9-983f-4a76615d0574.png)

>Todas as suas operações acontecerão no *workspace* definido no comando `vtex use`. Para alternar suas operações para master, por exemplo, execute o comando`vtex use master` na VTEX IO CLI.

Com o seu próprio *workspace* de desenvolvimento criado, navegue pela sua loja acessando `https://{{nomeexemplo}}-{{accountname}}.myvtex.com`. 

Nesse ambiente, `workspace` é o que você acabou de criar como `nomeexemplo` e `conta` é o nome da conta em que você está trabalhando.

Agora você já pode desenvolver sua loja no VTEX IO.
