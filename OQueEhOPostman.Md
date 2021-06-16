# Postman

## O que é o Postman?

Acompanhe o nosso guia e conheça um pouco mais a respeito da ferramenta “Postman”, bem como sua utilidade e as melhores práticas para começar a dominar o aplicativo!

Descubra como analisar e testar APIs RESTs na prática, ou seja, executar requisições em qualquer API, seja sua ou de terceiros!

Se você procura por uma ferramenta que ofereça uma interface de usuário prática e que permita realizar solicitações HTTP sem a necessidade de escrever um monte de códigos e testar a funcionalidade de uma API, então você precisa conhecer o Postman!

Neste post, você terá acesso a um tutorial introdutório desse aplicativo, com o qual você poderá realizar, por exemplo, uma requisição em uma API. E, dentro das demais funcionalidades da ferramenta, vamos mostrar:**

### Por que usar o Postman;

[ - O que é o Postman?](## O que é Postman?)
[ - Como funciona a interface do Postman](## Como funciona o Postman?)
[ - Como fazer requisições GET](## Como fazer uma requisição GET?)
[ - Como fazer requisições POST e qual a diferença entre elas](## Como fazer uma requisição POST e qual a diferença para um requisição GET?)
[ - Como Adicionar Parâmetros e popular variáveis de ambiente/globais](## Como criar parâmetros de dados?)
[ - Como fazer testes](## Como criar Postman Tests?)

## O que é Postman?

O Postman é uma ferramenta que dá suporte à documentação das requisições feitas pela API. Ele possui ambiente para a documentação, execução de testes de APIs e requisições em geral.

Ao utilizá-lo, você passará a trabalhar com APIs de modo mais eficiente, construindo solicitações rapidamente e, ainda, poderá guardá-las para uso posterior, além de conseguir analisar as respostas enviadas pela API.

Um bom motivo para usar essa ferramenta é que, por meio dela, é possível reduzir drasticamente o tempo necessário para testar e desenvolver APIs.

Em um exemplo prático, imagine que você queira fazer uma solicitação GET para procurar certas informações no nome da empresa.

Se fosse o caso de testar uma solicitação GET sem usar o Postman, você precisaria escrever todo um código para executar a requisição, além de uma interface visual para interagir com essa rotina.

Se fosse concedido, provavelmente você precisaria escrever tudo isso para criar um aplicativo funcional usando essa API, mas todo esse trabalho seria simplesmente para testar a sua funcionalidade, o que de fato, nesse formato, é tedioso e demorado.

Já com o Postman, esse teste é muito mais otimizado. Tudo o que precisa ser feito é:**

- Obter a conexão da rota à barra de endereços;
- Selecionar o método de resposta GET na caixa suspensa à esquerda;
- Digitar a chave da API na seção "Headers";
- Especificar o formato da resposta, que poderia ser em JSON, por exemplo, e;
- Clicar em enviar.

Em seguida, será obtido os dados de resposta em JSON (simples e fácil de ler) acompanhado do código de status 200, que confirma que a solicitação GET foi bem-sucedida. Bem mais tranquilo, não?

### Por que usar o Postman?

Além de ser um aplicativo gratuito e fácil de aprender, com pouco tempo você já estará enviando seus primeiros requests (solicitações/requisições). No mais, trata-se de uma ferramenta com um amplo suporte para todas as APIs e Schemas.

Entre as principais vantagens em se usar o Postman, podemos destacar:**

- Possibilita qualquer tipo de chamada de API —  REST, SOAP ou HTTP;
- Oferece suporte para formatos de dados populares, como OpenAPI GraphQL e RAML;
- **Fácil acessibilidade:** Para usar o Postman, basta fazer login em sua conta, facilitando o acesso a arquivos a qualquer momento, em qualquer lugar, desde que um aplicativo Postman esteja instalado no computador;
- **Uso de Coleções:** O Postman permite que os usuários criem coleções para suas chamadas de API. Cada coleção pode criar subpastas e várias solicitações. Isso ajuda a organizar suas suítes de teste;
- **Colaboração (Collaboration):** Coleções e ambientes podem ser importados ou exportados, facilitando o compartilhamento de arquivos. Um link direto também pode ser usado para compartilhar coleções;
- **Criar ambientes:** Ter vários ambientes ajuda a ter menos repetições de testes, pois é possível usar a mesma coleção, mas em um ambiente diferente;
- **Elaborar testes:** Pontos de verificação de teste, como a verificação do status de resposta HTTP bem-sucedido, podem ser adicionados a cada chamada de API, o que ajuda a garantir a cobertura do teste;
- **Teste de automação:** Com o uso do Collection Runner ou Newman, os testes podem ser executados em várias iterações, economizando tempo para testes repetitivos;
- **Depuração:** O console do Postman ajuda a verificar quais dados foram recuperados, facilitando a depuração de testes;
- **Integração Contínua:** A partir da sua capacidade de oferecer suporte à integração contínua, são mantidas práticas de desenvolvimento.

### Como funciona o Postman?

Já na página principal do aplicativos, temos muitas informações e, para esclarecer o modus operandi da  ferramenta, precisaremos dar uma passada rápida nas opções disponíveis na interface. Veja:**

- **New:** É aqui que você criará uma nova solicitação, coleção ou ambiente.
- **Import:** É usado para importar uma coleção ou ambiente. Existem opções como importar arquivo, pasta, vincular ou colar texto não processado.
- **Runner:** Os testes de automação podem ser executados através do Collection Runner. Isso será discutido mais adiante.
- **Open New:** Permite abrir uma nova guia, Postman Window ou Runner Window.
- **My Workspace:**  Você pode criar um novo espaço de trabalho individualmente ou em equipe.
- **Invite:** Permite convidar membros da equipe.
- **History:** As solicitações anteriores que você enviou serão exibidas no Histórico. Isso facilita o rastreamento das ações realizadas.
- **Collections:** Permite criar coleções. Cada coleção pode ter subpastas e várias solicitações. Uma solicitação ou pasta também pode ser duplicada.
- **Request tab:** Exibe o título da solicitação em que você está trabalhando.
- **HTTP Request:** Clicar nesse botão exibirá uma lista suspensa de solicitações diferentes, como GET, POST, COPY, DELETE etc. Nos testes, as solicitações mais usadas são GET e POST.
- **Request URL:** Também conhecido como “endpoint”, é aqui que você identificará o link para o qual a API se comunicará.
- **Save:** Serve para salvar novas alterações.
- **Params:** É aqui que você escreverá os parâmetros necessários para uma solicitação, como valores-chave.
- **Authorization:** Para acessar APIs, é necessária uma autorização adequada. Pode ser na forma de nome de usuário e senha, token de portador, entre outros.
- **Headers:** - Você poderá definir cabeçalhos, como o tipo de conteúdo JSON, por exemplo.
- **Body:** - Este botão possibilita personalizar detalhes em uma solicitação comumente usada na solicitação POST.
- **Pre-request Script:** São scripts que serão executados antes da solicitação. Geralmente, os scripts de pré-solicitação para o ambiente de configuração são usados ​​para garantir que os testes sejam executados no ambiente correto.
- **Tests:** São scripts executados durante a solicitação. É importante ter testes, pois configura pontos de verificação para analisar se o status da resposta está de acordo, ou se os dados recuperados estão conforme o esperado, por exemplo.

Agora que já temos uma boa visualização da interface da ferramenta, vamos passar para parte prática de como o postman funciona. Acompanhe!

## Como fazer uma requisição GET?

As requisições GET são usadas para recuperar informações da URL fornecida e não realizam alterações feitas nos endpoints.

Para realizar uma requisição GET é muito simples. Na área de trabalho do aplicativo, faça o seguinte:**

1 - Defina sua solicitação HTTP como GET.

2 - No campo URL da solicitação, coloque o link de entrada.

3 - Clique em Enviar.

4 - Você verá na aba “Status” a mensagem “200 OK”.

### OBSERVAÇÃO

Pode haver casos em que a requisição GET não tenha êxito. Isto pode acontecer devido a uma URL de solicitação ser inválida ou porque a autenticação é necessária.

## Como fazer uma requisição POST e qual a diferença para um requisição GET?

Pode-se dizer que a grande diferença entre um GET e um POST é que, no caso de um POST, existe a manipulação de dados, com o usuário adicionando informações ao endpoint. 

Para demonstrar isso na prática — usando os mesmos dados do exemplo anterior —, agora vamos adicionar nosso próprio usuário.

Para efetuar um Post Request você deverá seguir os 5 seguintes passos:

1 - Clique em uma nova guia para criar uma nova solicitação.

2 - Na nova guia, siga os seguintes caminhos:**

	1º. Defina sua solicitação HTTP para POST.

	2º. Insira o mesmo link no URL da solicitação

	3º. Selecione a aba “Body”

3 - Agora, na aba “Body”, clique em “raw” e selecione JSON.

4 - Copie e cole apenas o resultado de um usuário do GET, como segue exemplo abaixo. 

	A partir daí, verifique se o código foi copiado corretamente com chaves e colchetes emparelhados. E então, altere os campos “id” para 11 e o “name” para qualquer nome desejado. 

	Observação: Você também pode alterar outros detalhes, como o endereço, por exemplo.

	### ATENÇÃO
	O Post Request deve ter o formato correto para garantir que os dados solicitados serão criados. É uma boa prática usar o GET primeiro para verificar o formato JSON da solicitação.

5 - Por fim, clique em Enviar (Send). 

## Como criar parâmetros de dados?

A parametrização de dados é um dos recursos mais úteis do Postman. Em vez de criar as mesmas solicitações com dados diferentes, você pode usar variáveis ​​com parâmetros. 

Essas informações podem ser de um arquivo de dados ou de uma variável de ambiente. Vale lembrar que a parametrização ajuda a evitar a repetição dos mesmos testes e iterações podem ser usadas para testes de automação.

Esses parâmetros são criados por meio do uso de colchetes duplos: {{sample}}. Vamos dar uma olhada em um exemplo de uso de parâmetros:

Agora, vamos criar um parâmetro GET em 4 passos, acompanhe!

1° Passo:
	- Defina sua solicitação HTTP como GET.
	- Insira o link da URL. Substitua a primeira parte do link por um parâmetro como {{url}}. A URL de solicitação agora deve ser “{{url}}/users”.
	- Clique em enviar (Send).
	- Você deverá receber uma mensagem dizendo que não houve resposta (“could not get any response”), isso pois ainda não definimos a fonte do nosso parâmetro.

2º Passo:
	Para usar o parâmetro, você precisa definir o ambiente e, para isso, faça o seguinte:
	- Clique no ícone com o desenho de um “olho”, localizado no canto superior direito.
	- Clique em “edit” para definir a variável para um ambiente global que pode ser usado em todas as coleções.

3º Passo:
	Na aba “Variable”, realize as seguintes operações:
	- Defina o nome para o URL desejado.
	- Clique em  “Save” (Salvar).

	Atenção! Se após isso surgir uma janela, como demonstrado abaixo, basta fechá-la, sem problemas.

4º Passo:
	Volte para ao seu GET e clique em enviar (Send). A partir de agora já deve haver resultados para sua solicitação.
	Observação: As imagens utilizadas neste tópico foram aproveitadas do blog Guru99.

	#### ATENÇÃO
	Uma boa prática nesse quesito é sempre verificar se seus parâmetros possuem uma fonte, como uma variável de ambiente ou arquivo de dados, para evitar erros.

## Como criar Postman Tests?

Os Postman Tests são códigos JavaScript adicionados às solicitações, que ajudam a verificar resultados como status bem-sucedido ou com falha, além de poder fazer a comparação de resultados esperados, entre outras funcionalidades.

De regra, você verá que esse comando começará com “pm.test”. Para que você possa compreender melhor, abaixo, vamos criar alguns testes básicos para as solicitações parametrizadas do tópico anterior.

Etapa 1)

	- Acesse seu GET de usuário.

	- Alterne para a guia “Tests”. No lado direito, aparecerá uma seção de códigos snippets.

	- Nesta seção, clique em "Status Code: code is 200".

	- O painel será preenchido automaticamente.

Etapa 2) Agora clique em Enviar (Send). O resultado do teste deve ser exibido.

Etapa 3) Volte para a guia “Tests” e vamos adicionar outro teste. Desta vez, será comparado o resultado esperado com o resultado real.

	Na seção de snippets, clique em "Response body:JSON value check". Verificaremos aqui se “Rafael” possui o ID do usuário 1.

Etapa 4) 
	​- Substitua "Your Test Name" do código por "Check if user with id1 is Rafael" para que o nome do teste especifique exatamente o que queremos testar.
	- Substitua jsonData.value por jsonData [0].name. Para obter o caminho, verifique também o “Body” no GET anterior. 
	- Se você deseja obter um segundo resultado, use jsonData [1] e assim por diante para obter resultados futuros.
	- No eql, insira "Rafael".

Etapa 5)
	Clique em enviar (Send). A partir de agora deve haver dois resultados de teste aprovados para sua solicitação.

	Observação: Existem diferentes tipos de testes que podem ser criados no Postman. Tente explorar a ferramenta e veja quais testes atenderão às suas necessidades.


[Artigo original](https://enotas.com.br/blog/postman/#indice-0)