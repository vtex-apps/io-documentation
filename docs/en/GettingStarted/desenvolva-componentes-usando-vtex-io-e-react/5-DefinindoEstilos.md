# Definindo estilos

Após definir o bloco do seu tema, é hora de pensarmos no estilo que queremos para ele, definingo cores, tipografia, dentre outros elementos responsáveis por estabelecer a identidade visual do app quando renderizado. 

Para definir o estilo do(s) seu(s) componente(s), usaremos o mecanismo *Cascading Style Sheets* - **CSS**. 

No VTEX IO, existem três ferramentas diferentes para o uso de CSS em uma loja:

- **Tachyons** - Opção principal para a estilização dos componentes a partir de classes CSS.
- **CSS Modules** - Opção secundária para a estilização dos componentes a partir de classes CSS. Deve ser usado apenas quando o estilo desejado não pode ser configurado com o uso de Tachyons.
- **CSS Handles** - Exporta classes CSS genéricas para usuários do seu componente conseguirem customizá-lo de acordo com os seus respectivos cenários.

Uma vez que você conhece a diferença entre as ferramentas disponibilizadas pela plataforma, é hora de aprender mais sobre elas. 

Confira abaixo as instruções de uso para cada uma dessas ferramenta de acordo com o seu objetivo.

<div class="alert alert-info">
A customização do estilo de um componente pede conhecimentos básicos em CSS. Por isso, é indicado que você confira a <a href="https://www.w3schools.com/css/default.asp">documentação</a> dessa linguagem antes de seguir as intruções detalhadas abaixo.
</div>

## Usando Tachyons

