# Traduzindo o componente

Antes de pensar na globalização da sua marca, é crucial primeiramente cuidar da **internacionalização do conteúdo do seu website**. 

O **Messages** é o app do VTEX IO responsável pela tradução dos componentes de uma loja, atuando diretamente no código dos blocos para que o ciclo de desenvolvimento não seja limitado pelo fluxo necessário de versionamento de um idioma para outro.

Uma vez implementado na aplicação, o Messages se responsabiliza por identificar e interpretar automaticamente as mensagens de texto passivas de tradução, reduzindo obstáculos para a evolução do seu código - salvo os casos em que alguma tradução customizada já tenha sido manualmente inserida por você.

## Configurando o Messages

Para o funcionamento esperado do Messages, usaremos a biblioteca [`react-intl`](https://formatjs.io/docs/react-intl). Funcionando como motor de tradução, essa biblioteca altamente versátil possui uma série de recursos avançados de internacionalização (*i18n*) para a sua aplicação de *front*. 

1. Abra o código do seu app no editor de código de sua preferência.
2. Acesse a pasta `react` e execute em seguida o comando `yarn add react-intl@3 && yarn add @types/react-intl@3 --dev`.
3. Acesse o arquivo `manifest.json` e adicione o builder `messages` à lista de `builders`, conforme mostra o exemplo a seguir:

```diff
{
  ...
  "builders": {
    "react": "3.x",
    "docs": "0.x",
+   "messages": "1.x"
  },
  ...
}
```

4. Salve as alterações feitas no código. 

Pronto! Com todas as dependências do `react-intl` instaladas e o [builder](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-builders/) de Messages configurado, podemos avançar para as próximas etapas.

## Permitindo tradução automáticas

Para entendermos na prática como funcionam as traduções do VTEX IO, considere o componente React `HelloWorld` importado no passo 3 desta track:

```ts
import React from 'react'

const HelloWorld = () => <div>Hello World!</div>

export default HelloWorld
```

Note que, independentemente do idioma usado na página da loja, o texto `Hello World!` será renderizado no componente. 

Para que o texto `Hello World!` seja automaticamente traduzido quando o idioma da página for alterado, devemos utilizar o componente `FormattedMessage` do pacote `react-intl`, responsável por indicar quais strings devem ser traduzidas para outros idiomas.

Como parâmetro do componente `FormattedMessage`, teremos um ID (`id`) único associado a uma string específica declarada na sua aplicação: 

1. Substitua o código do componente `HelloWorld` para o código abaixo:

```ts
import React from 'react'
import { FormattedMessage } from 'react-intl'

const HelloWorld = () => {
  return (
    <div>
      <FormattedMessage id="store/my-app.hello"/>
    </div>
  )
}

export default HelloWorld
```

<div class="alert alert-warning">
Note que no exemplo acima usamos o componente <code>FormattedMessage</code> o associando ao ID <code>"store/my-app.hello"</code>, criada para o nosso exemplo. Como cada ID deve ser vinculado somente a uma única string, é necessário definir nesta pasta o componente <code>FormattedMessage</code> quantas vezes for preciso de acordo com as strings passíveis de tradução.
</div>

<div class="alert alert-info">
Ao criar um <code>id</code>, considere utilizar os prefixos <code>store/</code> ou <code>admin/</code> (dependendo da funcionalidade da sua app) seguido pelo nome da aplicação (<code>my-app</code>) e, por fim, uma palavra curta capaz de identificar a string em questão. Por exemplo: <code>store/my-app.hello</code>.
</div>

2. No diretório raiz da sua app, crie uma pasta `messages`.
3. Na pasta recém criada, crie um novo arquivo `.json` cujo nome será a siga ISO do idioma desejado. Por exemplo: `pt`, `en`, `fr`. 
4. No arquivo do idioma desejado, como `messages/en.json`, associe o `id` usado no componente `FormattedMessage` à string desejada:

```json
{
  "store/my-app.hello" : "Hello World!"
}
```

5. Salve todas as alterações feitas no código.

Ao [*linkar*](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-linking-an-app/) a sua app novamente e mudar o idioma da sua página, você perceberá que o texto `Hello World!` foi automaticamente traduzido na UI graças ao componente da biblioteca `react-intl` e ao Messages.

<div class="alert alert-info">
Para testar esses efeitos na loja vinculada a sua conta VTEX, acesse <code>https://{workspaceName}-{accountName}.myvtex.com</code> e adicione a query string <code>cultureInfo</code> com o valor do idioma desejado. Para verificar, por exemplo, a sua página em português do Brasil, digite: <code>https://{workspaceName}-{accountName}.myvtex.com/?cultureInfo=pt-BR</code>, substituindo <code>{workspaceName}</code> e <code>{accountName}</code> pelo nome do workspace de desenvolvimento sendo usado e pelo nome da sua conta VTEX, respectivamente.
</div>

## Sobreescrevendo traduções automáticas

De acordo com o seu cenário de negócio, é possível que você queira mudar uma tradução realizada automaticamente por outra customizada. 

Nesta seção, ensinaremos como você deve sobrescrever as traduções automáticas do Messages considerando o mesmo exemplo utilizado anteriormente:

1. Na pasta `Messages`, acesse o arquivo desejado por você de acordo com o idioma da tradução que será sobrescrita (`messages/pt.json`, por exemplo).
2. Neste arquivo, defina uma nova tradução para o mesmo `id` previamente vinculado à string desejada. Por exemplo:

```json
{
  "store/my-app.hello" : "Olá, pessoal!"
}
```

Ao vincular o mesmo `id` a outra tradução, você estará falando para o VTEX IO ignorar a tradução automática do Messages e considerar unicamente esta definida manualmente por você. 

Faça o [*link*](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-linking-an-app/) novamente da sua app e altere o idioma da página para português para conferir a tradução definida por você ser renderizada!

## Traduções avançadas

A internacionalização de um componente pode significar mais do que a tradução de suas strings. Ela pode incluir, por exemplo, mudança na formatação dos seus preços e suas porcentagens.

Levando em consideração o objetivo da sua aplicação, você pode (e deve) fazer alguns ajustes nas mensagens renderizadas quando elas apresentarem:

- Representação de preço;
- Valores variáveis;
- Dependência de concordância em gênero e número;
- Representação de porcentagens;
- Mensagens dinâmicas, como as de erro.

### Ajustando representação de preços

A formatação utilizada para descrever preços varia de país para país. Se a aplicação sendo desenvolvido por você envolve variáveis de preço, é fundamental torná-la pronto para lidar com os diferentes cenários que a internacionalização pode trazer.

Para automatizar essas mudanças de preço no fluxo de tradução, é preciso adicionar a biblioteca `vtex.format-currency` às dependências da sua app: 

1. Acesse o arquivo `manifest.json` e adicione `vtex.format-currency` na listagem de `dependencies`:

```diff
  dependencies: {
+   "vtex.format-currency": "0.x"
  }
```

2. Acesse o arquivo criado na pasta `react` para o componente React importado. 
3. Uma vez nele, importe o componente `FormattedCurrency` de `vtex.format-currency`. 
4. Utilize o padrão `<FormattedCurrency value={price} />` para indicar que a variável `price` deve ser tratada como o valor da notação de preço. Por exemplo:

```ts
import React from 'react'
import { FormattedCurrency } from 'vtex.format-currency'

const PriceComponent = () => {
  const price = 10.50

  return (
    <div>
      <FormattedCurrency value={price} />
    </div>
  )
}

export default PriceComponent
```

4. Salve as alterações feitas no código.

### Ajustando valores variáveis

É comum precisarmos incluir uma variável no meio da mensagem renderizada pelo componente. 

Considere o `HelloWorld`, por exemplo. Para renderizar um cumprimento seguindo o formato `Olá, {userName}!.`, devemos utilizar a **interpolação de variáveis**.

Considerando que você já tenha adicionado o pacote `react-intl` às dependências da sua app, como explicado anteriormente neste mesmo passo, siga as instruções abaixo:  

1. Acesse o arquivo criado na pasta `react` para o componente React importado. 
2. Uma vez nele, importe o componente `FormattedMessage` de `react-intl`, definindo a variável `user` (enviada como parâmetro do componente) usando o seguinte formato padrão: `<FormattedNumber id={id} values={{ user: user }}/>`. Por exemplo:

```ts
import React from 'react'
import { FormattedMessage } from 'react-intl'

const HelloUser = () => {
  const user = 'John'

  return (
    <div>
      <FormattedMessage id='store/my-app.hello-user' values={{ user: user }} />
    </div>
  )
}

export default HelloUser
```

3. Acesse o arquivo responsável pelas traduções do Messages de acordo com o idioma desejado (`messages/en.json`, por exemplo).
4. Defina para o `id` do `FormattedMessage` (no nosso exemplo, `store/my-app.hello-user`) a string que será renderizada em inglês usando o valor passado em `user`:

```json
{
    "store/my-app.hello-user" : "Hello {user}!"
}
```

5. Salve as alterações feitas no código.

<div class="alert alert-info">
Caso a construção da string pareça complexa, recomendamos a leitura atenta desta <a href="https://format-message.github.io/icu-message-format-for-translators/index.html">documentação</a>. Ela irá auxiliar o seu processo de aprendizagem, explicando mais detalhes sobre a formatação de mensagens utilizando ICU e interpolação de variáveis.
</div>

### Ajustando concordância em genêro e número

O gênero e número de uma variável têm impacto direto na construção de uma string.

Por exemplo: quando realizamos uma busca, esta pode não retornar nada, retornar um resultado, ou até vários resultados simultâneamente. Com isso, a resposta que desejamos renderizar para o usuário não se manterá constante, variando de acordo com a busca realizada e os resultados encontrados. 

Analisando este caso, poderíamos renderizar  `No products found`, `One product found` e `X products found`, respectivamente. 

Para fazer com que as mensagens da sua app tenham concordância em gênero e número de acordo com o cenário vigente, utilizaremos a **interpolação de variáveis**.

Considerando que você já tenha adicionado o pacote `react-intl` às dependências da sua app, como explicado no início deste artigo, siga as instruções abaixo:

1. Acesse o arquivo criado na pasta `react` para o componente React importado. 
2. Importe o componente `FormattedMessage` de `react-intl`, definindo a variável `myQuantity` (enviada como parâmetro do componente). Use o seguinte formato padrão: `<FormattedNumber id={id} values={{ quantity: myQuantity }}/>`. Por exemplo:

```ts
import React from 'react'
import { FormattedMessage } from 'react-intl'

const PluralSingularComponent = () => {
  const myQuantity = 1

  return (
    <div>
      <FormattedMessage id='store/my-app.pluralsingular' values={{ quantity: myQuantity }} />
    </div>
  )
}

export default PluralSingularComponent
```

3. Acesse o arquivo responsável pelas traduções do Messages de acordo com o idioma desejado (`messages/en.json`, por exemplo).
4. Defina para o `id` do `FormattedMessage` (no nosso exemplo, `store/my-app.pluralsingular`) a string que será renderizada em inglês de acordo com o valor retornado por `myQuantity`:

```json
{
    "store/my-app.pluralsingular" : "{quantity, plural, =0 {No product found} one{One product found} other{# products found}}"
}
```

5. Salve as alterações feitas no código.

<div class="alert alert-info">
Caso a construção da string pareça complexa, recomendamos a leitura atenta desta <a href="https://format-message.github.io/icu-message-format-for-translators/index.html">documentação</a>. Ela irá auxiliar o seu processo de aprendizagem, explicando mais detalhes sobre a formatação de mensagens utilizando ICU e interpolação de variáveis.
</div>

### Ajustando representação de porcentagens

Assim como preços, as porcentagens são expressas de diferentes formas dependendo da localidade em que estamos. 

Caso a aplicação sendo desenvolvida por você envolver variáveis com porcentagem, é fundamental torná-la pronta para os diferentes cenários que a internacionalização pode trazer.

Considerando que você já tenha adicionado o pacote `react-intl` às dependências da sua app, como explicado no início deste artigo, siga as instruções abaixo:  

1. Acesse o arquivo criado na pasta `react` para o componente React importado. 
2. Importe o componente `FormattedNumber` de `react-intl`, definindo as propriedades `value` e `style` no formato: `<FormattedNumber value={variable} style="percent"/>`. Por exemplo:

```ts
import React from 'react'
import { FormattedNumber } from 'react-intl'

const PercentageComponent = () => {
  const percent = 0.1

  return (
    <div>
      <FormattedNumber value={percent} style="percent" />
    </div>
  )
}

export default PercentageComponent
```

3. Salve as alterações feitas no código.

### Ajustando mensagens dinâmicas

Há casos em que a mensagem exibida pelo bloco não pode ser previamente definida por você, uma vez que ela depende diretamente das ações realizadas pelos usuários durante a navegação. Um caso comum de mensagens dinâmicas na interface são mensagens para erros HTTP.

Considerando que você já tenha adicionado o pacote `react-intl` às dependências da sua app, como explicado no início deste artigo, siga as instruções abaixo:  

1. Acesse o arquivo criado na pasta `react` para o componente React importado. 
2. Importe o componente `FormattedMessage` de `react-intl`, definindo a variável `errorCode` (enviada como parâmetro do componente) de acordo com o HTTP status code retornado. Por exemplo:

```ts
import React from 'react'
import { FormattedMessage, defineMessages } from 'react-intl'

const messages = defineMessages({
  404: {
    id: 'store/my-app.errors.404',
  },
  500: {
    id: 'store/my-app.errors.500',
  },
})

const ErrorMessage = ({ errorCode = 500 }) => {
  return {
    <div>
      <FormattedMessage id={messages[errorCode].id} />
    </div>
  }
}

export default ErrorMessage
```

3. Salve as alterações feitas no código.

<div class="alert alert-info">
Note que usamos uma variável para escolher o <code>id</code> usado no componente <code>FormattedMessage</code>, tornando a mensagem dinâmica. Para declarar mensagens dinâmicas no código do seu bloco, é necessário que todas as possíveis mensagens exportadas por ele sejam descritas em um objeto passado na função <code>defineMessages</code> do pacote <code>react-intl</code>. Essa função, que retorna o mesmo objeto sem alterações, é útil para que o código possa ser analisado estaticamente, garantindo que o Messages entregue apenas as mensagens necessárias para o browser renderizar.
</div>

