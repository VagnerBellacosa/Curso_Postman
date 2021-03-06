# Postman

## Testando servi�os Web API com Postman

### Aprenda neste artigo a testar servi�os Web API utilizando o Postman, aplica��o que permite enviar e receber dados via requisi��es HTTP.

##### Joel Rodrigues

Sistemas desenvolvidos com base em servi�os t�m se tornado cada vez mais comuns, principalmente pela flexibilidade que garantem aos clientes finais dos dados que podem ser quaisquer aplica��es capazes de consumir o servi�o, seja em ambiente web, desktop ou mobile. Atualmente a maior parte destes servi�os est� sendo constru�da sob o modelo REST, com a troca de mensagens sendo realizada atrav�s de requisi��es HTTP.

Neste tipo de cen�rio, os servi�os HTTP n�o possuem interface gr�fica com o usu�rio, atuando apenas no recebimento e provimento de dados atrav�s de requisi��es. Dessa forma, testar esse tipo de aplica��o envolve simular essas requisi��es a partir de um cliente conhecido, para que se tenha controle sobre os dados trafegados.

Desenvolver uma aplica��o cliente com interface gr�fica apenas para testar um servi�o seria um esfor�o adicional e que demandaria tempo e recursos que poderiam (e deveriam) ser utilizados no desenvolvimento do objeto principal: o servi�o.

Para suprir essa necessidade surge o Postman, uma aplica��o que permite realizar requisi��es HTTP a partir de uma interface simples e intuitiva, facilitando o teste e depura��o de servi�os REST.

O Postman est� dispon�vel como uma aplica��o para o browser Google Chrome e possui diversas funcionalidades �teis no desenvolvimento desse tipo de projeto. Aqui veremos como utiliz�-lo para testar as actions de um servi�o ASP.NET Web API, enviando e recebendo dados no formato JSON.

## Instalando o Postman

Por se tratar de um aplicativo para o Chrome, o Postman � instalado a partir da Chrome Web Store. Basta acessar o endere�o https://chrome.google.com/webstore/category/apps e na caixa de busca pesquise por Postman, como mostra a Figura 1.

Pesquisando pelo Postman na loja de extens�es do Chrome

- Pesquisando pelo Postman na loja de extens�es do Chrome

Ao serem retornados os resultados da busca, provavelmente o Postman aparecer� na primeira posi��o da lista. Clique ent�o no bot�o �Add to Chrome�, conforme mostra a Figura 2.

### Instalando o Postman

- Instalando o Postman

Na sequ�ncia voc� ser� informado sobre ao que esse aplicativo tem acesso e dever� confirmar a instala��o clicando em �Adicionar aplicativo�, como na Figura 3.

- Confirmando instala��o do Postman

Agora o aplicativo aparecer� como instalado no browser, como mostra a Figura 4.

- Extens�o instalada no browser

Clicando sobre ele voc� poder� ver todos os detalhes sobre o desenvolvimento, hist�rico de vers�es, tutorial de uso, opini�es de outros usu�rios e iniciar o bot�o clicando no bot�o �Launch App� no topo, como vemos na Figura 5.

## Detalhes sobre o aplicativo

Em sua vers�o 3 o Postman � iniciado como um aplicativo externo ao Chrome, diferente das vers�es anteriores em que era aberto em uma aba como extens�o. Se voc� desejar poder� criar uma conta e armazenar suas informa��es em um servidor do Postman, compartilhando assim seus testes e vari�veis entre v�rios dispositivos onde voc� fizer login. Aqui n�o utilizaremos essa funcionalidade, uma vez que desejamos apenas testar uma API local e explorar as principais funcionalidades, ent�o basta clicar em �Go to the app�, como ilustra a Figura 6.

## Iniciando o aplicativo>

Neste momento seremos direcionados ao ambiente principal do aplicativo onde temos, no lado esquerdo, o hist�rico de requisi��es feitas e no lado direito os campos e menus para se configurar e efetuar os requests HTTP.
 
- Ambiente principal do Postman

Agora que o Postman est� instalado e pronto para uso criaremos um projeto Web API para que possamos testar suas funcionalidades.

### Projeto Web API de exemplo

Aqui testaremos um servi�o do tipo ASP.NET Web API, mas o Postman pode ser usado para testar qualquer servi�o HTTP RESTful.

Crie ent�o um novo projeto do tipo Web API no Visual Studio e na pasta Models crie uma classe para modelar um objeto de dom�nio da aplica��o. Aqui trabalharemos com a classe �Livro�, cujo c�digo encontra-se na Listagem 1.

Listagem 1. Classe modelo da aplica��o de exemplo

...
public class Livro
{
    public int ID { get; set; }
    public string Titulo { get; set; }
    public string Autor { get; set; }
}
...

