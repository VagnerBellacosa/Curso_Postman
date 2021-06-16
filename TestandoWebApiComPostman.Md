# Postman

## Testando serviços Web API com Postman

### Aprenda neste artigo a testar serviços Web API utilizando o Postman, aplicação que permite enviar e receber dados via requisições HTTP.

##### Joel Rodrigues

Sistemas desenvolvidos com base em serviços têm se tornado cada vez mais comuns, principalmente pela flexibilidade que garantem aos clientes finais dos dados que podem ser quaisquer aplicações capazes de consumir o serviço, seja em ambiente web, desktop ou mobile. Atualmente a maior parte destes serviços está sendo construída sob o modelo REST, com a troca de mensagens sendo realizada através de requisições HTTP.

Neste tipo de cenário, os serviços HTTP não possuem interface gráfica com o usuário, atuando apenas no recebimento e provimento de dados através de requisições. Dessa forma, testar esse tipo de aplicação envolve simular essas requisições a partir de um cliente conhecido, para que se tenha controle sobre os dados trafegados.

Desenvolver uma aplicação cliente com interface gráfica apenas para testar um serviço seria um esforço adicional e que demandaria tempo e recursos que poderiam (e deveriam) ser utilizados no desenvolvimento do objeto principal: o serviço.

Para suprir essa necessidade surge o Postman, uma aplicação que permite realizar requisições HTTP a partir de uma interface simples e intuitiva, facilitando o teste e depuração de serviços REST.

O Postman está disponível como uma aplicação para o browser Google Chrome e possui diversas funcionalidades úteis no desenvolvimento desse tipo de projeto. Aqui veremos como utilizá-lo para testar as actions de um serviço ASP.NET Web API, enviando e recebendo dados no formato JSON.

## Instalando o Postman

Por se tratar de um aplicativo para o Chrome, o Postman é instalado a partir da Chrome Web Store. Basta acessar o endereço https://chrome.google.com/webstore/category/apps e na caixa de busca pesquise por Postman, como mostra a Figura 1.

Pesquisando pelo Postman na loja de extensões do Chrome

- Pesquisando pelo Postman na loja de extensões do Chrome

Ao serem retornados os resultados da busca, provavelmente o Postman aparecerá na primeira posição da lista. Clique então no botão “Add to Chrome”, conforme mostra a Figura 2.

### Instalando o Postman

- Instalando o Postman

Na sequência você será informado sobre ao que esse aplicativo tem acesso e deverá confirmar a instalação clicando em “Adicionar aplicativo”, como na Figura 3.

- Confirmando instalação do Postman

Agora o aplicativo aparecerá como instalado no browser, como mostra a Figura 4.

- Extensão instalada no browser

Clicando sobre ele você poderá ver todos os detalhes sobre o desenvolvimento, histórico de versões, tutorial de uso, opiniões de outros usuários e iniciar o botão clicando no botão “Launch App” no topo, como vemos na Figura 5.

## Detalhes sobre o aplicativo

Em sua versão 3 o Postman é iniciado como um aplicativo externo ao Chrome, diferente das versões anteriores em que era aberto em uma aba como extensão. Se você desejar poderá criar uma conta e armazenar suas informações em um servidor do Postman, compartilhando assim seus testes e variáveis entre vários dispositivos onde você fizer login. Aqui não utilizaremos essa funcionalidade, uma vez que desejamos apenas testar uma API local e explorar as principais funcionalidades, então basta clicar em “Go to the app”, como ilustra a Figura 6.

## Iniciando o aplicativo>

Neste momento seremos direcionados ao ambiente principal do aplicativo onde temos, no lado esquerdo, o histórico de requisições feitas e no lado direito os campos e menus para se configurar e efetuar os requests HTTP.
 
- Ambiente principal do Postman

Agora que o Postman está instalado e pronto para uso criaremos um projeto Web API para que possamos testar suas funcionalidades.

### Projeto Web API de exemplo

