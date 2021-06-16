# Postman

## Desenvolvimento»Tutorial de como utilizar o Postman para documentar uma API

### Como usar a plataforma Postman para a documentar uma API.
##### Daivid Silverio

Desenvolver um aplicativo muitas vezes exige algum tipo de integração com outro sistema já existente. Por exemplo, se você quiser que as pessoas comprem o seu serviço por meio do seu app, é preferível que você faça uma integração com uma plataforma de pagamento que está atuando no mercado (IUGU, Mercado Pago, etc). Essas integrações são muito úteis para que o desenvolvedor não precise criar determinada funcionalidade do zero (pagamentos, mapas, login com redes sociais, etc.), e sim, apenas integrar o aplicativo com um serviço já existente. Ou até mesmo se você quiser utilizar no seu app uma plataforma já usada pela sua empresa ou algum banco de dados que você possua. Essa integração é feita por meio do consumo de uma API. E isso também te ajuda a economizar seus recursos na hora da produção.

Nós já entendemos que essa API é necessária quando se trata das funcionalidades que precisam de uma integração com outro sistema. Mas, é necessário que você entenda também como funciona este trabalho na maioria das empresas de desenvolvimento.

Tem dois caminhos para desenvolver este material: você pode alocar a equipe da empresa para desenvolver isso ou fazer por conta própria. Porém, atente-se bem se você escolher a segunda opção, pois cada empresa de desenvolvimento possui algumas regras que devem ser seguidas quando se trata de produzir em conjunto. E o máximo de atenção a isso é essencial para você não perder tempo e dinheiro com algo que depois não poderá ser utilizado.

**Postman** é uma ferramenta que dá suporte a documentação das requisições feitas pela API. Ele possui ambiente para a documentação, execução e testes de APIs e requisições em geral. O objetivo deste texto é fornecer um tutorial introdutório para a criação de documentações vivas para a sua API por meio da plataforma Postman.

Saiba o que iremos aprender agora:

