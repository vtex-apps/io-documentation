# Criando a nova aplicação

Para começar o desenvolvimento da sua aplicação de forma otimizada, você deverá:

- Copiar para os seus arquivos locais um [repositório modelo](https://github.com/vtex-apps/react-app-template).
- Realizar as primeiras e principais alterações no arquivo `manifest.json` da aplicação React exemplo. 

Isso deve ser feito para que você não precise se preocupar com configurações padrões da plataforma VTEX IO, uma vez que o repositório copiado já importará automaticamente os ajustes básicos necessários para você começar a desenvolver a sua aplicação.  

## Clonando o repositório modelo para os seus arquivos locais

Usando o seu terminal, execute o comando abaixo para clonar o repositório modelo para os seus arquivos locais: 

```sh
git clone https://github.com/vtex-apps/react-app-template
```

Em seguida, abra o diretório da aplicação React importada usando o editor de código de sua preferência.

## Editando o arquivo `manifest.json`

Com o código da aplicação aberto no seu editor de código, vamos analisar o arquivo `manifest.json` responsável  por guardar as **informações básicas e essenciais**  do app, como:

- `vendor`  - Nome da conta VTEX responsável pelo desenvolvimento, pela manutenção e distribuição do app. 
- `name` - Nome do app. Deve ser um de sua escolha, mas atenção: evite o uso de caracteres especiais (com exceção do hífen `-`). 
- `version` - Versão atual do app. Para versionamento, o VTEX IO utiliza o [Semantic Versioning 2.0.0](https://semver.org/). 
- `title` - Nome de distribuição do app. Esse nome será usado para mostrá-lo na seção `Apps` do admin e também na VTEX App Store.
- `description` - Breve descrição da funcionalidade do app. 
- `builders` - Listagem dos [Builders](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-builders/) que facilitam o desenvolvimento do app, abstraindo configurações de serviços. 
- `dependencies` - Listagem de apps dos quais o app que você está desenvolvendo é dependente para funcionar corretamente. 

Neste primeiro momento, é fundamental que essas informações básicas do novo app sejam alteradas no arquivo `manifest.json` para que ele se torne devidamente seu e não mais uma versão exemplo disponibilizada pela VTEX. Para isso:

1. Substitua a conta indicada no campo `vendor` pela conta VTEX na qual você está desenvolvendo.
2. Substitua o valor indicado no campo `name` por outro de sua escolha. Lembre-se de que o nome definido nesse campo será o nome da sua nova aplicação.
3. Substitua o valor indicado no campo `title` e `description` por outros de sua escolha, de acordo com o app sendo desenvolvido por você.
4. Adicione o builder `store@0.x` na lista de builders para permitir a criação de novos blocos:

```diff
  "builders": {
+   "store": "0.x"
  }
```

5. Se você deseja importar algum componente React já desenvolvido previamente para o seu novo app, atualize a lista de `dependencies` com o nome do app responsável pelo componente desejado, por exemplo:

```diff
  "dependencies": {
+   "vtex.styleguide: 9.x"
}
```

Isso fará com que você consiga, posteriormente, importar o componente do app adicionado em `dependencies` para o seu código através da estrutura `import {componentName} from 'vtex.styleguide`, por exemplo. 