Aqui testaremos um serviço do tipo ASP.NET Web API, mas o Postman pode ser usado para testar qualquer serviço HTTP RESTful.

Crie então um novo projeto do tipo Web API no Visual Studio e na pasta Models crie uma classe para modelar um objeto de domínio da aplicação. Aqui trabalharemos com a classe “Livro”, cujo código encontra-se na Listagem 1.

Listagem 1. Classe modelo da aplicação de exemplo

...
public class Livro
{
    public int ID { get; set; }
    public string Titulo { get; set; }
    public string Autor { get; set; }
}
...

Na sequência criaremos uma classe que servirá de repositório de dados simulados, contendo apenas alguns dados estáticos que retornaremos e alteraremos a partir dos métodos da API. Essa classe, que aqui chamaremos de “RepositorioSimulado”, pode ser vista na Listagem 2.
 
### Classe de repositório de dados simulados

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
            Autor = "André Faria Gomes"
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
            Titulo = "Controlando versões com Git e Github",
            Autor = "Alexandre Aquiles; Rodrigo Ferreira"
        });
    }
}
...

O próximo passo será criar um novo controller do tipo ApiController, que aqui será chamado de “LivrosController” e cujo código pode ser visto na Listagem 3. Esse controller basicamente possui actions para os principais verbos do protocolo HTTP: GET, POST, PUT e DELETE. Sendo necessário, porém, é possível testar no Postman outros como HEAD e OPTIONS, por exemplo.

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
            return ResponseMessage(Request.CreateResponse<string>(HttpStatusCode.NotFound, "Livro não localizado."));
    }
  
    // POST: api/Livros
    public IHttpActionResult Post([FromBody]Livro objeto)
    {
        Livro livro = RepositorioSimulado.Livros.FirstOrDefault(l => l.ID == objeto.ID);
  
        if (livro != null)
            return ResponseMessage(Request.CreateResponse<string>(HttpStatusCode.Conflict, "Já existe um livro cadastrado com esse ID."));
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
            return ResponseMessage(Request.CreateResponse<string>(HttpStatusCode.NotFound, "Livro não localizado para alteração."));
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
            return ResponseMessage(Request.CreateResponse<string>(HttpStatusCode.NotFound, "Livro não localizado para exclusão."));
    }
}
...

Este controller basicamente lista todos os livros ou apenas um pelo id através do método GET, adiciona um livro via POST, altera um livro via PUT e exclui um livro via DELETE.

Podemos então executar o projeto para testá-lo.

### Testando a API

Com o serviço em execução testaremos os métodos na ordem em que aparecem no controller. Assim, começaremos pelo GET, que deve retornar todos os livros cadastrados. Para isso, no Postman adicione o endereço em que o serviço está sendo executado, seguido de /api/livros, no campo “Enter request URL here” como ilustra a Figura 8.

#### Enviando GET pelo Postman

Observe que ao lado do endereço deve estar selecionado o método GET. Pressione o botão “Send” e observe o resultado, que é exibido na Figura 9.

#### Resultado do GET no Postman

Nessa figura podemos observar alguns pontos importantes sobre a requisição:

No lado esquerdo vemos o histórico de requisições realizadas. Caso seja necessário, é possível clicar sobre uma delas e repeti-la;
Na parte inferior temos o resultado da requisição, que neste caso é a lista de livros cadastrados. Logo acima do resultado é possível mudar a forma de visualização, alterando o formato;
Podemos ver também o status da operação (que neste caso foi 200 – OK) e o tempo que demorou para se obter o resultado (22ms neste exemplo).
O próximo método a ser testado é o GET, em que passamos o ID de um livro no URL. Basta alterar o endereço, adicionando /1 no final, por exemplo, e pressionar “Send” novamente. Assim teremos como resultado um único registro, como mostra a Figura 10.

- Resultado do GET filtrando por ID

