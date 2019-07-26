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
 
Vamos então adicionar um novo componente [__Infocard__](*link doc infocard*) à página inicial da loja, antes da prateleira. Para isso, devemos adicionar `info-cardf#bestdeals` ao template `store.home` em `home.jsonc` e declarar o bloco mais abaixo neste mesmo arquivo.
 
<img width="645" alt="newblock-step4" src="https://user-images.githubusercontent.com/52087100/61960418-ca47b700-af9b-11e9-8787-b68cafae1225.png">


```
"info-card#bestdeals": {
   "props": {
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

<div class=“alert alert-info”>
O comportamento dos componentes da sua loja varia de acordo com as propriedades definidas para o bloco declarado. Confira os exemplos de configuração de blocos na [documentação](*link página doc componentes*) de cada componente. 
</div>

Ao salvar suas alterações no código e rodar `vtex link` no seu terminal, você deverá ver o novo Infocard renderizado ao visitar a página inicial da sua loja:

<img width="1422" alt="BANNER-INFOCARD-STEP4-FORREAL" src="https://user-images.githubusercontent.com/52087100/61972032-e73db380-afb6-11e9-833e-977964fe5105.png">

<div class=“alert alert-warning”>
As mudanças serão refletidas no workspace em que elas foram feitas. Por isso, ao conferir a renderização do novo infocard na sua loja, não se esqueça de conferir qual workspace da conta você está acessando.
</div>

