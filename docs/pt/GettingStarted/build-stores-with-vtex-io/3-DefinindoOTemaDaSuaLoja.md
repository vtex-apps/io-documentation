# Definindo o tema da sua loja

O [**Store Theme**](*link*) é um tema padrão aplicável para todas as lojas na plataforma VTEX IO. O tema realiza duas ações:

- **Declara *templates***, configurando e combinando componentes.

- **Declara estilos**, configurando cores primárias e secundárias, escalas de tipografia e espaçamento etc.

Isso quer dizer que o Store Theme é um tema padrão responsável por definir a aparência básica do *front* da sua loja.

O VTEX IO CLI do VTEX IO oferece um comando `vtex init` que pode rapidamente copiar o Store Theme no seu computador para que você o configure e customize de acordo com as necessidades do seu negócio.

>Observe que você deve instalar os seguintes apps a partir do terminal:

```
vtex install vtex.store-sitemap
vtex install vtex.store --force
vtex install vtex.admin-pages
```

## Implementando o Store Theme

Usando o seu terminal, navegue até um diretório já existente dos seus arquivos locais onde você deseja que o Store Theme seja copiado. Então, use o comando `vtex init` , selecione a opção **store-theme** e confirme que você gostaria de fazer o download do tema na pasta de destino previamente definida.

```
$ cd {{diretórioexemplo}}
```

```
$ vtex init
```

Você então receberá informações importantes sobre o Store Theme, como *vendor*, nome, título e a sua descrição. Com exceção de *vendor*, pressione *Enter* para manter os valores já pré-definidos de cada campo.

<div class="alert alert-info">
Substitua o valor pré-definido de <i>vendor</i> pelo nome da conta da loja em que você está desenvolvendo para que posteriormente você consiga publicar corretamente o tema nela. 
</div>

<img width="942" alt="VTEX IO CLI-store-theme-selection " src="https://user-images.githubusercontent.com/52087100/61887063-3d3b2a00-aed7-11e9-92b8-653c4972a218.png">

## *Linkando* seu código local ao VTEX IO

Agora que o Store Theme já foi copiado para os seus arquivos locais, você deve executar no seu terminal o comando `cd store-theme` . Depois, execute `vtex link` para ver o tema ser compilado e publicado na conta e no *workspace* que você acabou de criar.

<div class="alert alert-warning">
Execute <code>vtex whoami</code> para ter certeza de que você está na conta certa e em um <i>workspace</i> de desenvolvimento. Caso contrário, o VTEX IO CLI não irá aceitar o link direto com o master.
</div>

```
$ cd store-theme
```

```
 $ vtex link
```

<img width="910" alt="VTEX IO CLI-vtex-link" src="https://user-images.githubusercontent.com/52087100/61887229-9dca6700-aed7-11e9-9934-030a153b75b6.png">
  
Ao *linkar* o Store Theme, os arquivos locais do seu computador são sincronizados com a plataforma VTEX IO. Isso quer dizer que todas as alterações feitas por você localmente no código serão enviadas e refletidas no seu workspace.

## Entendendo a estrutura do Store Theme

Vamos dar uma olhada nos arquivos que foram gerados nos seus arquivos locais para entender a estrutura do tema padrão. Você pode navegar em seu código com o editor de sua preferência.

<img width="227" alt="vscode-folders-structure" src="https://user-images.githubusercontent.com/52087100/61887339-ce120580-aed7-11e9-8c7b-eb55d12def2b.png">

- **manifest.json**: arquivo principal de qualquer app. Ele guarda metadados importantes, como *vendor*, nome, versão, dependências de apps e [*builders*](*link*).

- **store**: pasta responsável por definir a estrutura de uma loja. É onde se configura os componentes de cada página e suas propriedades.

- **styles**: pasta responsável por definir o tema visual de uma loja, através da customização dos componentes de cada página.

## Visitando sua nova loja

Navegue novamente até a sua loja acessando:

`https://{{workspace}}-{{conta}}.myvtex.com`

Após o login, você deve ver o Store Theme já refletido na sua loja:

<img width="1426" alt="store-theme" src="https://user-images.githubusercontent.com/52087100/61896668-d4aa7800-aeeb-11e9-906b-9d6b04fd03c0.png">

Agora que sua loja já está no ar com o tema padrão, podemos construir a sua identidade configurando seus *templates* e customizando seus estilos.
