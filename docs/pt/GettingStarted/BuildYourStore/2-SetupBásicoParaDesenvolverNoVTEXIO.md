# Setup básico para desenvolver no VTEX IO
 
Todo desenvolvimento no VTEX IO começa com o [Toolbelt](*link doc*), nossa CLI (Command Line Interface) que permite fazer login, desenvolver novas apps e gerenciar as já instaladas.


<div class=“alert alert-info”>
Entenda melhor o que são apps no VTEX IO acessando o nosso [glossário](*link doc sobre o que são apps no VTEX IO).
</div>

## VTEX IO Toolbelt

Para instalar a CLI do VTEX IO, você precisa garantir que o seu computador tenha o [Yarn](https://yarnpkg.com/) instalado.

Em seguida, digite `yarn global add vtex` no terminal do seu computador.

```
$ yarn global add vtex
```

Para confirmar que a instalação ocorreu normalmente, você pode executar o comando `vtex`. Ele deverá mostrar um texto de ajuda com todos os comandos disponíveis.  

Com a CLI do VTEX IO instalada, você já pode fazer login na sua conta.

## Login

Com comando `vtex login`, você pode entrar na sua conta VTEX.

```
$ vtex login {myaccount}
```

Isso abrirá uma janela do seu navegador que solicitará suas credenciais.

Quando já estiver logado, você pode usar o comando `vtex whoami` para descobrir qual __conta__ e __workspace__ estão sendo usados pelo terminal. 

<img width="876" alt="toolbelt-whoami" src="https://user-images.githubusercontent.com/52087100/61886028-517e2780-aed5-11e9-9398-b6d2f3909a50.png">
  
## Criando seu próprio workspace

Ao usar o VTEX IO, toda interação com uma conta acontece em um __[workspace]__(*link doc*), uma versão isolada de sua loja.

Por padrão, quando efetua login em uma loja, você está no workspace master, correspondente à versão disponível para o usuário final. Quaisquer alterações no workspace master de uma conta são refletidas automaticamente em todos os outros workspaces da sua loja. Por isso, lembre-se que sempre que você quiser testar uma nova configuração, você deve criar seu próprio workspace de desenvolvimento usando o comando `vtex use`.

```
$ vtex use {nomeexemplo}
```

Isso muda o seu toolbelt para um workspace chamado `nomeexemplo` e o cria se ele não existir.

<img width="549" alt="vtex-use-nomeexemplo PT" src="https://user-images.githubusercontent.com/52087100/61886135-7ffc0280-aed5-11e9-983f-4a76615d0574.png">


<div class=“alert alert-warning”>
 O <code>vtex use</code> faz com que todas as suas operações passem a ocorrer no workspace definido no comando. Isso significa que é possível alternar suas operações para master apenas executando no Toolbelt  `vtex use master`, por exemplo. 
</div>

Com o seu próprio workspace de desenvolvimento criado, você pode navegar na sua loja através dele acessando:

`https://{{nomeexemplo}}-{{accountname}}.myvtex.com`

Pronto! Agora você já está pronto para começar a desenvolver sua loja no VTEX IO. 
