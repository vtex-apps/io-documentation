# Customizando estilos

Agora que entendemos como mudar a estrutura do seu tema de loja, vamos aprender a customizar o estilo dele usando a pasta `styles`.  

## Definindo um novo estilo para o seu tema

O arquivo `style.json`(*link doc*) é o responsável por definir automaticamente o estilo do seu tema, sem a necessidade de declarar CSS para os componentes de cada página. 

Isso significa que você pode customizar a aparência de toda a sua loja apenas ajustando as definições padrões declaradas neste arquivo. Essa customização pode ser feita de maneira fácil e rápida usando o [VTEX Styleguide](https://styleguide.vtex.com/#/Styles), guia de estilos do arquivo `style.json` baseado em uma estrutura CSS altamente configurável, o [VTEX Tachyons](https://vtex.github.io/vtex-tachyons/). 

Por exemplo: podemos definir no arquivo `style.json` que a cor de fundo do tema padrão agora será azul. Para isso, basta alterar a propriedade `base` do bloco `semanticColors`: 

```
"semanticColors": {
        "background": {
          "base": "#00BFFF",
          "base--inverted": "#03044e",
          "action-primary": "#0F3E99",
          "action-secondary": "#eef3f7",
          "emphasis": "#f71963",
          "disabled": "#f2f4f5",
          "success": "#8bc34a",
          "success--faded": "#eafce3",
          "danger": "#ff4c4c",
          "danger--faded": "#ffe6e6",
          "warning": "#ffb100",
          "warning--faded": "#fff6e0",
          "muted-1": "#727273",
          "muted-2": "#979899",
          "muted-3": "#cacbcc",
          "muted-4": "#e3e4e6",
          "muted-5": "#f2f4f5"
        },
        
````

Faça as alteração de `"base"` no seu código e salve as alterações feitas para conferir o resultado na loja:

<img width="1425" alt="store-theme-azul" src="https://user-images.githubusercontent.com/52087100/61905178-d467a800-aefe-11e9-9442-e13e1a186e95.png">

## Estilos avançados com substituições de CSS

O arquivo `style.json` possibilita a customização do seu tema de forma mais genérica. Porém, pode ser que você queira criar uma identidade mais personalizada para a sua loja, definindo uma aparência exclusiva para um componente dela. 

As __substituições de CSS__ permitem que você customize componentes com estilos diferentes do tema padrão, sobrescrevendo o que foi declarado no arquivo `styles.json` para a sua loja.  Por exemplo: é possível que você deseje que as prateleiras da sua home page tenham um estilo diferente daquele genérico implementado pelo Store Theme. 

Você declara as substituições de CSS criando um novo arquivo dentro da pasta `style` em `css`. O arquivo criado deve ter como nome a __app__  que terá sua customização sobrescrita, seguindo o seguinte formato: `vtex.{app}.css`. Verifique quais apps podem ter seus estilos sobrescritos acessando o `manifest.json` do seu tema. 

Dentro deste arquivo, as classes de componente que serão sobrescritas devem ser dividas para a customização, como mostra o exemplo abaixo. As classes de um componente podem ser encontradas na [documentação](*link doc*) de cada um deles.

Crie o arquivo `vtex.shelf.css` na pasta `css` e declare dentro dele a seguinte substituição de CSS:

```
.container {
    background-color: #FE2E2E
}
```

Salve suas alterações e acesse a sua loja mais uma vez para conferir o estilo vermelho das prateleiras sobrescever azul da sua loja:

<img width="1421" alt="shelfs-substituição-css" src="https://user-images.githubusercontent.com/52087100/61905097-a3877300-aefe-11e9-99d7-2a688b9e334f.png">

### Block Class

Agora que você sobrescreveu a aparência das prateleiras, imagine a seguinte situação: ao invés de todas as prateleiras da sua loja terem o mesmo estilo, você agora deseja que cada uma delas tenha um.

Isso quer dizer que será necessário não só declarar uma substituição de CSS para o componente Shelf, como também criar uma substituição de CSS para um bloco específico dele. 

O __Block Class__ (`"blockClass"`), portanto, é uma propriedade que pode ser adicionada a qualquer bloco declarado e permite a customização específica dele por substituição de CSS. 

Por exemplo, vamos customizar a maneira como o bloco que declaramos `shelf#deals` é renderizado:

IMAGEM VSCODE

```
"shelf#deals": {
    "blocks": [
      "product-summary.shelf"
    ],
    "props": {
      "orderBy": "OrderByTopSaleDESC",
      "productList": {
        "maxItems": 10,
        "itemsPerPage": 5,
        "scroll": "BY_PAGE",
        "arrows": true,
        "titleText": "Best deals",
        "blockClass": "secondshelf",
      }
    }
  },
  
  ```

<div class=“alert alert-info”>
A propriedade `"blockClass"` pode ter o valor de sua preferência, desde que ele seja referenciado corretamente no arquivo de CSS criado. 
</div>

Para referenciar o bloco, basta adicionar o valor da propriedade `"blockClass"` na substituição de CSS do seu componente seguindo o formato `.{class}--{blockClassvalue}`. 

```
.container--secondshelf {
    background-color: #FE2E2E
}
```

Depois de salvar as alterações feitas, conseguimos ver as duas prateleiras customizadas de formas diferentes:

IMAGEM RENDERIZADO


<div class=“alert alert-warning”>
As substituições de CSS só podem ser alteradas manualmente por código enquanto as customizações feitas pelo arquivo `style.json` podem ser facilmente editadas através do [Storefront](*link doc*). Por isso, ao customizar o estilo do seu tema, é recomendável evitar fazer grandes customizações que necessitem de substituição de CSS.
</div>

Ao longo desse tutorial, você entendeu o que é Store Framework, Toolbelt e Store Theme, além de aprender como estruturar as páginas da sua loja configurando templates e customizando estilos. Para continuar aprendendo sobre o VTEX IO, não se esqueça de acessar o restante da nossa [documentação](link página docs). 



  

Vamos escrever um pouco de CSS, para acrescentar uma linha vermelha sólida:

  
