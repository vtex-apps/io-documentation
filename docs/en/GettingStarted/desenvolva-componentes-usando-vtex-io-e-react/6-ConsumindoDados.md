# Consumindo dados

Agora é preciso aprender como esse novo componente irá dialogar com o sistema *back-end*, isso é, como ele vai **consumir e inserir dados na plataforma**. 

A comunicação entre apps de front de loja e o VTEX IO é feita através de **APIs GraphQL**.

## Entendendo GraphQL

GraphQL é uma linguagem para APIs cuja principal vantagem é a **possibilidade de solicitar dados específicos através de um único endpoint**, evitando *overfetching* e *underfetching*.

Para fazer o gerenciamento dos dados consumidos em GraphQL, usaremos uma biblioteca chamada [**React Apollo**](https://www.npmjs.com/package/react-apollo), responsável por providenciar componentes nativos para a realização de buscas de dados.

Os principais componentes desta biblioteca são:

| Nome | Descrição |
|-----|-----|
|[useQuery](https://www.apollographql.com/docs/react/data/queries/) | *React Hook* que, quando executado, consulta o servidor usando *API GraphQL* e retorna o que foi solicitado nas variáveis da *query*. | 
|[useMutation](https://www.apollographql.com/docs/react/data/mutations/) | *React Hook* que retorna uma função que, quando executada, faz a comunicação com o servidor a partir de *API GraphQL* a fim de enviar *updates* e sobrescrever dados.  |

O *React Hook* `useQuery` retorna um objeto que contém as seguintes propriedades:

 - `loading` (`boolean`) - Retorna `true` caso a *API GraphQL* ainda esteja sendo executada . Caso contrário, retorna `false`.
 - `error` (`any`) - Só assume algum valor quando algum erro ocorre na comunicação com o servidor.
 - `data` (`any`) - Contém o objeto retornado a partir da execução da *query*.

Já o *React Hook* `useMutation` retorna um *array* com:

- Uma função que pode ser chamada a qualquer momento para executar a comunicação com o servidor.
- Um objeto que representa o estado atual da *mutation* com as propriedades `loading`, `error` e `data`.

Tendo em vista os objetos recebidos pelos *React Hooks* `useQuery` e `useMutation`, é possível definir o que se deseja renderizar em *React* para as condições específicas `loading` e `error`, além de gerenciar o conteúdo retornado por queries feitas na API (armazenado em `data`).

<div class="alert alert-warning">
Para compreender melhor as instruções detalhadas a seguir, é recomendável ter conhecimentos básicos de linguagem GraphQL. Caso você não seja familizarizado com a solução, é recomendado que você acesse a sua <a href="https://graphql.org/learn/">documentação</a> e faça uma leitura atenta antes de seguir para os próximos passos.
</div>

## Instalando a biblioteca React Apollo

Usando o seu terminal, acesse o diretório da sua app e execute o comando listado abaixo para instalar a biblioteca `npm` *React Apollo*: 

```sh
yarn add react-apollo
```

## Fazendo queries em GraphQL

Para que o seu componente renderize as informações disponibilizadas pela plataforma do VTEX IO, você deve consultar os dados armazenados no servidor através de *APIs GraphQL*.

![GraphQL-query](https://user-images.githubusercontent.com/52087100/86273914-4fbde900-bba7-11ea-8980-e984df5e7f25.gif)

Para isso, usaremos o *React Hook* `useQuery`:

1. Abra o código da sua app no editor de código de sua preferência.
2. Na pasta `react`, acesse o arquivo `HelloData.tsx` ou o crie caso ele ainda não exista.
3. Neste arquivo, copie e cole o modelo básico abaixo para construir a sua *query GraphQL*:

```jsx
import { useQuery } from 'react-apollo'
import QUERY_VALUE from './helloData.gql'

const HelloData = () => {
  const { loading, error, data } = useQuery(QUERY_VALUE)

  if (loading) {
    return 'Loading…'
  }
  if (error) {
    return `Error ${error}`
  }

  return `Done fetching ${data}`
}

export default HelloData
```

Note que a propriedade `QUERY_VALUE` está sendo importada de um outro arquivo chamado `helloData.gql`. A extensão `.gql` aponta que é um arquivo escrito em *GraphQL*. O conteudo desse arquivo varia de acordo com a *query* a ser requisitada pela aplicação.

Um exemplo simples para `helloData.gql` seria:

```gql
query hello {
  hero {
    name  
    height
  }
}
```

Cuja resposta, dependendo do banco de dados, poderia ser algo como:

```json
{
  "hero": {
    "name": "Luke Skywalker",
    "height": 1.72,
  }
}
```

Perceba como o React Hook `useQuery` retorna um objeto com os parâmetros `loading`, `error` e `data`, que são preenchidos a partir da consulta realizada no servidor. Detendo os valores destes parâmetros, é possível **condicionar o que é renderizado na interface.**

De acordo com o exemplo acima, temos que caso `loading` retorne `true`, a mensagem `Loading...` será renderizada. Caso algum erro ocorra, a mensagem `Error {descrição do erro}` será renderizada no lugar. Por fim, se o parâmetro `data` receber corretamente os valores da *query* executada, será renderizada a mensagem `Done fetching {dados obtidos a partir da query}`.

<div class="alert alert-info">
Confira <a href="https://www.apollographql.com/docs/react/data/queries/">aqui</a> um exemplo prático de uma query GraphQL sendo usada.
</div>

## Fazendo mutations em GraphQL

Além das *queries*, as *mutations* são um outro tipo de operação em APIs GraphQL. 

As *mutations* são utilizadas para inserir ou modificar dados já existentes na plataforma, sendo usadas para enviar *updates* ao servidor.

![GraphQL-mutation](https://user-images.githubusercontent.com/52087100/86273910-4f255280-bba7-11ea-8c2a-ab2db58951bd.gif)

1. Abra o código da sua app no editor de código de sua preferência.
2. Na pasta `react`, acesse o arquivo `HelloMutation.tsx` ou o crie caso ele ainda não exista.
3. Neste arquivo, copie e cole o modelo básico abaixo para executar uma *mutation* `gql` usando o componente *React*:

```jsx
import { useMutation } from 'react-apollo'
import MUTATION_VALUE from './helloMutation.gql'

const HelloMutation = () => {
  const [doSomething] = useMutation(MUTATION_VALUE)

  return <button onClick={() => { doSomething() }}>Click me</button>
}

export default HelloMutation
```

Neste caso, diferentemente do *hook* `useQuery` em que a *query* é executada imediatamente, a chamada ao servidor só será feita após chamar a função retornada pelo *hook* `useMutation` (neste exemplo, `doSomething`).

É possível adicionar parâmetros da *mutation* como variáveis da função `doSomething`.

Vamos dizer, por exemplo, que uma das variáveis da *mutation* que você está executando é o nome de uma cidade (`cityName`). Uma forma de passar essa variável seria:

```diff
- return <button onClick={() => { doSomething() }}>Click me</button>
+ return <button onClick={() => { doSomething({ variables: { cityName: 'Rio' ) }}>Click me</button>
```

<div class="alert alert-info">
Confira <a href="https://www.apollographql.com/docs/react/data/mutations/">aqui</a> um exemplo prático de uma mutation GraphQL sendo usada.
</div>

## Debuggando queries e mutations em GraphQL

Para testar *queries* e *mutations* GraphQL, usaremos o app GraphQL IDE.

Para instalar este app na sua conta VTEX, execute o seguinte comando no seu terminal:

```sh
vtex install vtex.admin-graphql-ide
```

Com o app instalado, siga os passos descritos abaixo:

1. Acesse o  admin  da conta VTEX em que você está trabalhando.
2. Na barra lateral, acesse **Aplicativos**.
3. Procure pelo GraphQL IDE na listagem de aplicativos instalados.
4. No campo `Choose your app from the list below`, selecione o nome do app em que você deseja realizar o debug/teste. Neste caso, o nome a ser escolhido deve ser o nome do app desenvolvido por você. 

<div class="alert alert-warning">
Lembre-se de que, até este momento, o app de front sendo desenvolvido por você mora nos seus arquivos locais, estando conectado com a plataforma VTEX apenas a partir do <code>link</code>. Para encontrar o nome da sua app nessa listagem e assim realizar o debug, é preciso que ela já esteja disponível (publicada) e devidamente instalada no workspace Master da conta. As configurações necessárias para tornar o seu app publicamente disponível estão descritas no último passo desta trilha.
</div>

5. No editor de texto à sua esquerda, escreva a *query* ou *mutation* que você deseja executar para fins de teste. 
6. Em seguida, clique no botão de *play* e a resposta da sua consulta à API aparecerá no editor de texto à sua direita. 

Para te auxiliar neste processo, há uma aba `docs` no canto direito da sua tela que descreve as queries e mutations disponíveis para a aplicação selecionada.

![Exemplo GraphQL IDE](https://camo.githubusercontent.com/7e7dc6c6c4463c904d1442fca59730dbc2d24082/68747470733a2f2f692e696d6775722e636f6d2f68734d747843322e706e67)
*O exemplo acima mostra a utilização do GraphQL IDE Admin para realizar a query de uma rota interna na aplicação `vtex.rewriter`.*


