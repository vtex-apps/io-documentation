# Estruturando a documentação

Agora que você criou um componente e definiu o seu estilo, está na hora de gerar a documentação da nova aplicação!

A documentaçao de um app é uma das partes mais críticas do desenvolvimento de um projeto, pois é ela a responsável por apresentar todas as funcionalidades para os futuros usuários.

Pensando nisso, o time do VTEX IO disponibiliza um ***template* de documentação** responsável por te auxiliar neste processo:

1. Acesse a pasta `docs` do seu app.
2. Acesse o arquivo `README.md`.

No arquivo `README.md`, você encontrará uma estrutura de recomendações a serem seguidas na produção da sua documentação. Leia com atenção o arquivo e faça as alterações de acordo com o seu cenário real. 

Além de apresentar os blocos de tema exportados pela sua aplicação, você também deve descrever as suas propriedades e listar os CSS Handles criados no passo anterior, como indicado no *template*. 

Lembre-se de que **documentação é um processo contínuo**: sempre que alguma nova configuração atingir a experiência do usuário da sua aplicação, o arquivo `README.md` deverá ser atualizado.

<div class="alert alert-info">
As propriedades de um bloco são as mesmas do componente React que ele renderiza. Isso significa que, ao importar um componente React e vinculá-lo a um bloco de tema sendo desenvolvido, este último automaticamente herda as propriedades do primeiro. Por isso, não se esqueça de acessar a documentação do componente em questão e documentar as propriedades disponíveis para o bloco no <code>README.md</code> sua app, esclarecendo o que cada uma configura e o seu valor padrão.
</div>


