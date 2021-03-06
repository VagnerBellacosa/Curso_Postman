# Postman

## Desenvolvimento�Tutorial de como utilizar o Postman para documentar uma API

### Como usar a plataforma Postman para a documentar uma API.
##### Daivid Silverio

Desenvolver um aplicativo muitas vezes exige algum tipo de integra��o com outro sistema j� existente. Por exemplo, se voc� quiser que as pessoas comprem o seu servi�o por meio do seu app, � prefer�vel que voc� fa�a uma integra��o com uma plataforma de pagamento que est� atuando no mercado (IUGU, Mercado Pago, etc). Essas integra��es s�o muito �teis para que o desenvolvedor n�o precise criar determinada funcionalidade do zero (pagamentos, mapas, login com redes sociais, etc.), e sim, apenas integrar o aplicativo com um servi�o j� existente. Ou at� mesmo se voc� quiser utilizar no seu app uma plataforma j� usada pela sua empresa ou algum banco de dados que voc� possua. Essa integra��o � feita por meio do consumo de uma API. E isso tamb�m te ajuda a economizar seus recursos na hora da produ��o.

N�s j� entendemos que essa API � necess�ria quando se trata das funcionalidades que precisam de uma integra��o com outro sistema. Mas, � necess�rio que voc� entenda tamb�m como funciona este trabalho na maioria das empresas de desenvolvimento.

Tem dois caminhos para desenvolver este material: voc� pode alocar a equipe da empresa para desenvolver isso ou fazer por conta pr�pria. Por�m, atente-se bem se voc� escolher a segunda op��o, pois cada empresa de desenvolvimento possui algumas regras que devem ser seguidas quando se trata de produzir em conjunto. E o m�ximo de aten��o a isso � essencial para voc� n�o perder tempo e dinheiro com algo que depois n�o poder� ser utilizado.

**Postman** � uma ferramenta que d� suporte a documenta��o das requisi��es feitas pela API. Ele possui ambiente para a documenta��o, execu��o e testes de APIs e requisi��es em geral. O objetivo deste texto � fornecer um tutorial introdut�rio para a cria��o de documenta��es vivas para a sua API por meio da plataforma Postman.

Saiba o que iremos aprender agora:

