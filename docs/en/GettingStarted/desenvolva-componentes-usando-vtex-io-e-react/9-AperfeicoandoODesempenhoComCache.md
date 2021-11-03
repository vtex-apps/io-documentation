# Aperfeiçoando o desempenho com cache

Buscas repetida por dados semelhantes podem se tornar um investimento caro e frustrante, uma vez que pedem um número alto de respostas do servidor para a entrega das informações requisitadas.  

Por isso, a **habilidade de usar *cache* e reutilizar dados já previamente obtidos no servidor pode ser um ponto crítico para a otimização da performance da sua aplicação de front e, consequentemente, do seu website**. 

A plataforma de desenvolvimento VTEX IO já aplica técnicas avançadas de *cache* no [Store Framework](https://developers.vtex.com/vtex-developer-docs/docs/getting-started-3), usando o *cache* Apollo como solução de busca e gerenciamento de dados capaz de interagir com os serviços GraphQL da VTEX. 

É altamente recomendável que você use a [solução Apollo](https://www.apollographql.com/docs/react/caching/cache-configuration/) na sua aplicação e assim defina estratégias próprias de *cache* de acordo com o cenário de negócio da sua loja.  

![React Apollo overview](https://miro.medium.com/max/1400/1*Akd1I7jc0teE_mz15fnZog.jpeg)

Uma vez implementada, a solução opera sem grandes configurações: dois *requests* GraphQL com mesma *query* e variáveis atingem uma única vez o servidor para a coleta dos dados.

Você pode ler sobre as [normas e regras de uso do Apollo](https://medium.com/@galen.corey/understanding-apollo-fetch-policies-705b5ad71980) para entender mais a fundo sobre possíveis cenários de coleta de dados usando a solução. 

Usando a regra `cache-and-network`, por exemplo, você conseguirá retornar imediatamente os dados requisitados caso eles estejam *cacheados* e, ainda assim, consultar os servidor para confirmar se algum dado foi alterado desde então. 

