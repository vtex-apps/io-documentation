# *Setup* básico para desarrollar en VTEX IO
 
Todo desarrollo en VTEX IO comienza con [**VTEX IO CLI**](*link*), nuestra CLI (Command Line Interface) que permite iniciar sesión, desarrollar nuevos [apps](*link*) y gestionar los ya instalados.

## VTEX IO CLI

Para instalar la CLI de VTEX IO, debe asegurarse de que su computadora tenga [Node.js](https://nodejs.org/) e [Yarn](https://yarnpkg.com/) instalados.

Luego, digite `yarn global add vtex` en el terminal de su computadora.

```
$ yarn global add vtex
```

<div class="alert alert-warning">
Para confirmar que la instalación ocurrió con normalidad, puede ejecutar el comando <code>vtex</code>. Este deberá mostrar un texto de ayuda con todos los comandos disponibles.
</div>

## Login

Con la CLI de VTEX IO instalada, use el comando `vtex login` para entrar en su cuenta VTEX.

```
$ vtex login {ContaVTEX}
```

Esto abrirá una ventana de su navegador que solicitará sus credenciales.

Una vez que haya iniciado sesión, puede usar el comando `vtex whoami` para averiguar cuál cuenta y *workspace* están siendo utilizados por el terminal.

<img width="876" alt="VTEX IO CLI-whoami" src="https://user-images.githubusercontent.com/52087100/61886028-517e2780-aed5-11e9-9398-b6d2f3909a50.png">

## Creando su propio *workspace*

Al usar VTEX IO, toda interacción con una cuenta se produce en un [***workspace***](*link*). 

Cuando inicia sesión en una tienda, está automáticamente en el *workspace* master de esta, es decir, en la versión disponible para el usuario final. Por esto, recuerde  que siempre que quiera probar una nueva configuración, debe crear su propio *workspace* de desarrollo utilizando el comando `vtex use`.

```
$ vtex use {nombreejemplo}
```

Esto cambia su VTEX IO CLI a un *workspace* llamado `nombreejemplo` y lo crea si este no existe.

<img width="436" alt="workspace-nombreejemplo ES" src="https://user-images.githubusercontent.com/52087100/63979676-d1c51900-ca8f-11e9-826b-43293439e630.png">

<div class="alert alert-warning">
<code>vtex use</code> hace que todas sus operaciones se produzcan en el <i>workspace</i> definido en el comando. Esto significa que es posible alternar sus operaciones para master apenas ejecutando en VTEX IO CLI <code>vtex use master</code>, por ejemplo.
</div>

Con su propio *workspace* de desarrollo creado, puede navegar en su tienda accediendo a: 

`https://{{workspace}}-{{cuenta}}.myvtex.com`

Donde `workspace` es el *workspace* que usted acaba de crear (como `nombreejemplo`) y `cuenta` es el nombre de la cuenta en la que está trabajando.

¡Listo! Ahora ya puede desarrollar su tienda en VTEX IO.