VTEX Tachyons é uma estrutura CSS funcional construída com base no [Tachyons](https://tachyons.io/).

A estrutura consiste em ter classes CSS de propósito único que podem ser compostas para construir qualquer coisa, de layouts complexos a componentes responsivos. 

Na prática, o VTEX Tachyons ajuda você a usar classes CSS em seu app de front de loja sem grandes esforços.

<div class="alert alert-info">
Para entender melhor os tokens do VTEX Tachyons para classes CSS, é importante se familiarizar com a solução Tachyons. Portanto, leia atentamente sua <a href="https://tachyons.io/#getting-started">documentação</a>.
</div>

1. Abra o código da sua aplicação no seu editor de código.
2. Na pasta `react`, acesse o arquivo criado para o componente que você deseja estilizar.
3. Acesse a [documentação do VTEX Tachyons](https://vtex.github.io/vtex-tachyons/) e, de acordo com a customização desejada por você, procure as classes CSS mais adequadas.
4. No código do componente React, declare as classes CSS desejadas. Por exemplo:

```css
const Example = () => (
  <div className="flex justify-center pv4 ph3 bg-base--inverted">
    <p>Hello, World!</p>
  </div>
)
```

5. Salve as suas alterações. 

## Usando CSS Modules

CSS Modules é um arquivo CSS no qual as classes CSS são projetadas de acordo com o app de front de loja responsável por exportar o componente.

<div class="alert alert-warning">
Por definir classes de CSS nesses moldes, a ferramenta de CSS Modules se torna limitante quando pensamos nos cenários de importação e exportação de componentes entre diferentes apps. Por isso, recomendamos apenas o uso de VTEX Tachyons no seu projeto. <b>Use CSS Modules apenas para casos não solucionados pelo Tachyons.</b>
</div>

1. Na pasta `react` da sua app, crie o arquivo `styles.css`.
2. Dentro deste arquivo, crie as classes de CSS desejadas (aquelas não compreendidas pelos tokens do Tachyons). Por exemplo:

```css
.myButton {
   background-color: red;
}
```

3. Ainda na pasta `react`, acesse o arquivo do componente sendo customizado e importe o arquivo `styles`, criado no passo 1. Por exemplo:

```jsx
import styles from './styles.css'
```

4. É possível também importar o arquivo `styles` de modo que as classes de CSS a serem geradas sejam privadas, isso é, sejam geradas com um identificador único (*hash*) ao invés do formato tradicional `vendor-app-major-x-classname`. Para esse fim, você deve importar seguindo o modelo abaixo:

```jsx
import styleModule from './style.module.css'
```

5. A partir daí, o `styles` importado para o seu componente será um objeto cujas chaves serão os nomes das classes criadas por você (`className`). Por exemplo:

```jsx
/* /react/MyButton.tsx */
import styles from './styles.css'

export default function MyButton() {
  return (
    <button className={styles.myButton}>
      My button
    </button>
  )
}
```


<div class="alert alert-info">
Lembre-se que o nome das classes criadas dependerão do modelo de <i>import</i> feito por você (passo 3 ou passo 4 desta seção). 
</div>

6. Salve as mudanças efetuadas e faça o [link](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-linking-an-app/) do seu app. 

Ao ser renderizado e inspecionado, o componente agora apresentará a seguinte estrutura HTML caso você tenha optado por seguir o modelo de *import* apresentado no passo 3:

```html
<button class="vtex-my-app-name-0-x-myButton">My button</button>
```

## Usando CSS Handles 

Um CSS Handle é um **identificador de elemento HTML**. Por isso, os Handles são ótimos assistentes na criação de temas da loja, permitindo que os usuários do seu app apliquem classes de CSS conforme a identidade visual desejada por eles.

Para disponibilizar Handles aos futuros usuários do seu app, adicione` vtex.css-handles` na lista de `dependencies` do arquivo `manifest.json`:

```diff
  "dependencies": {
+   "vtex.css-handles": "0.x"	
  }
```

Uma vez que `vtex.css-handles` for adicionado como uma dependência, o seu app estará pronto para gerar CSS Handles.

Para gerá-los, contudo, precisaremos prestar atenção à forma como o(s) componente(s) React do seu app são importados e definidos. 

Os dois possíveis cenários aqui são:

- ***Function components*** - Componentes React são definidos na sua aplicação por meio de uma função.
- ***Class components*** - Componentes React são definidos na sua aplicaç!ao por meio de uma classe.

### Criando CSS Handles para componentes de funções

1. Na pasta `react` do seu app, acesse o arquivo do componente React desejado.
2. Copie e cole no arquivo o seguinte exemplo de código:

```jsx
import { useCssHandles } from 'vtex.css-handles'

const CSS_HANDLES = ['container', 'background', 'text', 'item'] as const
/* Using `as const at the end` hints to Typescript that this array
 * won't change, thus allowing autocomplete and other goodies. */

const Component: FC = () => {
  const handles = useCssHandles(CSS_HANDLES)  
```

3. No array `CSS_HANDLES`, substitua as strings exemplificadas por novas (de acordo com os nomes dos *CSS Handles* desejados). O nome do *CSS Handle* pode ser qualquer um de sua escolha, mas lembre-se: ele será usado com classes CSS pelos usuários do seu app para personalizar elementos HTML de lojas. Portanto, é recomendável que a escolha de nomes intuitivos.

*Seguindo o exemplo dado acima, a variável `(CSS_HANDLES)` será um objeto no seguinte formato:*
  
```json
{
  container: 'vtex-foobar-1-x-container',
  background: 'vtex-foobar-1-x-background',
  text: 'vtex-foobar-1-x-text',
  item: 'vtex-foobar-1-x-item',
}
```

<div class="alert alert-info">
Note que os CSS Handles gerados e armazenados no objeto seguem o padrão: <code>vtex-{appName}-{majorVersion}-x-{handleName}</code>.
</div>

4. Adicione o novo *CSS Handle* à classe CSS desejada - de acordo com o elemento HTML a ser personalizado pelos usuários do app. Lembre-se de usar a variável `handle` ao adicioná-lo e também o nome do *CSS Handle* definido no array` CSS_HANDLES` (como `container`). Por exemplo:

```css
    <div className={handles.container}>
      <div className={`${handles.background} bg-red`}>
        <h1 className={`${handles.text} f1 c-white`}>Hello world</h1>
        <ul>
          {['blue', 'yellow', 'green'].map(color => (
            <li
              className={`${handles.item} bg-${color}`}>
              Color {color}
            </li>
          ))}
        </ul>
      </div>
    </div>
```

### Criando CSS Handles para componentes de classe

1. Na pasta `react` do seu app, acesse o arquivo do componente React desejado.
2. Copie e cole no arquivo o seguinte exemplo de código:

```jsx
import { withCssHandles } from 'vtex.css-handles'

const CSS_HANDLES = ['text'] as const

class ExampleComponent extends Component {
  render() {
    const { cssHandles } = this.props
 ```
 
<div class="alert alert-info">
Como componentes definidos como classes não podem utilizar <i>hooks</i>, usaremos então um <i>HOC</i> chamado <code>withCssHandles</code>.
</div>

3. No *array* `CSS_HANDLES`, substitua as strings exemplificadas por novas (de acordo com os nomes dos *CSS Handles* desejados). O nome do *CSS Handle* pode ser qualquer um de sua escolha, mas lembre-se: ele será usado com classes CSS pelos usuários do seu aplicativo para personalizar elementos HTML. Portanto, recomendamos que você use nomes intuitivos.

*Seguindo o exemplo dado acima, a variável `{ cssHandles }` será um objeto no seguinte formato:*

```json
{
  text: 'vtex-foobar-1-x-text',
}
```

<div class="alert alert-info">
Note que os CSS Handles gerados e armazenados no objeto seguem o padrão: <code>vtex-{appName}-{majorVersion}-x-{handleName}</code>.
</div>

4. Adicione o novo *CSS Handle* à classe CSS desejada - de acordo com o elemento HTML a ser personalizado pelos usuários do app. Lembre-se de usar a variável `handle` ao adicioná-lo e também o nome do *CSS Handle* definido no array` CSS_HANDLES` (como `text`). Por exemplo:

```css
<div className={`${cssHandles.text} f1 c-white`}>Hello world</div>
```

Depois de salvar suas alterações, seu app será capaz de não apenas de exportar um estilo predefinido de acordo com as classes CSS configuradas por você, mas também de exportar *CSS Handles*, fornecendo aos seus usuários maior flexibilidade de personalização.

<div class="alert alert-info">
Para obter mais detalhes sobre como os <i>CSS Handles</i> podem ser usados para definir estilos, acesse a documentação <a href="https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-using-css-handles-for-store-customization/">Using CSS Handles for store customization</a>.
 </div>