[Criar Cole��es](## Como usar o Postman: Criar Cole��es)
[Criar Pastas](## Como usar o Postman: Criar Pastas)
[Criar Requests](Como usar o Postman: Criar Requests)
[Adicionar Par�metros](## Como usar o Postman: Adicionar Par�metros)
[Adicionar Headers](## Como usar o Postman: Adicionar Headers)
[Criar e popular vari�veis de ambiente/globais](## Como usar o Postman: Criar e popular vari�veis de ambiente/globais)

## Como usar o Postman: Criar Cole��es

Clique no �cone da pastinha para abrir um formul�rio para criar a cole��o.

- Preencha com o nome desejado para a sua cole��o e clique em �Create�. Pronto! Cole��o criada! Agora vamos adicionar algumas requests e pastas na sua cole��o.


## Como usar o Postman: Criar Pastas

Clique no �cone de retic�ncias para abrir o submenu da Cole��o. Clique em �Add Folder� para Adicionar uma nova pasta.

- Escreva o nome da pasta que voc� acabou de criar e clique em �Create� para salvar. Voc� pode usar essa funcionalidade para organizar melhor suas requests, de acordo com os recursos ou funcionalidade que sua API prov�.

## Como usar o Postman: Criar Requests

- Para criar uma request, basta voc� digitar o endere�o da API que voc� est� documentando na barra de endere�o e selecionar o m�todo HTTP que ser� usado na request.

- Para salvar essa request na Cole��o, clique em �Save�.

- Um formul�rio ir� aparecer, onde voc� poder� preencher o nome da request e informar em qual Cole��o e Pasta voc� deseja salv�-la. Finalmente, clique no bot�o �Save� laranja pra salvar a request.

## Como usar o Postman: Adicionar Par�metros

- Por exemplo, vamos utilizar o POST para localhost:3000/users, que criamos na se��o anterior.

- Para informar os par�metros da request, selecione o formato desejado: form-data, x-www-form-urlencoded, raw (Text, JSON, XML etc), binary.

- Por exemplo, supondo os par�metros de cria��o de um usu�rio:
...
name: Test
email: test@test.com
password: 123456
...

- Para testar, basta clicar no bot�o azul �Send�. O resultado da Request vem na parte de baixo onde est� escrito �Response�

- Em form-data:

- Em JSON:

Voc� pode observar a resposta na aba �Body�, seguida pelos �Cookies� e �Headers� da mesma.

No exemplo, eu criei um header chamado �TOKEN�, para a demonstra��o.

## Como usar o Postman: Adicionar Headers

Adicionar headers � ainda mais simples do qu� adicionar par�metros. Basta selecionar a aba �Headers�, ao lado de �Body�, logo abaixo a barra de endere�o:

Criei uma request adicional que exige um token de autentica��o para fazer requests a recursos protegidos, como as informa��es do usu�rio, neste caso.

Caso a autentica��o funcione, os dados do usu�rio s�o retornados. Podemos ver isto na imagem abaixo. 


Se acontecer o contr�rio, um erro � recebido, 401 (Unauthorized), que significa que n�o foi autenticado.


## Como usar o Postman: Criar e popular vari�veis de ambiente/globais

Ficar escrevendo todos esses valores para par�metros e headers pode acabar ficando um pouco tedioso dependendo da sua API. Principalmente, se ela possuir autentica��o via tokens que podem mudar.

Para facilitar nossa vida um pouco, podemos fazer uso das vari�veis de ambiente e da aba extra �Tests�, encontrada logo abaixo da barra de endere�os.

Primeiramente, vamos criar um ambiente. Clique no �cone com uma engrenagem no canto superior direito e logo em seguida, Manage Environments.

Na janela que aparecer, clique no bot�o �Add�. Um campo para preencher o nome do novo ambiente ir� aparecer. Preencha com o nome desejado e clique em �Add�.

A partir desse momento voc� tamb�m j� pode adicionar as vari�veis que eu havia comentado.

Vamos adicionar uma vari�vel chamada �Last User Token�. Clique em �Add� ou �Update� (caso voc� voltar nessa tela e estiver adicionando novas vari�veis).

Agora vamos voltar na request que hav�amos criado na se��o �Criar Requests�. Tendo a request selecionada, clique onde est� escrito �No Environment� e selecione o nome do ambiente que voc� acabou de criar.

Em seguida, selecione a aba �Tests� para come�ar a facilitar a vida de quem for utilizar sua API.

Nessa aba voc� pode executar scripts javascript que ser�o executados ap�s as requests. Assim, voc� poder� capturar os resultados contidos nos corpos e headers das suas respostas.

Como um exemplo bem simples, vamos capturar o e-mail do usu�rio contido no corpo da resposta e header TOKEN da mesma.

...
postman.setEnvironmentVariable(�Last User Email�, JSON.parse(responseBody).email); 
postman.setEnvironmentVariable(�Last User Token�, postman.getResponseHeader(�TOKEN�));
...

Agora podemos modificar o m�todo que obt�m informa��es do usu�rio para usar o header de autentica��o. Para isso, utilize o Token salvo na vari�vel de ambiente �Last User Token�

Selecione a request que precisa usar a vari�vel de ambiente. Ent�o, v� at� o campo do Header, Par�metros ou Corpo da Request e utilize a vari�vel usando a nota��o {{Nome da Vari�vel}} para recuperar o valor salvo.

No exemplo da autentica��o, ficamos com: Authorization:Bearer {{Last User Token}}

Podemos usar esse mecanismo n�o apenas nos par�metros, mas tamb�m nos par�metros/corpos das requests.

Ex:

O postman tamb�m te possibilita salvar suas requests e cole��es na nuvem. Ele tamb�m tem a capacidade de importar/exportar Cole��es via um link �nico ou um arquivo .json. Basta clicar no �cone de retic�ncias na cole��o e escolher a op��o �Export�.

Postman � uma ferramenta muito poderosa e f�cil de ser utilizada. Pode ser usada como um meio de comunica��o entre equipes de times/empresas diferentes quando houver necessidade de integra��o de APIs e com certeza tem o potencial de facilitar a vida de muita gente!

Mais exemplos e documenta��o oficial: https://www.getpostman.com/docs/ 

[Artigo original](https://jera.com.br/blog/5847/desenvolvimento/como-usar-o-postman)

[Aprenda+ no Postman](https://learning.postman.com/docs/getting-started/introduction/)