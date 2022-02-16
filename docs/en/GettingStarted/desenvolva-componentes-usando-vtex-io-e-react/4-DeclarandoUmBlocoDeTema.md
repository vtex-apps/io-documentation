# Declarando um bloco de tema

Com o modelo da aplicação já copiado, vamos agora criar um **novo bloco de tema**. 

Antes de seguir para as instruções abaixo, é importante que você já conheça o VTEX Store Framework e entenda inteiramente o que é um bloco, tema de loja e template. 

Caso você ainda não seja familiarizado com esses conceitos ou queira relembrar um pouco deste universo antes de começar as suas configurações, acesse a trilha [**Build stores with Store Framework**](https://developers.vtex.com/vtex-developer-docs/docs/getting-started-3).

## Entendendo interfaces

Uma interface funciona basicamente como uma API (*application programming interface*) responsável por definir o comportamento que os blocos de tema devem assumir considerando o componente React que eles renderizam.

Da mesma forma que uma API usa parâmetros para definir como será a conversa com um servidor, a interface usa o que chamamos de *chaves*. 

**As interfaces, por meio das suas chaves, definem qual será o comportamento de um bloco quando implementado e renderizado em um tema de loja**. 

Isso significa que, para cada bloco de tema exportado pela sua aplicação, você precisará definir uma [interface](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-interfaces/), vinculando o bloco a um componente React de sua escolha.

A tabela a seguir mostra algumas chaves possíveis de serem adicionadas à interface do seu bloco, bem como as suas respectivas descrições:

| Chave | Descrição | 
|----- | ----- |
| `component` | Nome do componente React ao qual o bloco de tema está vinculado, ou seja, nome do componente React que o bloco de tema vai renderizar.|
| `allowed` | Lista de outros blocos de tema que, quando declarados, ajudarão a construir o componente React desejado. Na prática, os blocos declarados como `allowed` devem ser declarados na app de tema (Store Theme) como filhos do bloco desenvolvido por você.|
| `composition` | Define se os filhos do bloco sendo desenvolvido por você terão uma posição de renderização específica na interface ou não. Lembre-se de que ao definir a chave `composition`, você não está controlando o posicionamento do bloco sendo definido por ela, mas sim o posicionamento dos filhos desse bloco. Os valores possíveis para esta chave são: `blocks` (os blocos filhos têm uma posição específica na interface, de acordo com o componente React nos quais eles se baseiam) ou `children` (a posição dos blocos filhos depende exclusivamente da maneira como são declarados no tema). Se nenhum valor para a chave `composition` for definido, o padrão assumido pela plataforma é `blocks`.|
| `device` | Define se o seu bloco de tema é projetado para dispositivos móveis ou desktop. Os valores possíveis são: `mobile` (projetado para dispositivos móveis) e `desktop` (projetado para dispositivos desktop).|
| `required` | Lista de blocos de tema que necessariamente devem ser renderizados na interface para suportar a renderização bloco que você está desenvolvendo.|
| `around` | Lista de blocos de tema que devem ser renderizados na interface ao entorno do seu novo bloco para o seu correto funcionamento. |
| `before` | Lista de blocos de tema que devem ser renderizados na interface antes do seu bloco (acima dele) para o seu correto funcionamento. Por exemplo: cabeçalho. |
| `after` | Lista de blocos de tema que devem ser renderizados na interface após o seu bloco (abaixo dele) para o seu correto funcionamento. Por exemplo: rodapé. |
| `preview` | Define o comportamento da página enquanto o bloco é carregado. |
| `render` | Define o tipo de renderização do bloco. Os valores possíveis são: `lazy` (o bloco só é renderizado quando um usuário interage com ele),` server` (a renderização do bloco é feita pelo lado do servidor) ou `client` (a renderização do bloco é feita pelo lado do cliente, ou seja, pelo navegador). |

A única chave obrigatória a ser declarada na interface de um bloco é a `component`. As demais devem ser declaradas por você de acordo com o cenário desejado para o seu novo bloco de tema.
 
## Declarando uma interface

Declaramos a interface de um ou mais blocos no arquivo `interfaces.json` da aplicação, usado pelo [Store Builder](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-builders/) para construir corretamente o *front-end* do seu website.

Para este exemplo, vamos criar uma interface para um bloco básico chamado `hello-world` (baseado no componente React `HelloWorld`). 

Ao seguir o passo a passo, lembre-se de substituir os valores de acordo com o cenário real da sua aplicação, de acordo com o componente React realmente sendo importado por você.

1. Abra o código do seu app (anteriormente denominado `react-app-template`) no seu editor de código.
2. Na pasta `react`, crie um novo arquivo TypeScript com o nome do componente React desejado. De acordo com o nosso exemplo, teríamos `HelloWorld.tsx`.
3. Uma vez no arquivo, adicione o código exemplo abaixo (substituindo os valores de acordo com seu cenário):

```jsx
import { React } from 'react'

const HelloWorld = () => <div>Hello, World!</div>

export default HelloWorld
```

<div class="alert alert-info">
Não se esqueça de conferir a <a href="https://reactjs.org/docs/getting-started.html">documentação da solução React</a> para entender melhor o funcionamento de componentes.
</div>

4. No primeiro nível de pastas do seu aplicativo, crie uma nova chamada `store`.
5. Na pasta `store`, adicione um novo arquivo chamado `interfaces.json`.
6. Declare no novo arquivo a interface do componente. Por exemplo:

```json
{
 "hello-world": {
    "component": "HelloWorld"
  }
}
```

Observe a estrutura acima: a primeira definição dada pela interface é o nome do seu novo bloco de tema (`hello-world`). Dentro dele, declaramos um objeto contendo as chaves da interface apresentadas anteriormente.

Em nosso exemplo básico, usamos apenas a chave `component` para vincular o bloco` hello-world` ao componente React que ele irá renderizar (`HelloWorld`). Observe que o valor da chave `component` é `HelloWorld` - nome do arquivo criado anteriormente para o componente React (`react / HelloWorld.tsx`).

<div class="alert alert-info">
Não deixe de conferir o código de aplicações nativas do Store Framework para aprender mais sobre a estruturação do arquivo <code>interfaces.json</code>, como o da <a href="https://github.com/vtex-apps/search-result/blob/master/store/interfaces.json">Search Result</a> e <a href="https://github.com/vtex-apps/store-header/blob/master/store/interfaces.json">Header</a>. Lembre-se de que a maneira como declaramos uma interface depende diretamente do comportamento que queremos para o novo bloco. Por isso, à medida que estudamos diferentes apps e blocos, entendemos mais as possibilidades de interfaces.
</div>

Depois de salvar suas alterações no código, o seu novo bloco estará pronto para ser implementado por qualquer usuário que instalar a sua aplicação.

<div class="alert alert-info">
Se a aplicação em desenvolvimento exportar mais do que um bloco de tema para a renderizacao do componente React, as interfaces de todos esses blocos também devem ser declaradas no arquivo <code> interfaces.json</code>, de acordo com o formato indicado acima.
</div>

### Declarando diferentes interfaces por breakpoint 

É possível que você queira que a sua aplicação exporte diferentes blocos para a renderização de diferentes componentes de acordo com o *breakpoint* da loja, isso é, de acordo com o dispositivo através do qual ela está sendo acessada.

Para isso, você deverá criar blocos diferentes para cada possível dispositivo e, consequentemente, criar interfaces para cada um deles. 

Por exemplo: você está desenvolvendo o bloco `hello-world` e deseja criar para ele uma versão móvel e uma desktop. Deve-se criar então os componentes `HelloWorld`, `HelloWorldMobile` e `HelloWorldDesktop`, e definir interfaces para cada um deles, como `hello-world`, `hello-world.mobile` e `hello-world.desktop`. 

A interface `hello-world` do bloco pai deve conter apenas as chaves `component` e `allowed`, esta última declarando os blocos `hello-world.mobile` e `hello-world.desktop`. 

As interfaces dos últimos blocos, por sua vez, devem declarar as chaves desejadas para definir o comportamento de cada bloco de acordo com o dispositivo para o qual foram projetadas, como a chave `device`. 

Exemplos de apps que usam diferentes componentes React para diferentes dispositivos são [Header](https://github.com/vtex-apps/store-header) e [Footer](https://github.com/vtex-apps/store-footer).

## Usando o seu novo bloco de tema

Vamos implementar agora o novo bloco criado por você.  

Se a conta VTEX na qual você está trabalhando já possui a Store Theme do VTEX Store Framework instalada, siga a intrução abaixo a partir do passo 2. Caso a sua conta ainda não tenha a Store Theme app instalada, siga as instruções normalmente a partir do primeiro passo:

1. Leia atentamente o [passo 3 da trilha Build stores with Store Framework](hhttps://developers.vtex.com/vtex-developer-docs/docs/getting-started-3) e siga os passos detalhados no artigo. Ao final dele, você terá implementado o tema padrão do VTEX Store Framework e estará pronto para testar o seu novo bloco.
2. Abra a pasta da aplicação Store Theme nos seus arquivos locais usando o editor de código de sua escolha.
3. No arquivo `manifest.json` da Store Theme, adicione a aplicação de front sendo desenvolvida por você como uma dependência em `dependencies`. Por exemplo:

```diff
  "dependencies": {
+   "yourVTEXAccountName.yourAppName": "0.x",
    "vtex.store": "2.x",
    "vtex.store-header": "2.x",
    "vtex.product-summary": "2.x",
    "vtex.store-footer": "2.x",
    "vtex.store-components": "3.x",
    ...
}
```

4. Adicione então o novo bloco de tema (em nosso exemplo, `hello-world`) a um dos templates. Para este passo a passo, adicionaremos o bloco `hello-world` à página inicial da loja, no template `store.home`:

```diff
{
  "store.home": { 
    "blocks": [
+     "hello-world"
    ]
  },
  ...
}
```

5. Faça o [link](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-linking-an-app/) do tema da loja com a plataforma VTEX IO para verificar os resultados:

[![image](https://user-images.githubusercontent.com/18701182/78390827-9bb6bd00-75bb-11ea-837e-4cb5aaac9e32.png)](https://user-images.githubusercontent.com/18701182/78390827-9bb6bd00-75bb-11ea-837e-4cb5aaac9e32.png)

6. Acesse a sua loja VTEX usando a estrutura `{workspaceName}-{accountName}.myvtex.com` para ver seu novo bloco `hello-world` sendo exibido no seu *workspace* de desenvolvimento:

[![image](https://user-images.githubusercontent.com/18701182/78391781-74f98600-75bd-11ea-9482-2b68f6549caa.png)](https://user-images.githubusercontent.com/18701182/78391781-74f98600-75bd-11ea-9482-2b68f6549caa.png)