[Criar Coleções](## Como usar o Postman: Criar Coleções)
[Criar Pastas](## Como usar o Postman: Criar Pastas)
[Criar Requests](Como usar o Postman: Criar Requests)
[Adicionar Parâmetros](## Como usar o Postman: Adicionar Parâmetros)
[Adicionar Headers](## Como usar o Postman: Adicionar Headers)
[Criar e popular variáveis de ambiente/globais](## Como usar o Postman: Criar e popular variáveis de ambiente/globais)

## Como usar o Postman: Criar Coleções

Clique no ícone da pastinha para abrir um formulário para criar a coleção.

- Preencha com o nome desejado para a sua coleção e clique em “Create”. Pronto! Coleção criada! Agora vamos adicionar algumas requests e pastas na sua coleção.


## Como usar o Postman: Criar Pastas

Clique no ícone de reticências para abrir o submenu da Coleção. Clique em “Add Folder” para Adicionar uma nova pasta.

- Escreva o nome da pasta que você acabou de criar e clique em “Create” para salvar. Você pode usar essa funcionalidade para organizar melhor suas requests, de acordo com os recursos ou funcionalidade que sua API provê.

## Como usar o Postman: Criar Requests

- Para criar uma request, basta você digitar o endereço da API que você está documentando na barra de endereço e selecionar o método HTTP que será usado na request.

- Para salvar essa request na Coleção, clique em “Save”.

- Um formulário irá aparecer, onde você poderá preencher o nome da request e informar em qual Coleção e Pasta você deseja salvá-la. Finalmente, clique no botão “Save” laranja pra salvar a request.

## Como usar o Postman: Adicionar Parâmetros

- Por exemplo, vamos utilizar o POST para localhost:3000/users, que criamos na seção anterior.

- Para informar os parâmetros da request, selecione o formato desejado: form-data, x-www-form-urlencoded, raw (Text, JSON, XML etc), binary.

- Por exemplo, supondo os parâmetros de criação de um usuário:
...
name: Test
email: test@test.com
password: 123456
...

- Para testar, basta clicar no botão azul “Send”. O resultado da Request vem na parte de baixo onde está escrito “Response”

- Em form-data:

- Em JSON:

Você pode observar a resposta na aba “Body”, seguida pelos “Cookies” e “Headers” da mesma.

No exemplo, eu criei um header chamado “TOKEN”, para a demonstração.

## Como usar o Postman: Adicionar Headers

Adicionar headers é ainda mais simples do quê adicionar parâmetros. Basta selecionar a aba “Headers”, ao lado de “Body”, logo abaixo a barra de endereço:

Criei uma request adicional que exige um token de autenticação para fazer requests a recursos protegidos, como as informações do usuário, neste caso.

Caso a autenticação funcione, os dados do usuário são retornados. Podemos ver isto na imagem abaixo. 


Se acontecer o contrário, um erro é recebido, 401 (Unauthorized), que significa que não foi autenticado.


## Como usar o Postman: Criar e popular variáveis de ambiente/globais

Ficar escrevendo todos esses valores para parâmetros e headers pode acabar ficando um pouco tedioso dependendo da sua API. Principalmente, se ela possuir autenticação via tokens que podem mudar.

Para facilitar nossa vida um pouco, podemos fazer uso das variáveis de ambiente e da aba extra “Tests”, encontrada logo abaixo da barra de endereços.

Primeiramente, vamos criar um ambiente. Clique no ícone com uma engrenagem no canto superior direito e logo em seguida, Manage Environments.

Na janela que aparecer, clique no botão “Add”. Um campo para preencher o nome do novo ambiente irá aparecer. Preencha com o nome desejado e clique em “Add”.

A partir desse momento você também já pode adicionar as variáveis que eu havia comentado.

Vamos adicionar uma variável chamada “Last User Token”. Clique em “Add” ou “Update” (caso você voltar nessa tela e estiver adicionando novas variáveis).

Agora vamos voltar na request que havíamos criado na seção “Criar Requests”. Tendo a request selecionada, clique onde está escrito “No Environment” e selecione o nome do ambiente que você acabou de criar.

Em seguida, selecione a aba “Tests” para começar a facilitar a vida de quem for utilizar sua API.

Nessa aba você pode executar scripts javascript que serão executados após as requests. Assim, você poderá capturar os resultados contidos nos corpos e headers das suas respostas.

Como um exemplo bem simples, vamos capturar o e-mail do usuário contido no corpo da resposta e header TOKEN da mesma.

...
postman.setEnvironmentVariable(“Last User Email”, JSON.parse(responseBody).email); 
postman.setEnvironmentVariable(“Last User Token”, postman.getResponseHeader(“TOKEN”));
...

Agora podemos modificar o método que obtém informações do usuário para usar o header de autenticação. Para isso, utilize o Token salvo na variável de ambiente “Last User Token”

Selecione a request que precisa usar a variável de ambiente. Então, vá até o campo do Header, Parâmetros ou Corpo da Request e utilize a variável usando a notação {{Nome da Variável}} para recuperar o valor salvo.

No exemplo da autenticação, ficamos com: Authorization:Bearer {{Last User Token}}

Podemos usar esse mecanismo não apenas nos parâmetros, mas também nos parâmetros/corpos das requests.

Ex:

O postman também te possibilita salvar suas requests e coleções na nuvem. Ele também tem a capacidade de importar/exportar Coleções via um link único ou um arquivo .json. Basta clicar no ícone de reticências na coleção e escolher a opção “Export”.

Postman é uma ferramenta muito poderosa e fácil de ser utilizada. Pode ser usada como um meio de comunicação entre equipes de times/empresas diferentes quando houver necessidade de integração de APIs e com certeza tem o potencial de facilitar a vida de muita gente!

Mais exemplos e documentação oficial: https://www.getpostman.com/docs/ 

[Artigo original](https://jera.com.br/blog/5847/desenvolvimento/como-usar-o-postman)

[Aprenda+ no Postman](https://learning.postman.com/docs/getting-started/introduction/)