Na sequ�ncia criaremos uma classe que servir� de reposit�rio de dados simulados, contendo apenas alguns dados est�ticos que retornaremos e alteraremos a partir dos m�todos da API. Essa classe, que aqui chamaremos de �RepositorioSimulado�, pode ser vista na Listagem 2.
 
### Classe de reposit�rio de dados simulados

...
public class RepositorioSimulado
{
    private static List<Livro> livros;
  
    public static List<Livro> Livros
    {
        get
        {
            if (livros == null)
                GerarLivros();
            return livros;
        }
        set
        {
            livros = value;
        }
    }
  
    private static void GerarLivros()
    {
        livros = new List<Livro>();
  
        livros.Add(new Livro
        {
            ID = 1,
            Titulo = "Agile",
            Autor = "Andr� Faria Gomes"
        });
  
        livros.Add(new Livro
        {
            ID = 2,
            Titulo = "Building Microservices",
            Autor = "Sam Newman"
        });
  
        livros.Add(new Livro
        {
            ID = 3,
            Titulo = "Controlando vers�es com Git e Github",
            Autor = "Alexandre Aquiles; Rodrigo Ferreira"
        });
    }
}
...

O pr�ximo passo ser� criar um novo controller do tipo ApiController, que aqui ser� chamado de �LivrosController� e cujo c�digo pode ser visto na Listagem 3. Esse controller basicamente possui actions para os principais verbos do protocolo HTTP: GET, POST, PUT e DELETE. Sendo necess�rio, por�m, � poss�vel testar no Postman outros como HEAD e OPTIONS, por exemplo.

### Controller de exemplo da API

...
public class LivrosController : ApiController
{
    // GET: api/Livros
    public IEnumerable<Livro> Get()
    {
        return RepositorioSimulado.Livros;
    }
  
    // GET: api/Livros/5
    public IHttpActionResult Get(int id)
    {
        Livro livro = RepositorioSimulado.Livros.FirstOrDefault(l => l.ID == id);
  
        if (livro != null)
            return ResponseMessage(Request.CreateResponse<Livro>(HttpStatusCode.OK, livro));
        else
            return ResponseMessage(Request.CreateResponse<string>(HttpStatusCode.NotFound, "Livro n�o localizado."));
    }
  
    // POST: api/Livros
    public IHttpActionResult Post([FromBody]Livro objeto)
    {
        Livro livro = RepositorioSimulado.Livros.FirstOrDefault(l => l.ID == objeto.ID);
  
        if (livro != null)
            return ResponseMessage(Request.CreateResponse<string>(HttpStatusCode.Conflict, "J� existe um livro cadastrado com esse ID."));
        else
        {
            RepositorioSimulado.Livros.Add(objeto);
            return ResponseMessage(Request.CreateResponse(HttpStatusCode.OK));
        }                
    }
  
    // PUT: api/Livros/5
    public IHttpActionResult Put([FromBody]Livro objeto)
    {
        Livro livro = RepositorioSimulado.Livros.FirstOrDefault(l => l.ID == objeto.ID);
  
        if (livro != null)
        {
            livro.Autor = objeto.Autor;
            livro.Titulo = objeto.Titulo;
            return ResponseMessage(Request.CreateResponse(HttpStatusCode.OK));
        }
        else
            return ResponseMessage(Request.CreateResponse<string>(HttpStatusCode.NotFound, "Livro n�o localizado para altera��o."));
    }
  
    // DELETE: api/Livros/5
    public IHttpActionResult Delete(int id)
    {
        Livro livro = RepositorioSimulado.Livros.FirstOrDefault(l => l.ID == id);
  
        if (livro != null)
        {
            RepositorioSimulado.Livros.Remove(livro);
            return ResponseMessage(Request.CreateResponse(HttpStatusCode.OK));
        }
        else
            return ResponseMessage(Request.CreateResponse<string>(HttpStatusCode.NotFound, "Livro n�o localizado para exclus�o."));
    }
}
...

Este controller basicamente lista todos os livros ou apenas um pelo id atrav�s do m�todo GET, adiciona um livro via POST, altera um livro via PUT e exclui um livro via DELETE.

Podemos ent�o executar o projeto para test�-lo.

### Testando a API

Com o servi�o em execu��o testaremos os m�todos na ordem em que aparecem no controller. Assim, come�aremos pelo GET, que deve retornar todos os livros cadastrados. Para isso, no Postman adicione o endere�o em que o servi�o est� sendo executado, seguido de /api/livros, no campo �Enter request URL here� como ilustra a Figura 8.

#### Enviando GET pelo Postman

Observe que ao lado do endere�o deve estar selecionado o m�todo GET. Pressione o bot�o �Send� e observe o resultado, que � exibido na Figura 9.

#### Resultado do GET no Postman

Nessa figura podemos observar alguns pontos importantes sobre a requisi��o:

