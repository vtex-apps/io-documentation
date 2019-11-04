# Configurando *templates*

Cuando se crea una tienda, se debe configurar un ***template*** para cada una de las páginas que visitará el usuario, como la página de inicio, de producto, etc.

El modelo estándar Store Theme ya implementa *templates* básicos para las páginas de su tienda. Sin embargo, es posible configurarlos agregando o eliminando componentes a través de [**bloques**](*link*).

## Estructura de bloques

**Declaramos un nuevo bloque en un *template* para agregar un nuevo componente a una página**, al igual que podemos eliminar un bloque para que un componente se elimine de esta.

Como vimos anteriormente, la carpeta responsable por la organización de los bloques y *templates* de su tienda es `store`. Dentro de esta, puede declarar todos sus bloques en el archivo `blocks.jsonc` o crear tantas carpetas y archivos como desee para declararlos de forma organizada en la subcarpeta `blocks`.

Para comprender mejor esta estructura, echemos un vistazo al template predefinido por el Store Theme para la página de inicio de su tienda usando el editor de código de tu elección. Acceda a `store` > `blocks`> `home`> `home.jsonc` para ver el siguiente ejemplo:


```
{
 "store.home": {
  
 "blocks": [
     "carousel#home",
     "flex-layout.row#deals",
     "shelf#home",
     "info-card#home",
     "rich-text#question",
     "rich-text#link"
     "newsletter"
   ]
 }, 
    (...)
}
```
Como podemos ver, el *template* de la página de inicio estándar `store.home` declara los siguientes bloques: 

- `carousel#home`
- `flex-layout.row#deals`
- `shelf#home`
- `info-card#home`
- `rich-text#question`
- `rich-text#link`
- `newsletter`

Esto significa que estos bloques declarados serán, en el orden en que están dispuestos, los componentes de la página de inicio estándar de su tienda.

En este mismo archivo, la declaración de cada uno de estos bloques se puede encontrar más abajo, como es el caso de `rich-text#question`:

```
"rich-text#question": {
  "props": {
    "text": "**This is an example store built using the VTEX platform.\nWant to know more?**",
    "blockClass": "question"
  }
},
```

De acuerdo con las necesidades de su negocio, es posible personalizar los bloques ya declarados por Store Theme libremente, así como declarar nuevos.

## Declarando un nuevo bloque 
 
Vamos entonces a agregar un nuevo componente [**Infocard**](*link*) a la página de inicio de la tienda, antes del estante. Para esto, debemos agregar `info-cardf#bestdeals` al *template* `store.home` en `home.jsonc`. Despues vamos a declarar el bloque más abajo en este mismo archivo.
 
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

<div class="alert alert-info">
El comportamiento de los componentes de su tienda varía según las propiedades definidas para el bloque declarado. Consulte los ejemplos de configuración de bloques en la<a href="">documentación</a> de cada componente.
</div>

Al guardar sus alteraciones en el código y ejecutar `vtex link` en su terminal, deberá ver el nuevo Infocard renderizado al visitar la página de inicio de su tienda:

<img width="1422" alt="BANNER-INFOCARD-STEP4-FORREAL" src="https://user-images.githubusercontent.com/52087100/61972032-e73db380-afb6-11e9-833e-977964fe5105.png">

<div class="alert alert-warning">
Los cambios se reflejarán en el <i>workspace</i> en que estos se realizaron. Por esto, al comprobar la renderización del nuevo Infocard en su tienda, asegúrese de verificar a cuál <i>workspace</i> de la cuenta está accediendo.
</div>

Ahora que ya comprende la configuración de los *templates* de su tema, aprendamos a personalizar sus estilos.
