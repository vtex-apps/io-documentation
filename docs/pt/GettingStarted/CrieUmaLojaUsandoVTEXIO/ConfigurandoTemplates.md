# Configurando templates

Quando uma loja é criada, um __template__ deve ser configurado para cada uma das páginas que o usuário irá visitar, como a página inicial, de produto, etc.

O modelo padrão Store Theme já implementa templates básicos para as páginas da sua loja. Porém, é possível que você os configure adicionando ou removendo componentes através de [__blocos__](*link doc*). 

Declaramos um novo bloco em um template para adicionarmos um novo componente a uma página, da mesma forma que podemos remover um bloco para que um componente seja excluído dela. 

Como vimos anteriormente, a pasta responsável pela organização dos blocos e templates da sua loja é a `store`.  Dentro dela, você pode declarar todos os seus blocos no arquivo `blocks.jsonc` ou criar quantas pastas e arquivos forem desejados para declará-los de forma organizada na subpasta `blocks`. 

Para compreender melhor essa estrutura, vamos dar uma olhada no template pré-definido pelo Store Theme para a página inicial da sua loja, acessando `store` > `blocks`> `home`> `home.jsonc`. 


```
{
 "store.home": {
   "blocks": [
     "carousel#home",
     "flex-layout.row#deals",
     "shelf#home",
     "info-card#home",
     "rich-text#question",
     "rich-test#link"
     "newsletter"
   ]
 }, 
    (...)
}
```
Como podemos ver, o template da página inicial padrão `store.home` declara os seguintes blocos: 

- carousel#home
- flex-layout.row#deals
- shelf#home
- info-card#home
- rich-text#question
- rich-text#link
- newsletter

Isso quer dizer que esses blocos declarados serão, na ordem em que estão dispostos, os componentes da página inicial padrão da sua loja. 

Neste mesmo arquivo, a declaração de cada um desses blocos pode ser encontrada mais abaixo, como é o caso do `rich-text#question` :

```
"rich-text#question": {
  "props": {
    "text": "**This is an example store built using the VTEX platform.\nWant to know more?**",
    "blockClass": "question"
  }
},
```

De acordo com as necessidades do seu negócio, é possível personalizar os blocos já declarados pela Store Theme livremente, assim como declarar novos.

## Declarando um novo bloco 
 
Vamos então adicionar um novo componente [__Shelf__](*link doc de shelf*) à página inicial da loja. Para isso, devemos adicionar `shelf#deals` ao template `store.home` em `home.jsonc` de acordo com o posicionamento desejado para o componente e declarar o bloco mais abaixo neste mesmo arquivo.
 
<img width="684" alt="shelf#deals declared" src="https://user-images.githubusercontent.com/52087100/61897575-b9406c80-aeed-11e9-8656-c736e53ffcd8.png">


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
        "titleText": "Top sellers"
      }
    }
  },

  "product-summary#deals": {
    "props": {
      "isOneClickBuy": false,
      "showBadge": true,
      "badgeText": "OFF",
      "buyButtonText": "Add to cart",
      "displayBuyButton": "displayButtonAlways",
      "showCollections": false,
      "showListPrice": true,
      "labelSellingPrice": "To",
      "labelListPrice": "From",
      "showLabels": true,
      "showInstallments": true,
      "showSavings": true,
      "name": {
        "showBrandName": true,
        "showSku": true,
        "showProductReference": true
      }
    }
  },

```
<div class=“alert alert-info”>
O comportamento dos componentes da sua loja varia de acordo com as propriedades definidas para o bloco declarado. Confira os exemplos de configuração de blocos na [documentação](*link página doc componentes*) de cada componente. 
</div>

Ao salvar suas alterações no código e rodar `vtex link` no seu terminal, você deverá ver a nova prateleira renderizada ao visitar a página inicial da sua loja:

<img width="1426" alt="best-deals" src="https://user-images.githubusercontent.com/52087100/61897037-93ff2e80-aeec-11e9-9a1c-33e0dc68e031.png">

<div class=“alert alert-warning”>
As mudanças serão refletidas no workspace em que elas foram feitas. Por isso, ao conferir a renderização da nova prateleira na sua loja, não se esqueça de conferir qual workspace da conta você está acessando.
</div>

 
