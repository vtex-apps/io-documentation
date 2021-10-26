# Customizando estilos

O arquivo `style.json` da pasta `styles` é o responsável por definir o estilo do seu tema. Isso significa que você pode customizar a aparência de toda a sua loja apenas ajustando as definições padrões declaradas neste arquivo, sem precisar declarar CSS para os componentes de cada página.

Essa customização pode ser feita de maneira fácil e rápida usando o [VTEX Styleguide](https://styleguide.vtex.com/#/Styles), guia de estilos do arquivo `style.json` baseado em uma estrutura CSS altamente configurável, o [VTEX Tachyons](https://vtex.github.io/vtex-tachyons/).

Por exemplo: podemos definir no arquivo `style.json` que a cor de fundo do tema padrão agora será azul. Para isso, basta alterar o valor da propriedade `base` do bloco `semanticColors`:

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

```

Salve as alterações feitas no seu código e confira a nova aparência da sua loja:

<img width="1423" alt="STORE-THEME-BLUE-FORREAL" src="https://user-images.githubusercontent.com/52087100/61972132-31269980-afb7-11e9-863f-0727c363cb8f.png">

## Estilos avançados com substituições de CSS

O arquivo `style.json` possibilita a customização do seu tema de forma mais genérica. Mas pode ser que você queira criar uma identidade mais personalizada para a sua loja, definindo uma aparência exclusiva para um componente dela.

**As substituições de CSS customizam componentes para que eles assumam estilos diferentes do tema padrão**, sobrescrevendo o que foi declarado no arquivo `styles.json`. É possível que você deseje que os Infocards da página inicial tenha um estilo diferente do restante dos componentes da sua loja, por exemplo.

Você declara novas substituições de CSS criando um arquivo dentro da pasta `style`, em `css`. O arquivo criado deve ter como nome a app do seu tema que terá a sua customização sobrescrita, seguindo o formato `vtex.{app}.css`. 

<div class="alert alert-info">
Verifique quais apps do seu tema podem ter seus estilos sobrescritos acessando o <code>manifest.json</code> do seu tema.
</div>

As classes devem ser individualmente customizadas dentro do arquivo. Você pode encontrar as classes de um componente acessando a [documentação](*link*) dele.

No arquivo `vtex.store-components.css`, declare a seguinte substituição de CSS:

```
.infoCardContainer {
 background-color: #E71111

}

```

Salve suas alterações e acesse a sua loja mais uma vez para conferir o novo estilo vermelho dos infocards sobrescrever o azul pré-definido para a sua loja:

<img width="1425" alt="banner-1-substituiçãocss-FORREAL" src="https://user-images.githubusercontent.com/52087100/61972638-7a2b1d80-afb8-11e9-8fd3-65e3852f1022.png">

<img width="1422" alt="banner-2-sobrescrevendo-FORREAL" src="https://user-images.githubusercontent.com/52087100/61972620-697aa780-afb8-11e9-81a9-729478961e62.png">

### Block Class

Agora que você aprendeu como sobrescrever a aparência de um componente, imagine a seguinte situação: ao invés de todos os Infocards da sua loja terem o mesmo estilo, você agora deseja que cada um deles tenha um.

Isso quer dizer que será necessário não só declarar uma substituição de CSS para o componente Infocard, como também criar uma substituição de CSS para um bloco específico dele.

**O Block Class (**`"blockClass"`**) é uma propriedade de alguns componentes do Store Theme que, quando declarada em um bloco, permite a sua customização exclusiva.**

Por exemplo: vamos customizar a maneira como o bloco `info-card#bestdeals` é renderizado, adicionando a prop `"blockClass"` a ele:

<img width="639" alt="INFOCARD-BLOCKCLASS-FORREAL-REAL" src="https://user-images.githubusercontent.com/52087100/61976127-54564680-afc1-11e9-9f62-ab3473639805.png">

```
"info-card#bestdeals": {
    "props": {
      "id": "sales",
      "blockClass": "sales",
      "isFullModeStyle": false,
      "textPosition": "center",
      "imageUrl": "http://cybercitycomix.com/wp-content/uploads/2015/08/Sale-sign.jpg",
      "headline": "BEST DEALS",
      "callToActionText": "DISCOVER",
      "callToActionUrl": "/sale/d",
      "textAlignment": "center"
    }
  },

```

<div class="alert alert-info">
A propriedade <code>"blockClass"</code> pode ter o valor de sua preferência, desde que ele seja referenciado corretamente no arquivo de CSS criado. 
</div>

Para referenciar corretamente o bloco, basta adicionar o valor da propriedade `"blockClass"` em uma substituição de CSS do seu componente seguindo o formato `.{class}--{blockClassvalue}`.

```
.infoCardContainer--sales {
  background-color: #E6BB12
}

```

Depois de salvar as alterações feitas, você poderá visualizar o Infocard com a sua customização exclusiva:

<img width="1426" alt="infocard-yellow-forreal" src="https://user-images.githubusercontent.com/52087100/61976477-405f1480-afc2-11e9-842d-de5caa3f07d9.png">

<div class="alert alert-warning">
As substituições de CSS só podem ser alteradas manualmente por código enquanto as customizações feitas pelo arquivo <code>style.json</code> podem ser facilmente editadas através da seção de Storefront do admin. Por isso, ao customizar o estilo do seu tema, é recomendável evitar fazer grandes customizações que necessitem de substituição de CSS.
</div>

Ao longo deste tutorial, você entendeu o que é **Store Framework**, **VTEX IO CLI** e **Store Theme**, além de aprender como estruturar as páginas da sua loja configurando ***templates*** e customizando **estilos**. Para continuar aprendendo sobre o VTEX IO, não se esqueça de acessar o restante da nossa [documentação](*link*).