No lado esquerdo vemos o hist�rico de requisi��es realizadas. Caso seja necess�rio, � poss�vel clicar sobre uma delas e repeti-la;
Na parte inferior temos o resultado da requisi��o, que neste caso � a lista de livros cadastrados. Logo acima do resultado � poss�vel mudar a forma de visualiza��o, alterando o formato;
Podemos ver tamb�m o status da opera��o (que neste caso foi 200 � OK) e o tempo que demorou para se obter o resultado (22ms neste exemplo).
O pr�ximo m�todo a ser testado � o GET, em que passamos o ID de um livro no URL. Basta alterar o endere�o, adicionando /1 no final, por exemplo, e pressionar �Send� novamente. Assim teremos como resultado um �nico registro, como mostra a Figura 10.

- Resultado do GET filtrando por ID

Caso informemos um ID que n�o existe na lista (neste exemplo, qualquer n�mero diferente de 1, 2 ou 3), teremos como resultado a mensagem que foi retornada pelo servi�o e o status de retorno ser� 404 � Not Found, conforme definimos no controller, de acordo com a Figura 11.

- Retorno com status 404 � Not Found

Testaremos agora a action que responde a requisi��es utilizando o verbo POST, ou seja, aquela que cadastra um livro que deve ser informado como par�metro.

A URL para o qual enviaremos a requisi��o ser� a mesma em que fizemos o primeiro GET (<host>/api/livros), basta alterarmos o verbo para POST no lado esquerdo do campo em que inserimos o endere�o. Em seguida devemos ir � aba �Body� e marcar a op��o �raw�, uma vez que informaremos o conte�do da mensagem na forma de texto j� formatado como JSON. Logo em seguida devemos selecionar o formato �JSON (application/json)�, como mostra a Figura 12. Isso adicionar� um cabe�alho � requisi��o informando o tipo do conte�do que ser� enviado.

- Configurando a mensagem via POST

Ap�s inserir os dados do livro a ser enviado (em formato JSON), devemos clicar novamente em �Send� e observar o resultado, que se tudo correu bem, deve ser um status 200 � Ok exibido logo abaixo do campo onde inserimos o conte�do.

Se tentarmos inserir um livro com ID que j� esteja cadastrado receberemos como resultado um status 409 � Conflict e uma mensagem informando o problema, conforme mostra a Figura 13.

### Requisi��o via POST com retorno 409 � Conflict

Se fizermos agora um novo request GET teremos na lista o novo livro adicionado, como vemos na Figura 14.

- Lista atualizada com objeto adicionado

Para testar o m�todo Put do controller basta alterar o verbo do request para PUT (mantendo o endere�o base) e, de forma semelhante ao POST, informe o conte�do do objeto Livro a ser alterado no campo central. Se tudo correr bem, teremos como resultado um status 200 � Ok (Figura 15), caso contr�rio, se informarmos um ID inexistente, teremos um 404 � Not Found.

#### Mensagem enviada via PUT

Para verificar a altera��o, podemos fazer outra requisi��o GET e verificar a lista de todos os livros.

Por fim, para testar o m�todo DELETE, al�m de mudar o verbo ao lado do endere�o, devemos adicionar ao fim da URL o ID do livro a ser exclu�do, semelhante ao que fizemos no segundo GET. Conforme a Figura 16, observe que a URL ser� a mesma, por�m, como o verbo utilizado � outro, o servi�o Web API reconhecer� essa diferen�a e direcionar� a requisi��o a outra action (Delete, neste caso).

#### Requisi��o com verbo DELETE

Agora podemos fazer outra requisi��o via GET para o endere�o base e veremos que a lista foi atualizada, como mostra a Figura 17.

- Lista atualizada ap�s opera��es

Al�m das funcionalidades que exploramos aqui, o Postman permite ainda trabalhar em times, customizar ambientes de teste, importar arquivos com requisi��es pr�-definidas, entre outras.

Quando se est� desenvolvendo um servi�o que ser� exposto para clientes externos, � fundamental que os mais diversos testes sejam realizados a fim de validar o funcionamento da aplica��o diante das diversas situa��es poss�veis. Com o Postman essa tarefa � simplificada, pois podemos facilmente enviar requests HTTP para servi�os RESTful, enviando par�metros e recebendo as devidas respostas, al�m de analisar o tempo gasto em cada requisi��o, o que tamb�m pode auxiliar na localiza��o de problemas de desempenho.

A ferramenta possui ampla documenta��o, que pode ser encontrada no link no final do artigo, al�m de uma vers�o paga que conta com alguns recursos adicionais, como o trabalho em nuvem.

Links

P�gina oficial do Postman
http::/getpostman.com

Chrome Web Store
https://chrome.google.com/webstore/category/apps

ASP.NET Web API
http://www.asp.net/web-api


Read more: http://www.linhadecodigo.com.br/artigo/3712/testando-servicos-web-api-com-postman.aspx#ixzz6xyDqwnBj

[Artigo original](http://www.linhadecodigo.com.br/artigo/3712/testando-servicos-web-api-com-postman.aspx) 