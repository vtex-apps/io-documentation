# Personalizando estilos

El archivo `style.json` de la carpeta `styles` es el responsable por definir el estilo de su tema. Esto significa que usted puede personalizar la apariencia de toda su tienda apenas ajustando las definiciones estándares declaradas en este archivo, sin la necesidad de declarar CSS para los componentes de cada página.

Esta personalización puede realizarse de maneira fácil y rápida usando [VTEX Styleguide](https://styleguide.vtex.com/#/Styles), guía de estilos del archivo  `style.json` basado en una estructura CSS altamente configurable, el [VTEX Tachyons](https://vtex.github.io/vtex-tachyons/). 

Por ejemplo: podemos definir en el archivo `style.json` que el color de fondo del tema estándar ahora será azul. Para esto, basta alterar el valor de la propiedad `base` del bloque `semanticColors`: 

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

Guarde las alteraciones hechas en su código y verifique la nueva apariencia de su tienda:

<img width="1423" alt="STORE-THEME-BLUE-FORREAL" src="https://user-images.githubusercontent.com/52087100/61972132-31269980-afb7-11e9-863f-0727c363cb8f.png">


## Estilos avanzados con sustituciones de CSS

El archivo `style.json` posibilita la personalización de su tema de forma más genérica. Sin embargo, es posible que desee crear una identidad más personalizada para su tienda, definiendo una apariencia exclusiva para un componente de esta.

**Las sustituciones de CSS personalizan componentes para que estos asuman estilos diferentes del tema estándar**, sobrescribiendo lo que se declaró en el archivo `styles.json`. Es posible que desee que los Infocards de la página de inicio tenga un estilo diferente al resto de los componentes de su tienda, por ejemplo.

Usted declara nuevas sustituciones de CSS creando un archivo dentro de la carpeta `style` en `css`. El archivo creado debe tener como nombre el app cuya personalización se sobrescribirá, siguiendo el formato `vtex.{app}.css`. 

<div class="alert alert-info">
Verifique cuáles apps permiten que sus estilos sean sobreescritos accediendo al <code>manifest.json</code> de su tema.
</div>

Las clases deben personalizarse individualmente dentro del archivo. Puede encontrar las clases de un componente accediendo a la [documentación](*link*) de este.

En el archivo `vtex.store-components.css`, declare la siguiente sustitución de CSS:

```
.infoCardContainer {
 background-color: #E71111

}

```

Guarde los cambios y acceda a su tienda de nuevo para verificar el nuevo estilo rojo de Infocards para sobrescribir el azul predeterminado para su tienda:

<img width="1425" alt="banner-1-substituiçãocss-FORREAL" src="https://user-images.githubusercontent.com/52087100/61972638-7a2b1d80-afb8-11e9-8fd3-65e3852f1022.png">

<img width="1422" alt="banner-2-sobrescrevendo-FORREAL" src="https://user-images.githubusercontent.com/52087100/61972620-697aa780-afb8-11e9-81a9-729478961e62.png">

### Block Class

Ahora que aprendió cómo sobreescribir la apariencia de un componente, imagine la siguiente situación: en lugar de que todos los Infocards de su tienda tengan el mismo estilo, ahora desea que cada uno tenga uno.

Esto significa que no solo será necesario declarar una sustitución de CSS para el componente Infocard, sino también crear una sustitución de CSS para un bloque específico de este.

**El Block Class (**`"blockClass"`**) es una propiedad de algunos componentes del Store Theme que, cuando se declara en un bloque, permite su personalización exclusiva.** 

Por ejemplo: vamos a personalizar la manera como el bloque `info-card#bestdeals` se renderiza, agregando la prop `"blockClass"` a este:

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
La propiedad <code>"blockClass"</code> puede tener el valor de su preferencia, siempre que se haga su referencia correctamente en el archivo CSS creado.
</div>

Para hacer referencia correctamente al bloque, basta agregar el valor de la propiedad `"blockClass"` en una sustitución de CSS de su componente siguiendo el formato `.{class}--{blockClassvalue}`. 


```
.infoCardContainer--sales {
  background-color: #E6BB12
}

```

Una vez que haya guardado las alteraciones, podrá ver el Infocard con su personalización exclusiva:

<img width="1426" alt="infocard-yellow-forreal" src="https://user-images.githubusercontent.com/52087100/61976477-405f1480-afc2-11e9-842d-de5caa3f07d9.png">

<div class="alert alert-warning">
Las sustituciones de CSS solo pueden alterarse manualmente por código, mientras que las personalizaciones hechas por el archivo `style.json` pueden editarse fácilmente a través de la sección de Storefront del admin. Por lo tanto, cuando personalice el estilo de su tema, le recomendamos que evite realizar grandes personalizaciones que requieran de sustitución de CSS.
</div>

A lo largo de este tutorial, usted entendió qué es **Store Framework**, **VTEX IO CLI** y **Store Theme**, además de aprender cómo estructurar las páginas de su tienda configurando ***templates*** y personalizando **estilos**. Para continuar aprendiendo sobre VTEX IO, no olvide acceder al resto de nuestra [documentación](*link*). 

