# Definiendo el tema de su tienda

El [**Store Theme**](*link*) es un tema estándar aplicable para todas las tiendas en la plataforma VTEX IO. El tema realiza dos acciones:

- **Declara *templates***, configurando y combinando componentes.

- **Declara estilos**, configurando colores primarios y secundarios, escalas de tipografía y espaciado, etc.

Esto significa que el Store Theme es un tema estándar responsable de definir la apariencia básica del *front* de su tienda.

El VTEX IO CLI de VTEX IO ofrece un comando `vtex init` que puede copiar rápidamente el Store Theme en su computadora para que pueda configurarlo y personalizarlo de acuerdo con las necesidades de su negocio.

>Tenga en cuenta que debe instalar las siguientes aplicaciones con los siguientes comandos: 

```
vtex install vtex.store-sitemap
vtex install vtex.store --force
vtex install vtex.admin-pages
```

## Implementando el Store Theme

Usando su terminal, navegue a un directorio ya existente de sus archivos locales donde desea copiar el Store Theme. Luego, use el comando `vtex init`, seleccione la opción `store-theme` y confirme que desea descargar el tema en la carpeta de destino previamente definida.

```
$ cd {{directorioejemplo}}
```

```
$ vtex init
```

Luego, usted recibirá informaciones importantes sobre el Store Theme, como *vendor*, nombre, título y su descripción. Con excepción de *vendor*, presione *Enter* para mantener los valores predeterminados de cada campo.

<div class="alert alert-info">
Reemplace el valor predeterminado de <i>vendor</i> con el nombre de la cuenta de la tienda en que está desarrollando para que posteriormente pueda publicar correctamente el tema en esta.
</div>

<img width="942" alt="VTEX IO CLI-store-theme-selection " src="https://user-images.githubusercontent.com/52087100/61887063-3d3b2a00-aed7-11e9-92b8-653c4972a218.png">

## *Linkeando* su código local a VTEX IO

Ahora que el Store Theme se ha copiado en sus archivos locales, debe ejecutar el comando `cd store-theme` en su terminal. Luego, ejecute `vtex link` para ver que se compile y publique el tema en la cuenta y el *workspace* que acaba de crear.

<div class="alert alert-warning">
 Ejecute <code>vtex whoami</code> para asegurarse de estar en la cuenta correcta y en un <i>workspace</i> de desarrollo. De lo contrario, el VTEX IO CLI no aceptará el link directo con el master.
</div>

```
$ cd store-theme
```

```
 $ vtex link
```

<img width="910" alt="VTEX IO CLI-vtex-link" src="https://user-images.githubusercontent.com/52087100/61887229-9dca6700-aed7-11e9-9934-030a153b75b6.png">
  
Al *linkear* el Store Theme, los archivos locales de su computadora se sincronizan con la plataforma VTEX IO. Esto significa que cualquier alteración que realice localmente en el código será enviada y reflejada en su <i>workspace</i>.

## Entendiendo la estructura del Store Theme

Echemos un vistazo a los archivos que se generaron en sus archivos locales para comprender la estructura del tema estándar. Puede navegar en su código con el editor de su preferencia.  

<img width="227" alt="vscode-folders-structure" src="https://user-images.githubusercontent.com/52087100/61887339-ce120580-aed7-11e9-8c7b-eb55d12def2b.png">

- **manifest.json**: archivo principal de cualquier app. Guarda metadatos importantes, como *vendor*, nombre, versión, dependencias de apps y *builders*.

- **store**: carpeta responsable de definir la estructura de una tienda. Es donde se configuran los componentes de cada página y sus propiedades.

- **styles**: carpeta responsable de definir el tema visual de una tienda, a través de la personalización de los componentes de cada página.

## Visitando su nueva tienda 

Navegue de nuevo hasta su tienda accediendo a:

`https://{{Workspace}}-{{AccountName}}.myvtex.com`

Después de iniciar sesión, debe ver el Store Theme ya reflejado en su tienda:

<img width="1426" alt="store-theme" src="https://user-images.githubusercontent.com/52087100/61896668-d4aa7800-aeeb-11e9-906b-9d6b04fd03c0.png">

Ahora que su tienda ya está en el aire con el tema estándar, podemos construir su identidad configurando sus *templates* y personalizando sus estilos.   

