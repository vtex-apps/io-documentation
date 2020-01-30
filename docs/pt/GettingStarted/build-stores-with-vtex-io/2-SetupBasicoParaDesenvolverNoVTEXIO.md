# *Setup* básico para desenvolver no VTEX IO

Todo desenvolvimento no VTEX IO começa com o [**Toolbelt**](*link*), nossa CLI (Command Line Interface) que permite fazer login, desenvolver novas [apps](*link*) e gerwenciar as já instaladas.

## VTEX IO Toolbelt

Para instalar a CLI do VTEX IO, você precisa garantir que o seu computador tenha o [Node.js](https://nodejs.org/) e o [Yarn](https://yarnpkg.com/) instalados.

Em seguida, digite `yarn global add vtex` no terminal do seu computador.

```
$ yarn global add vtex
```

<div class="alert alert-info">
Para confirmar que a instalação ocorreu normalmente, você pode executar o comando `vtex`. Ele deverá mostrar um texto de ajuda com todos os comandos disponíveis.
</div>

## Login

Com a CLI do VTEX IO instalada, use o comando `vtex login` para entrar na sua conta VTEX:

```
$ vtex login {ContaVTEX}
```

Isso abrirá uma janela do seu navegador que solicitará suas credenciais.

Quando já estiver *logado*, você pode usar o comando `vtex whoami` para descobrir qual conta e *workspace* estão sendo usados pelo terminal.

<img width="876" alt="toolbelt-whoami" src="https://user-images.githubusercontent.com/52087100/61886028-517e2780-aed5-11e9-9398-b6d2f3909a50.png">
  
## Criando seu próprio *workspace*

Ao usar o VTEX IO, toda interação com uma conta acontece em um [***workspace***](*link*).

Ao fazer *login* em uma loja, você está automaticamente no *workspace* master dela, ou seja, na versão disponível para o usuário final. Por isso, lembre-se que sempre que você quiser testar uma nova configuração, o seu próprio *workspace* de desenvolvimento deve ser criado usando o comando `vtex use`.

```
$ vtex use {nomeexemplo}
```

Isso muda o seu Toolbelt para um *workspace* chamado `nomeexemplo` e o cria se ele não existir.

<img width="549" alt="vtex-use-nomeexemplo PT" src="https://user-images.githubusercontent.com/52087100/61886135-7ffc0280-aed5-11e9-983f-4a76615d0574.png">

<div class="alert alert-warning">
O <code>vtex use</code> faz com que todas as suas operações passem a ocorrer no <i>workspace</i> definido no comando. Isso significa que é possível alternar suas operações para master apenas executando no Toolbelt <code>vtex use master</code>, por exemplo. 
</div>

Com o seu próprio *workspace* de desenvolvimento criado, você pode navegar na sua loja acessando:

`https://{{nomeexemplo}}-{{accountname}}.myvtex.com`

Onde `workspace` é o *workspace* que você acabou de criar (como `nomeexemplo`) e `conta` é o nome da conta em que você está trabalhando.

Pronto! Agora você já pode desenvolver sua loja no VTEX IO.