Caso informemos um ID que não existe na lista (neste exemplo, qualquer número diferente de 1, 2 ou 3), teremos como resultado a mensagem que foi retornada pelo serviço e o status de retorno será 404 – Not Found, conforme definimos no controller, de acordo com a Figura 11.

- Retorno com status 404 – Not Found

Testaremos agora a action que responde a requisições utilizando o verbo POST, ou seja, aquela que cadastra um livro que deve ser informado como parâmetro.

A URL para o qual enviaremos a requisição será a mesma em que fizemos o primeiro GET (<host>/api/livros), basta alterarmos o verbo para POST no lado esquerdo do campo em que inserimos o endereço. Em seguida devemos ir à aba “Body” e marcar a opção “raw”, uma vez que informaremos o conteúdo da mensagem na forma de texto já formatado como JSON. Logo em seguida devemos selecionar o formato “JSON (application/json)”, como mostra a Figura 12. Isso adicionará um cabeçalho à requisição informando o tipo do conteúdo que será enviado.

- Configurando a mensagem via POST

Após inserir os dados do livro a ser enviado (em formato JSON), devemos clicar novamente em “Send” e observar o resultado, que se tudo correu bem, deve ser um status 200 – Ok exibido logo abaixo do campo onde inserimos o conteúdo.

Se tentarmos inserir um livro com ID que já esteja cadastrado receberemos como resultado um status 409 – Conflict e uma mensagem informando o problema, conforme mostra a Figura 13.

### Requisição via POST com retorno 409 – Conflict

Se fizermos agora um novo request GET teremos na lista o novo livro adicionado, como vemos na Figura 14.

- Lista atualizada com objeto adicionado

Para testar o método Put do controller basta alterar o verbo do request para PUT (mantendo o endereço base) e, de forma semelhante ao POST, informe o conteúdo do objeto Livro a ser alterado no campo central. Se tudo correr bem, teremos como resultado um status 200 – Ok (Figura 15), caso contrário, se informarmos um ID inexistente, teremos um 404 – Not Found.

#### Mensagem enviada via PUT

Para verificar a alteração, podemos fazer outra requisição GET e verificar a lista de todos os livros.

Por fim, para testar o método DELETE, além de mudar o verbo ao lado do endereço, devemos adicionar ao fim da URL o ID do livro a ser excluído, semelhante ao que fizemos no segundo GET. Conforme a Figura 16, observe que a URL será a mesma, porém, como o verbo utilizado é outro, o serviço Web API reconhecerá essa diferença e direcionará a requisição a outra action (Delete, neste caso).

#### Requisição com verbo DELETE

Agora podemos fazer outra requisição via GET para o endereço base e veremos que a lista foi atualizada, como mostra a Figura 17.

- Lista atualizada após operações

Além das funcionalidades que exploramos aqui, o Postman permite ainda trabalhar em times, customizar ambientes de teste, importar arquivos com requisições pré-definidas, entre outras.

Quando se está desenvolvendo um serviço que será exposto para clientes externos, é fundamental que os mais diversos testes sejam realizados a fim de validar o funcionamento da aplicação diante das diversas situações possíveis. Com o Postman essa tarefa é simplificada, pois podemos facilmente enviar requests HTTP para serviços RESTful, enviando parâmetros e recebendo as devidas respostas, além de analisar o tempo gasto em cada requisição, o que também pode auxiliar na localização de problemas de desempenho.

A ferramenta possui ampla documentação, que pode ser encontrada no link no final do artigo, além de uma versão paga que conta com alguns recursos adicionais, como o trabalho em nuvem.

Links

Página oficial do Postman
http::/getpostman.com

Chrome Web Store
https://chrome.google.com/webstore/category/apps

ASP.NET Web API
http://www.asp.net/web-api


Read more: http://www.linhadecodigo.com.br/artigo/3712/testando-servicos-web-api-com-postman.aspx#ixzz6xyDqwnBj

[Artigo original](http://www.linhadecodigo.com.br/artigo/3712/testando-servicos-web-api-com-postman.aspx) 