# ASP.NET

# Criando a primeira aplicação com .Net

```jsx
dotnet new web -o MinhaApi        // cria uma aplicação nova
cd .\MinhaApi\                    // localiza a pasta
dotnet clear                      // limpa os codigos
dotnet run                        // roda a aplicação
```

eu criei a api pela interface normal do visual studio e depois excluir algumas partes do swagger para acessar somente a url pura e da o retorno de mensagem somente.

---

# Protocolo HTTPS,DNS e Fundamentos

**1. Protocolo HTTPS:**

O HTTPS (Hyper Text Transfer Protocol Secure) é um protocolo de comunicação seguro utilizado para transferir dados entre um navegador web (cliente) e um servidor web. Ele é uma versão mais segura do HTTP e é amplamente utilizado para proteger a privacidade e a integridade dos dados transmitidos pela internet.

Principais características do HTTPS:

- **Criptografia:** O HTTPS utiliza criptografia SSL/TLS para proteger os dados durante a transferência. Isso significa que os dados são codificados antes de serem enviados e só podem ser decodificados pelo destinatário correto.
- **Autenticação:** O certificado SSL/TLS utilizado no HTTPS permite a autenticação do servidor, garantindo que o usuário está se conectando ao servidor correto e não a um impostor.
- **Integridade dos dados:** O HTTPS garante que os dados não sejam alterados ou corrompidos durante a transferência, pois qualquer modificação seria detectada pela criptografia.

**2. Sistema de Nomes de Domínio (DNS):**

O DNS (Domain Name System) é um sistema que traduz nomes de domínio legíveis para humanos (como "**[www.exemplo.com](http://www.exemplo.com/)**") em endereços IP (como "192.168.1.1") que os computadores usam para identificar servidores na internet. Em vez de memorizar endereços IP numéricos, os usuários podem acessar sites usando seus nomes de domínio.

Principais conceitos do DNS:

- **Resolução de nomes:** Quando um usuário digita um nome de domínio em um navegador, o computador precisa resolver esse nome em um endereço IP. Isso é feito por meio do processo de resolução de DNS.
- **Hierarquia de domínios:** O DNS possui uma estrutura hierárquica, onde os domínios são organizados em níveis, como o domínio de topo (.com, .org, .net) e os domínios de segundo nível (exemplo.com, exemplo.org).
- **Servidores DNS:** Existem servidores DNS que armazenam informações sobre os domínios e seus respectivos endereços IP. Há servidores raiz, servidores de domínio de topo e servidores autoritativos para cada domínio.
- **Cache DNS:** Para acelerar o processo de resolução, os resultados de consultas DNS podem ser armazenados em cache nos servidores e nos dispositivos dos usuários.

**Fundamentos:**

Ambos HTTPS e DNS são fundamentais para o funcionamento seguro e eficiente da internet. O HTTPS protege a comunicação entre os usuários e os servidores, enquanto o DNS fornece uma maneira amigável de acessar recursos online. Juntos, eles desempenham papéis cruciais na experiência online, garantindo segurança, autenticidade e acessibilidade.

---

# Metodos de Http e envio de requisição

são essas aplicação para ser usadas na API, é a mesma coisa do CRUD, mas com nomes diferentes.

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled.png)

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%201.png)

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%202.png)

podemos ver que o site  e o post man retorna uma informação que enviamos, usando o POST

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%203.png)

---

# RETORNO **HTTP Status Code**

1. **1xx (Informacional):**
    - 100: Continue
    - 101: Mudando Protocolos
    - 102: Processamento (WebDAV; RFC 2518)
2. **2xx (Sucesso):**
    - 200: OK
    - 201: Criado
    - 204: Sem Conteúdo
    - 206: Conteúdo Parcial
3. **3xx (Redirecionamento):**
    - 300: Múltiplas Escolhas
    - 301: Movido Permanentemente
    - 302: Encontrado (às vezes usado para redirecionamento temporário)
    - 304: Não Modificado
4. **4xx (Erro do Cliente):**
    - 400: Requisição Inválida
    - 401: Não Autorizado
    - 403: Proibido
    - 404: Não Encontrado
    - 422: Entidade Improcessável (WebDAV; RFC 4918)
5. **5xx (Erro do Servidor):**
    - 500: Erro Interno do Servidor
    - 501: Não Implementado
    - 502: Gateway Incorreto
    - 503: Serviço Indisponível
    
    ---
    

# Explicando codigo do program.cs

```csharp
var builder = WebApplication.CreateBuilder(args);    // aqui ele criar a aplicação e o builder é repassado logo abaixo.

var app = builder.Build();
app.MapGet("/", () => "Hello World!");    // temos varias opção de mapGet,mappPost,mapPut,mapDelete

/*  " / " esta barra é a mesma coisa da barra que fica na url do navegador, se caso colocarmos 
algum nome dentro dessa barra, temos que especificar na url tbm, pois ela é a localização do ip*/

/*  "() =>"  esses sinais antes da frase significa funções anonimas, como se fosse um metodo anonimo dando um return*/

app.Run();  // roda a aplicação
```

---

# Enviando parametros para url

```csharp
var builder = WebApplication.CreateBuilder(args);

var app = builder.Build();
app.MapGet("/", () => {
return Results.Ok("Hello World!");
});

app.MapGet("/name/{nome}", (string nome) => { // aqui enviamos o nome pela url, igual no exemplo abaixo
    return Results.Ok($"Hello {nome}");
});

app.Run();
```

precisei escrever “/name/caio” para aparecer meu nome depois do hello, mas no código nao precisa de colocar /name/, isso foi somente para testar e [aps.net](http://aps.net) identificar que se trata de um nome.

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%204.png)

---

# **Parâmetros e enviando dados**

```csharp
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

app.MapGet("/", () =>
{
    return Results.Ok("Hello World");
});

app.MapGet("/name/{nome}", (string nome) =>   // a chave de identificação name na url depois o nome da pessoa
{
    return Results.Ok($"Hello {nome}");      // interpolação de strings para mostrar a reposta
});

app.Run();
```

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%205.png)

---

# Serialização e deserialização

```csharp
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

app.MapGet("/", () =>
{
    return Results.Ok("Hello World");
});

app.MapGet("/name/{nome}", (string nome) =>   
{
    return Results.Ok($"Hello {nome}");      
});

app.MapPost("/", (User user) =>          //fizemos um mapPost para receber os dados e retorna o 200OK
{
    return Results.Ok(user);             
});

app.Run();

public class User
{
    public int Id { get; set; }
    public string Username { get; set; }       // criamos as prop para receber os dados
}
```

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%206.png)

---

# Iniciando o projeto

foi criado a API de modo padrão e criado a pasta model

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%207.png)

```csharp
namespace MeuPrimeiroMVC.Models
{
    public class TodoModel
    {

        public int id { get; set; }

        public string Title  { get; set; }

        public bool Done { get; set; }      

        public DateTime CreatedAt { get; set; }
    }
}
```

---

# Configurando o EntityFramework

primeiro temos que add o seguinte pacote no terminal, sqlite é mais rapido e abstrai algumas alterações, mas no final do curso vamos usar o sqlServer normal

```csharp
dotnet add package Microsoft.EntityFrameworkCore.Sqlite
```

depois vamos add o pacote design

```csharp
dotnet add package Microsoft.EntityFrameworkCore.Design
```

---

# Criando o DBContext e outros erros que foi resolvido

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%208.png)

```csharp
using MeuPrimeiroMVC.Models;
using Microsoft.EntityFrameworkCore;

namespace MeuPrimeiroMVC.Data
{
    public class AppDbContext : DbContext
    {

        public DbSet<TodoModel> Todos { get; set; }

        protected override void OnConfiguring(DbContextOptionsBuilder options)
           => options.UseSqlite("DataSource=app.db;Cache=Shared");
        

    }
}
```

um dos erros que estava ocorrendo para baixar o pacote de design era a imcompatibilidade com outras funções do sistema, principalmente do EntityFramework.tools

resolvir desta maneira (consultando o chatGPT)

```csharp
dotnet ef --version
```

atualizar o pacote que estava desatualizado

```csharp
dotnet tool update --global dotnet-ef
```

## Após isso foi criado o migrations

```csharp
dotnet ef migrations add CreateDatabase
```

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%209.png)

depois para criar o banco e atualizar os dados

```csharp
dotnet ef database update
```

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2010.png)

o app.db é uma DEMO de integração de banco com o sqlLite, isso se trata de um banco offline, mas no decorrer do curso vamos usar o sqlServer

---

# Entendendo o MVC

MVC = Models Views Controllers . é um padrão de arquitetura

vamos usar somente o models e controllers, simplificando os models seria aonde organizar e armazena todas as propriedades, as controllers seria mais a parte de processamento de recebimento e envio de dados

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2011.png)

foi criado uma pasta e uma classe.

Classe:

```csharp
using Microsoft.AspNetCore.Mvc;

namespace MeuPrimeiroMVC.Controllers
{

    [ApiController]  // apontando para o visual estudio que isso é uma API
    public class HomeController : ControllerBase
    {
        [HttpGet]    // apontando para o aspNet que isso se trata de um GET
        public string Get()       
        {

            return "Hello World";
        }

        /* esse metodo é para envio de dados (GET) e todos os metodos dentro da api é uma action, que determina uma ação*/

    }
}
```

---

# Route e controllers

fiz uma alteração antes dos testes e modificações. o swagger estava sendo aberto e não necessitava por enquanto

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2012.png)

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2013.png)

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2014.png)

depois foi feito os testes realizado no postMan para verificar o GET.

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2015.png)

ele explicou um pouco sobre o ROUTE (rotas) , seria mais para colocar um pre fixamento na url, normalmente o pessoal faz isso para fazer o versionamento e ter um controle maior do site.

---

# Adicionando suporte aos controllers

primeiramente foi realizado um teste no post com o ROUTE

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2016.png)

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2017.png)

em sequencia foi feito a seguinte modificação no program.cs

```csharp
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers();  // pedindo para o asp.net adicionar as controllers

var app = builder.Build();   // roda a aplicação

app.MapControllers();  // aqui roda tudo o que pertence ao controller

app.Run();
```

---

# Lendo itens do banco de dados

a primeira modificação foi feita no program.cs na parte que deixamos o [asp.net](http://asp.net) gerenciar as conexões  na linha 4 

```csharp
using MeuPrimeiroMVC.Data;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers();  // pedindo para o asp.net adicionar as controllers

builder.Services.AddDbContext<AppDbContext>();  // quando fazemos isso deixamos o aps.net gerenciar as conexões feita na api no db context

var app = builder.Build();   // roda a aplicação

app.MapControllers();  // aqui roda tudo o que pertence a controlle

app.Run();
```

no home controller vou deixar uma imagem de antes e depois e o código em sequencia

                  ANTES                                                                  DEPOIS 

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2018.png)

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2019.png)

```csharp
using MeuPrimeiroMVC.Data;
using MeuPrimeiroMVC.Models;
using Microsoft.AspNetCore.Mvc;

namespace MeuPrimeiroMVC.Controllers
{

    [ApiController]  // apontando para o visual estudio que isso é uma API
    public class HomeController : ControllerBase
    {
        [HttpGet ("/")]    // apontando para o aspNet que isso se trata de um GET
        public List<TodoModel> Get([FromServices] AppDbContext context)   // foi feito uma injeção de dependencia para apontar os dbcontext como um serviço
        {

            return context.Todos.ToList ();  // instancia de uma lista do todos que fica no modelz
        }

        /* esse metodo é para envio de dados (GET) e todos os metodos dentro da api é uma action, que determina uma ação*/

    }
}
```

depois rodamos o visual studio, esse foi o resultado porque ainda nao inserimos nada.

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2020.png)

---

# Criando um registro

foi criado desta vez o POST para enviar os dados

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2021.png)

código :

```csharp

        [HttpPost("/")]
        public TodoModel Post(
         [FromBody] TodoModel todo,  // ele vai vim no corpo da requisição através do postMan
         [FromServices] AppDbContext context)
        {
            context.Todos.Add(todo);
            context.SaveChanges();
            return todo;
        }
```

no postMan fizemos algumas configurações e fizemos um JSON manualmente para enviar os dados no asp.net

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2022.png)

houve um erro também que estava gerando o erro 415, erro de midia não suportada, o chatGPT me instruiu a modificar as configurações do headers

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2023.png)

---

# CRUD Básico

```csharp
using MeuPrimeiroMVC.Data;
using MeuPrimeiroMVC.Models;
using Microsoft.AspNetCore.Mvc;

namespace MeuPrimeiroMVC.Controllers
{

    [ApiController]  // apontando para o visual estudio que isso é uma API
    public class HomeController : ControllerBase
    {
        [HttpGet ("/")]    // apontando para o aspNet que isso se trata de um GET
        public List<TodoModel> Get([FromServices] AppDbContext context)   // foi feito uma injeção de dependencia para apontar os dbcontext como um serviço
        {

            return context.Todos.ToList ();  // instancia de uma lista do todos que fica no modelz
        }

        /* esse metodo é para envio de dados (GET) e todos os metodos dentro da api é uma action, que determina uma ação*/

        [HttpGet("/{id:int}")]    
        public TodoModel GetById([FromRoute] int id, [FromServices] AppDbContext context)
        {

            return context.Todos.FirstOrDefault(x=>x.Id == id);  
        }

        [HttpPost("/")]
        public TodoModel Post(
         [FromBody] TodoModel todo,  // ele vai vim no corpo da requisição através do postMan
         [FromServices] AppDbContext context)
        {
            context.Todos.Add(todo);
            context.SaveChanges();
            return todo;
        }

        [HttpPut("/{id:int}")]
        public TodoModel Put(
         [FromRoute] int id,   // pegando id pela rota 
         [FromBody] TodoModel todo,  // ele vai vim no corpo da requisição através do postMan
         [FromServices] AppDbContext context)
        {
            var model = context.Todos.FirstOrDefault(x=>x.Id == id);
            if (model == null)
                return todo;

            model.Title = todo.Title;    // selecionando as coluas que vai ser alterada
            model.Done = todo.Done;

            context.Todos.Update(model);   // context para atualizar
            context.SaveChanges();           // salvar no banco
            return model;
        }

        [HttpDelete("/{id:int}")]
        public TodoModel Delete(
         [FromRoute] int id,   // pegando id pela rota 
         [FromServices] AppDbContext context)
        {
            var model = context.Todos.FirstOrDefault(x => x.Id == id);

            context.Todos.Remove(model);   // context para deletar
            context.SaveChanges();           // salvar no banco
            return model;
        }
    }

  }
```

esse foi o teste no put deu tudo certo                                              esse teste foi com o delete, depois tentei buscar usando o GET, ai ele deu 

                                                                                  que o conteúdo não existe

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2024.png)

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2025.png)

---

# Melhorando a API

Esse é o código de otimização:

```csharp
using MeuPrimeiroMVC.Data;
using MeuPrimeiroMVC.Models;
using Microsoft.AspNetCore.Mvc;

namespace MeuPrimeiroMVC.Controllers
{

    [ApiController]  
    public class HomeController : ControllerBase
    {
        [HttpGet ("/")]    
        public IActionResult Get([FromServices] AppDbContext context)  // no  IActionResult ele mostra a mensagem de "bad request" dando exemplo, não fica mostando somente o código de erro para o usuário
       =>  Ok(context.Todos.ToList ());  // expressão lambda quando tem somente um função de retorno

        [HttpGet("/{id:int}")]    
        public IActionResult GetById(
            [FromRoute] int id,
            [FromServices] AppDbContext context)
        {

            var todos = context.Todos.FirstOrDefault(x=>x.Id == id);
            if (todos == null)
                return NotFound();
            return Ok(todos);
        }
        

        [HttpPost("/")]
        public IActionResult Post(
         [FromBody] TodoModel todo,  
         [FromServices] AppDbContext context)
        {
            context.Todos.Add(todo);
            context.SaveChanges();
            return Created($"/{todo.Id}", todo);
        }

        [HttpPut("/{id:int}")]
        public IActionResult Put(
         [FromRoute] int id,  
         [FromBody] TodoModel todo,  
         [FromServices] AppDbContext context)
        {
            var model = context.Todos.FirstOrDefault(x=>x.Id == id);
            if (model == null)
                return NotFound();

            model.Title = todo.Title;    
            model.Done = todo.Done;

            context.Todos.Update(model);   
            context.SaveChanges();           
            return Ok(model);
        }

        [HttpDelete("/{id:int}")]
        public IActionResult Delete(
         [FromRoute] int id,   
         [FromServices] AppDbContext context)
        {
            var model = context.Todos.FirstOrDefault(x => x.Id == id);
            if (model == null)
                return NotFound();

            context.Todos.Remove(model);   
            context.SaveChanges();           
            return Ok(model);
        }
    }

  }
```

---

# Criando um novo projeto [ASP.NET](http://ASP.NET)

depois de criado uma aplicação web no visual studio foi adicionado dois pacotes.

```jsx
dotnet add package microsoft.entityframeworkcore.sqlserver
```

```jsx
dotnet add package microsoft.entityframeworkcore.design
```

[https://github.com/balta-io/2808](https://github.com/balta-io/2808)

nesse link do gitHub ele pediu para pegar a pasta models e data que continha bastante coisa já feita pelo curso anterior de entity.

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2026.png)

o DBcontext foi alterado também e ficou desta forma

```jsx
using Blog.Data.Mappings;
using Blog.Models;
using Microsoft.EntityFrameworkCore;

namespace Blog.Data
{
    public class BlogDataContext : DbContext
    {
        public DbSet<Category> Categories { get; set; }
        public DbSet<Post> Posts { get; set; }

        public DbSet<User> Users { get; set; }

        protected override void OnConfiguring(DbContextOptionsBuilder options)
            => options.UseSqlServer("Server=localhost,1433;Database=Blog;User ID=sa;Password=1q2w3e4r@#$");

        protected override void OnModelCreating(ModelBuilder modelBuilder)
        {
            modelBuilder.ApplyConfiguration(new CategoryMap());
            modelBuilder.ApplyConfiguration(new UserMap());
            modelBuilder.ApplyConfiguration(new PostMap());
        }
    }
}
```

---

# iniciando as controllers e modificando o program.cs

no program.cs foi realizado algumas alterações

```jsx
using Blog.Data;

var builder = WebApplication.CreateBuilder(args);

            builder.Services.AddControllers();

            builder.Services.AddDbContext<BlogDataContext>();

            var app = builder.Build();
            app.MapControllers();

            app.Run();
```

depois foi criado a pasta controllers e HomeControllers

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2027.png)

código do HomeController

```jsx
using Microsoft.AspNetCore.Mvc;

//Health check   checagem de saúde
namespace Blog.Controllers
{

    [ApiController]
    [Route("")]
    public class HomeController : ControllerBase
    {

        [HttpGet("")]
        public IActionResult Get() { 
        
                return Ok();
        }
    }
}
```

---

# Nomeando um endPoint e versionamento

foi criado uma classe nos controllers aonde pega uma lista de informação em categories, depois foi incluído um padrao Rest que altera a url no endPoint

```jsx
using Blog.Data;
using Microsoft.AspNetCore.Mvc;

namespace Blog.Controllers
{
    [ApiController]
    public class CategoryController : ControllerBase
    {

        [HttpGet("categories")]   // isso é um padrão de ApiRest, ele altera a URL no endPoint
                                   

        public IActionResult Get(
            [FromServices]BlogDataContext context)
        {
            var categories = context.Categories.ToList();
            return Ok(categories);
        }
    }
}
```

essa é a parte no versionamento é um hábito simples, mas que faz uma diferença para outros programadores e também quando for realizado algum tipo de manutenção futura no sistema

```jsx
using Blog.Data;
using Microsoft.AspNetCore.Mvc;

namespace Blog.Controllers
{
    [ApiController]
    public class CategoryController : ControllerBase
    {

        [HttpGet("v1/categories")]   // isso é um padrão de ApiRest, ele altera a URL no endPoint
                                   //localHost:PORT/v1/categories

        public IActionResult Get(
            [FromServices]BlogDataContext context)
        {
            var categories = context.Categories.ToList();
            return Ok(categories);
        }

        [HttpGet("v2/categories")]   
                                     //localHost:PORT/v2/categories

        public IActionResult Get2(
    [FromServices] BlogDataContext context)
        {
            var categories = context.Categories.ToList();
            return Ok(categories);
        }
    }
}
```

podemos ver que tem a versão 1 (antiga), versão 2 (nova), em apps o cash consegue segurar a versão antiga do app para continuar funcionando ainda para que não atualizou, depois de um prazo determinado as versões anteriores é descontinuada e segue com as versões mais novas, isso acontece tanto em aplicações web e principalmente em app, esse código acima é um exemplo e ajuda demais a refatorar ou realizar otimização no sistema.

localHost:PORT/v1/categories o endPoint ficaria assim

---

# Async e Await

com Async podemos fazer múltiplas requisições ao mesmo tempo

com o Await o processamento aguarda aquela tarefa ser concluida

```jsx
using Blog.Data;
using Microsoft.AspNetCore.Mvc;
using Microsoft.EntityFrameworkCore;

namespace Blog.Controllers
{
    [ApiController]
    public class CategoryController : ControllerBase
    {

        [HttpGet("v1/categories")]   // isso é um padrão de ApiRest, ele altera a URL no endPoint
                                   //localHost:PORT/v1/categories

        public async Task<IActionResult> Get(   // sempre que possivel usar ao maximo o async com  IActionResult
            [FromServices]BlogDataContext context)
        {
            var categories = await context.Categories.ToListAsync();  // foi realizado o await aqui para que o return aguarde a tarefa ser concluida.
            return Ok(categories);
        }

    }
}
```

foi colocado um await embaixo para que o return aguarde a tarefa categories ser concluida e depois retornar, porque caso fosse ativados paralelamentes ele ia retornar uma tarefa em cima de outra tarefa.

---

# CRUD de categorias

foi criado um crud de categorias conforme o código

```jsx
using Blog.Data;
using Blog.Models;
using Microsoft.AspNetCore.Mvc;
using Microsoft.EntityFrameworkCore;

namespace Blog.Controllers
{
    [ApiController]
    public class CategoryController : ControllerBase
    {

        [HttpGet("v1/categories")]   // isso é um padrão de ApiRest, ele altera a URL no endPoint
                                   //localHost:PORT/v1/categories

        public async Task<IActionResult> Get(   // sempre que possivel usar ao maximo o async com  IActionResult
            [FromServices]BlogDataContext context)
        {
            var categories = await context.Categories.ToListAsync();  // foi realizado o await aqui para que o return aguarde a tarefa ser concluida.
            return Ok(categories);
        }

        [HttpGet("v1/categories/{id:int}")]
        public async Task<IActionResult> GetByIdAsync(
        [FromRoute] int id,
        [FromServices] BlogDataContext context)

        {
            var category = await context
                .Categories
                .FirstOrDefaultAsync(x=>x.Id == id);  

            if (category == null)
                return NotFound();

            return Ok(category);
        }

        [HttpPost("v1/categories/")]
        public async Task<IActionResult> PostAsync(
        [FromBody] Category model,
        [FromServices] BlogDataContext context)

        {
           await context.Categories.AddAsync(model);
           await context.SaveChangesAsync();

            return Created($"v1/categories/{model.Id}", model);
        }

        [HttpPut("v1/categories/{id:int}")]
        public async Task<IActionResult> PutAsync(
        [FromRoute] int id,
        [FromBody] Category model,
        [FromServices] BlogDataContext context)

        {
            var category = await context
                .Categories
                .FirstOrDefaultAsync(x => x.Id == id);

            if (category == null)
                return NotFound();

            category.Name = model.Name;
            category.Slug = model.Slug;

            context.Categories.Update(category);
            await context.SaveChangesAsync();

            return Ok(model);
        }

        [HttpDelete("v1/categories/{id:int}")]
        public async Task<IActionResult> DeleteAsync(
        [FromRoute] int id,
        [FromServices] BlogDataContext context)

        {
            var category = await context
                .Categories
                .FirstOrDefaultAsync(x => x.Id == id);

            if (category == null)
                return NotFound();

            context.Categories.Remove(category);
            await context.SaveChangesAsync();

            return Ok(category);
        }
    }
}
```

---

# Testando a api e gerando exceptions

foi realizado essa alteração no código

```jsx
[HttpPost("v1/categories/")]
        public async Task<IActionResult> PostAsync(
        [FromBody] Category model,
        [FromServices] BlogDataContext context)

        {
            try
            {
                await context.Categories.AddAsync(model);
                await context.SaveChangesAsync();

                return Created($"v1/categories/{model.Id}", model);
            }
            catch (DbUpdateException)
            {
                return StatusCode(500,"não foi possivel incluir a categoria");

            }
            catch (Exception ex)
            {

                return StatusCode(500, "falha interna do servidor");
            }
        }
```

esta sendo gerado um erro no id de proposito, para que pudessemos gerar essas exceptions, o erro foi tentar incluir um id e enviar pelo postMan, mas no .net deixamos um id que gera automaticamente

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2028.png)

depois foi criado as informações com o json, mas sem especificar o id, deu tudo certo

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2029.png)

depois foi acionado o json criado no .net

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2030.png)

Depois disso usei o postMan para realizar a busca dos dados, atualizar, deletar e depois buscar os dados de novo. Foi realizado os testes em toda camada da Api e funcionou corretamente

---

# Melhorando o código da Api

foi colocado try e catch em todos os métodos, pois caso ocorra algum erro com o usuário, devemos mostrar a mensagem e verificar aonde está o erro.

```jsx
using Blog.Data;
using Blog.Models;
using Microsoft.AspNetCore.Mvc;
using Microsoft.EntityFrameworkCore;

namespace Blog.Controllers
{
    [ApiController]
    public class CategoryController : ControllerBase
    {

        [HttpGet("v1/categories")]   // isso é um padrão de ApiRest, ele altera a URL no endPoint
                                   //localHost:PORT/v1/categories

        public async Task<IActionResult> Get(   // sempre que possivel usar ao maximo o async com  IActionResult
            [FromServices]BlogDataContext context)
        {
            try
            {
                var categories = await context.Categories.ToListAsync();  // foi realizado o await aqui para que o return aguarde a tarefa ser concluida.
                return Ok(categories);
            }
            catch (Exception ex)
            {

                return StatusCode(500, "falha interna do servidor");
            }
        }

        [HttpGet("v1/categories/{id:int}")]
        public async Task<IActionResult> GetByIdAsync(
        [FromRoute] int id,
        [FromServices] BlogDataContext context)

        {
            try
            {
                var category = await context
                .Categories
                .FirstOrDefaultAsync(x => x.Id == id);

                if (category == null)
                    return NotFound();

                return Ok(category);
            }
            catch (Exception ex)
            {

                return StatusCode(500, "falha interna do servidor");
            }
        }

        [HttpPost("v1/categories/")]
        public async Task<IActionResult> PostAsync(
        [FromBody] Category model,
        [FromServices] BlogDataContext context)

        {
            try
            {
                await context.Categories.AddAsync(model);
                await context.SaveChangesAsync();

                return Created($"v1/categories/{model.Id}", model);
            }
            catch (DbUpdateException)
            {
                return StatusCode(500,"não foi possivel incluir a categoria");

            }
            catch (Exception ex)
            {

                return StatusCode(500, "falha interna do servidor");
            }
        }

        [HttpPut("v1/categories/{id:int}")]
        public async Task<IActionResult> PutAsync(
        [FromRoute] int id,
        [FromBody] Category model,
        [FromServices] BlogDataContext context)

        {
            try
            {
                var category = await context
                .Categories
                .FirstOrDefaultAsync(x => x.Id == id);

                if (category == null)
                    return NotFound();

                category.Name = model.Name;
                category.Slug = model.Slug;

                context.Categories.Update(category);
                await context.SaveChangesAsync();

                return Ok(model);
            }
            catch (DbUpdateException)
            {
                return StatusCode(500, "não foi possivel Atualizar a categoria");

            }
            catch (Exception ex)
            {

                return StatusCode(500, "falha interna do servidor");
            }
        }

        [HttpDelete("v1/categories/{id:int}")]
        public async Task<IActionResult> DeleteAsync(
        [FromRoute] int id,
        [FromServices] BlogDataContext context)

        {
            try
            {
                var category = await context
                .Categories
                .FirstOrDefaultAsync(x => x.Id == id);

                if (category == null)
                    return NotFound();

                context.Categories.Remove(category);
                await context.SaveChangesAsync();

                return Ok(category);
            }
            catch (DbUpdateException)
            {
                return StatusCode(500, "não foi possivel deletar a categoria");

            }
            catch (Exception ex)
            {

                return StatusCode(500, "falha interna do servidor");
            }
        }
    }
}
```

---

# Criando o view Models e otimizando mais ainda o código

primeiramente vou mostrar o antes e depois do post(criar), deixamos uma classe especifica somente para o trabalho dos dados que chega da tela inicial

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2031.png)

essa classe foi criado na intenção de separar as informações que chegam pra gente
através da tela, ex disso, quando alguém tenta acessa seu usuário na tela de login ou criar um login mesmo, 
tanto que category controller vamos deixar um tipo de criação padrao apontando para o category criado lá mesmo

```csharp
namespace Blog.ViewModels
{
    public class CreateCategoryViewModel
    {
           
        public string Name { get; set; }

        public string Slug { get; set;}
    }
}
```

código antes :

```csharp
        [HttpPost("v1/categories/")]
        public async Task<IActionResult> PostAsync(
        [FromBody] Category model,
        [FromServices] BlogDataContext context)

        {
            try
            {
                await context.Categories.AddAsync(model);
                await context.SaveChangesAsync();

                return Created($"v1/categories/{model.Id}", model);
            }
            catch (DbUpdateException)
            {
                return StatusCode(500,"não foi possivel incluir a categoria");

            }
            catch (Exception ex)
            {

                return StatusCode(500, "falha interna do servidor");
            }
        }
```

código Depois :

repara que deixamos o CreateCategoryViewModel responsável pela entrada de dados e pelo Post, ai fica muito mais otimizado, além disso o model fica mais leve e também deixamos somente os dados necessários para o usuário incluir.

```csharp
[HttpPost("v1/categories/")]
        public async Task<IActionResult> PostAsync(
        [FromBody] CreateCategoryViewModel model,   // tivemos que mudar a entrada de dados
        [FromServices] BlogDataContext context)

        {
            try
            {               // na hora de criar deixamos esse padrão
                var category = new Category { 
                    Id =0,
                    // Posts = null,    na vdd não precisa de incluir, pois ele ja cria nulo
                    Name = model.Name,
                    Slug = model.Slug.ToLower(),
                
                };
                await context.Categories.AddAsync(category);
                await context.SaveChangesAsync();

                return Created($"v1/categories/{category.Id}", category);
            }
            catch (DbUpdateException)
            {
                return StatusCode(500,"não foi possivel incluir a categoria");

            }
            catch (Exception ex)
            {

                return StatusCode(500, "falha interna do servidor");
            }
        }
```

---

# EditorViewModels

foi alterado o nome da classe

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2032.png)

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2033.png)

EditorCategoryViewModel foi colocado no post(criar) e no put(atualizar), o put ja estava configurado de forma correta para receber essa classe. Essa classe esta pronta para criar e atualizar as informações que chega da tela.

---

# Validações

usando o required e o stringlength conseguimos gerar validações para regras e o usuário criar ou atualizar de acordo com a regra da empresa

```csharp
using System.ComponentModel.DataAnnotations;

namespace Blog.ViewModels
{
    public class EditorCategoryViewModel
    {
        [Required(ErrorMessage =" O nome é obrigatório")]   // nome obrigatorio na hora de criar
        [StringLength(40, MinimumLength =3, ErrorMessage = "Este campo deve conter entre 3 e 40 caracteres")]
        public string Name { get; set; }

        [Required(ErrorMessage = " O slug é obrigatório")]   // slug obrigatorio na hora de criar
        public string Slug { get; set;}
    }
}
```

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2034.png)

---

# Padronização

foi usada uma sobrecarga de metodo, usada também o construtor na classe ResultViewModel

```csharp
namespace Blog.ViewModels
{
    public class ResultViewModel<T>    // tipo generico 
    {

        public ResultViewModel(T data, List<string> errors)
        {
                Data = data;
                Errors = errors;
        }

        public ResultViewModel(T data)
        {
            Data = data;
            
        }

        public ResultViewModel(List<string> errors)
        {
            Errors = errors;
        }

        public ResultViewModel(string error)
        {
            Errors.Add(error);
        }

        public T Data { get; private set; }

        public List<string> Errors { get; private set; } = new();

    }
}
```

alteração no program.cs 

```csharp
using System.Globalization;
using Blog.Data;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers().ConfigureApiBehaviorOptions(options =>{      // essa parte faz com que a validação não seja obrigatoria, depois vou pesquisar exatamente oq faz 

        options.SuppressModelStateInvalidFilter = true;
});

builder.Services.AddDbContext<BlogDataContext>();

var app = builder.Build();
app.MapControllers();

app.Run();
```

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2035.png)

essa parte do get esta linkada com a classe ResultViewModel

```csharp
public async Task<IActionResult> GetAsync(   // sempre que possivel usar ao maximo o async com  IActionResult
            [FromServices]BlogDataContext context)
        {
            try
            {
                var categories = await context.Categories.ToListAsync();  // foi realizado o await aqui para que o return aguarde a tarefa ser concluida.
                return Ok(new ResultViewModel<List<Category>>(categories));
            }
            catch
            {

                return StatusCode(500, new ResultViewModel<List<Category>>("falha interna do servidor"));
            }
        }
```

e foi gerado esse resultado utilizando o get no postMan:

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2036.png)

na parte do data ele mostra todos os dados em uma lista generica e na parte de baixo uma lista generica de erros, tudo isso foi feito na classe ResultViewModel

---

# Melhorando o getByIdAsync

foi modificado nos return para que surgisse uma nova mensagem de erro 

```csharp
[HttpGet("v1/categories/{id:int}")]
        public async Task<IActionResult> GetByIdAsync(
        [FromRoute] int id,
        [FromServices] BlogDataContext context)

        {
            try
            {
                var category = await context
                .Categories
                .FirstOrDefaultAsync(x => x.Id == id);

                if (category == null)
                    return NotFound(new ResultViewModel<Category>("Conteúdo não encontrado"));

                return Ok(new ResultViewModel<Category>(category));
            }
            catch
            {

                return StatusCode(500, new ResultViewModel<Category>("falha interna do servidor"));
            }
        }
```

como pode ver acionamos um id errado, para que ele enviasse uma mensagem de erro para o usuário

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2037.png)

---

# Padronizando o BadRequest

esse padrão usado é para deixa a mensagem de erro mais amigavel para o pessoal do front-end e para o usuário.

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2038.png)

---

# Autenticação e Autorização

foi criado uma nova classe na raiz do projeto

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2039.png)

peguei um codigo GUID para encriptar e fazer alguns testes

```csharp
namespace Blog
{
    public static class Configuration
    {

        // TOKEN - JWT - Json Web Token
        public static string JwtKey { get; set; } = "5ea2ad53-50fb-4c0f-9dc5-50fc585d54c8";

    }
}
```

---

# Token Service

tivemos que baixar um pacote da autenticação

```csharp
dotnet add package microsoft.aspnetcore.authentication
dotnet add package Microsoft.AspNetCore.Authentication.JwtBearer
```

foi criado uma nova pasta e mais uma nova classe

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2040.png)

essa classe é responsável por gerar um token

```csharp
using Blog.Models;
using Microsoft.IdentityModel.Tokens;
using System.IdentityModel.Tokens.Jwt;
using System.Text;

namespace Blog.Services
{
    public class TokenServices             // finalidade dessa classe é para gerar um Token
    {

        public string GenerateToken(User user)
        {

            var tokenHandler = new JwtSecurityTokenHandler();
            var key = Encoding.ASCII.GetBytes(Configuration.JwtKey);
            var tokenDescriptor = new SecurityTokenDescriptor();
            var token = tokenHandler.CreateToken(tokenDescriptor);
            return tokenHandler.WriteToken(token);

        }

    }
}
```

no proximo video foi adicionado no token um tempo de expiração para segurança também

```csharp
using Blog.Models;
using Microsoft.IdentityModel.Tokens;
using System.IdentityModel.Tokens.Jwt;
using System.Text;

namespace Blog.Services
{
    public class TokenServices             // finalidade dessa classe é para gerar um Token
    {

        public string GenerateToken(User user)
        {

            var tokenHandler = new JwtSecurityTokenHandler();
            var key = Encoding.ASCII.GetBytes(Configuration.JwtKey);
            var tokenDescriptor = new SecurityTokenDescriptor
            {
                Expires = DateTime.UtcNow.AddHours(8),    // limite de oito horas de token, pois ele pode ser descoberto por hacker e usado tbm caso ele fosse permanente
                SigningCredentials = new SigningCredentials(
                    new SymmetricSecurityKey(key), SecurityAlgorithms.HmacSha256Signature)
            };
            var token = tokenHandler.CreateToken(tokenDescriptor);
            return tokenHandler.WriteToken(token);

        }

    }
}
```

---

# Injeção de dependência

primeiramente foi criado uma nova classe chamada accountController

```csharp
using Blog.Services;
using Microsoft.AspNetCore.Mvc;

namespace Blog.Controllers
{
    [ApiController]
    public class AccountController : ControllerBase
    {
        private readonly TokenServices _tokenServices;               // injeção
        public AccountController(TokenServices tokenService)            // construtor para gerar a dependencia
        {
            _tokenServices = tokenService;
        }

        [HttpPost("v1/login")]
        public IActionResult Login()
        {

            var token = _tokenServices.GenerateToken(null);

            return Ok(token);
        }

    }
}
```

---

# AddSigleton,scoped,transient

```csharp
using System.Globalization;
using Blog.Data;
using Blog.Services;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers().ConfigureApiBehaviorOptions(options =>{    

        options.SuppressModelStateInvalidFilter = true;
});

builder.Services.AddDbContext<BlogDataContext>();   // sempre que usar o dataContext utilizar essa instancia
builder.Services.AddTransient<TokenServices>();                    // sempre vai criar uma nova instancia no token, cada vez que acionado
//builder.Services.AddScoped();                       // ele sempre dura por transação aonde ele estiver instanciado, enquanto a transação durar ele funciona
//builder.Services.AddSingleton();                    // um por app, ele nunca derruba da aplicação, sempre fica carregando, consome muita memoria por isso

var app = builder.Build();
app.MapControllers();

app.Run();
```

---

# Gerando um token na requisição

usando o claim para gerar alguma string

```csharp
using Blog.Models;
using Microsoft.IdentityModel.Tokens;
using System.IdentityModel.Tokens.Jwt;
using System.Security.Claims;
using System.Text;

namespace Blog.Services
{
    public class TokenServices             // finalidade dessa classe é para gerar um Token
    {

        public string GenerateToken(User user)
        {

            var tokenHandler = new JwtSecurityTokenHandler();
            var key = Encoding.ASCII.GetBytes(Configuration.JwtKey);
            var tokenDescriptor = new SecurityTokenDescriptor
            {
               Subject = new ClaimsIdentity(new Claim[]{
                
                    new Claim("fruta","banana")
                }),
                Expires = DateTime.UtcNow.AddHours(8),    // limite de oito horas de token, pois ele pode ser descoberto por hacker e usado tbm caso ele fosse permanente
                SigningCredentials = new SigningCredentials(
                new SymmetricSecurityKey(key), 
                SecurityAlgorithms.HmacSha256Signature)
            };
            var token = tokenHandler.CreateToken(tokenDescriptor);
            return tokenHandler.WriteToken(token);

        }

    }
}
```

depois da requisição no postMan foi gerado esse resultado

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2041.png)

através dessa imagem podemos ver que após descriptografar o token, ele consegue indentificar as strings digitada no visual studio

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2042.png)

no final do video o codigo ficou assim 

```csharp
using Blog.Models;
using Microsoft.IdentityModel.Tokens;
using System.IdentityModel.Tokens.Jwt;
using System.Security.Claims;
using System.Text;

namespace Blog.Services
{
    public class TokenServices             // finalidade dessa classe é para gerar um Token
    {

        public string GenerateToken(User user)
        {

            var tokenHandler = new JwtSecurityTokenHandler();
            var key = Encoding.ASCII.GetBytes(Configuration.JwtKey);
            var tokenDescriptor = new SecurityTokenDescriptor
            {
               Subject = new ClaimsIdentity(new Claim[]{    // uma lista de claims

                    new (ClaimTypes.Name,"caioSilva"),     // User.indentity.Name
                    new (ClaimTypes.Role,"admin"),          // User.IsInRole
                    new ("fruta","banana")
                }),
                Expires = DateTime.UtcNow.AddHours(8),    // limite de oito horas de token, pois ele pode ser descoberto por hacker e usado tbm caso ele fosse permanente
                SigningCredentials = new SigningCredentials(
                new SymmetricSecurityKey(key), 
                SecurityAlgorithms.HmacSha256Signature)
            };
            var token = tokenHandler.CreateToken(tokenDescriptor);
            return tokenHandler.WriteToken(token);

        }

    }
}
```

com esse resultado

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2043.png)

---

# Configurando Autenticação e Autorização

essa parte marcada de vermelho é o que foi configurado.

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2044.png)

```csharp
using System.Globalization;
using System.Text;
using Blog;
using Blog.Data;
using Blog.Services;
using Microsoft.AspNetCore.Authentication.JwtBearer;
using Microsoft.IdentityModel.Tokens;

var builder = WebApplication.CreateBuilder(args);

var key = Encoding.ASCII.GetBytes(Configuration.JwtKey);
builder.Services.AddAuthentication(x =>
{
    x.DefaultAuthenticateScheme = JwtBearerDefaults.AuthenticationScheme;
    x.DefaultChallengeScheme = JwtBearerDefaults.AuthenticationScheme;
}).AddJwtBearer(x =>
{
    x.TokenValidationParameters = new TokenValidationParameters
    {
        ValidateIssuerSigningKey = true,                     // validar a chave de assinatura
        IssuerSigningKey = new SymmetricSecurityKey(key),       
        ValidateIssuer = false,
        ValidateAudience = false
    };
});

builder.Services.AddControllers().ConfigureApiBehaviorOptions(options =>{    

        options.SuppressModelStateInvalidFilter = true;
});

builder.Services.AddDbContext<BlogDataContext>();   // sempre que usar o dataContext utilizar essa instancia
builder.Services.AddTransient<TokenServices>();                    // sempre vai criar uma nova instancia no token, cada vez que acionado
//builder.Services.AddScoped();                       // ele sempre dura por transação aonde ele estiver instanciado, enquanto a transação durar ele funciona
//builder.Services.AddSingleton();                    // um por app, ele nunca derruba da aplicação, sempre fica carregando, consome muita memoria por isso

var app = builder.Build();

app.UseAuthentication();        // autenticação vem antes de autorização
app.UseAuthorization();         // essa ordem para indentificar quem você é, e o que pode fazer

app.MapControllers();

app.Run();
```

---

# TESTANDO AUTENTICAÇÃO E AUTORIZAÇÃO

foi feito algumas alterações no codigo do AccountController

```csharp
using Blog.Services;
using Microsoft.AspNetCore.Authorization;
using Microsoft.AspNetCore.Mvc;

namespace Blog.Controllers
{
    
    [ApiController]
    public class AccountController : ControllerBase
    {
        
        private readonly TokenServices _tokenServices;
        public AccountController(TokenServices tokenService)
        {
            _tokenServices = tokenService;
        }

        [AllowAnonymous]
        [HttpPost("v1/login")]
        public IActionResult Login()
        {

            var token = _tokenServices.GenerateToken(null);

            return Ok(token);
        }

        [Authorize(Roles = "user")]
        [HttpGet("v1/user")]
        public IActionResult GetUser() => Ok(User.Identity.Name);

        [Authorize(Roles = "author")]
        [HttpGet("v1/author")]
        public IActionResult GetAuthor() => Ok(User.Identity.Name);

        [Authorize(Roles = "admin")]
        [HttpGet("v1/admin")]
        public IActionResult GetAdmin() => Ok(User.Identity.Name);

    }
}
```

```csharp
using Blog.Models;
using Microsoft.IdentityModel.Tokens;
using System.IdentityModel.Tokens.Jwt;
using System.Security.Claims;
using System.Text;

namespace Blog.Services
{
    public class TokenServices             // finalidade dessa classe é para gerar um Token
    {

        public string GenerateToken(User user)
        {

            var tokenHandler = new JwtSecurityTokenHandler();
            var key = Encoding.ASCII.GetBytes(Configuration.JwtKey);
            var tokenDescriptor = new SecurityTokenDescriptor
            {
               Subject = new ClaimsIdentity(new Claim[]{    // uma lista de claims

                    new (ClaimTypes.Name,"caioSilva"),     // User.indentity.Name
                    new (ClaimTypes.Role,"user"),          // User.IsInRole
                    new (ClaimTypes.Role,"admin"),           // gerei mais uma claim para autorizar o login
                    new ("fruta","banana")
                }),
                Expires = DateTime.UtcNow.AddHours(8),    // limite de oito horas de token, pois ele pode ser descoberto por hacker e usado tbm caso ele fosse permanente
                SigningCredentials = new SigningCredentials(
                new SymmetricSecurityKey(key), 
                SecurityAlgorithms.HmacSha256Signature)
            };
            var token = tokenHandler.CreateToken(tokenDescriptor);
            return tokenHandler.WriteToken(token);

        }

    }
}
```

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2045.png)

essa é a configuração do postMan

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2046.png)

tentei mudar o Json que fica no site, ele gerou um novo token criptografado, após tentar gerar ele no postMan, deu não autorizado

---

# Gerando um novo usuario

primeiramente vamos baixar um novo pacote, segue o código:

```csharp
dotnet add package SecureIdentity
```

apos gerar a aplicação e debugar consultei para verificar se ele salvou os dados corretos

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2047.png)

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2048.png)

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2049.png)

---

# Autenticando Login

primeiro fazemos algumas verificações no login, verificamos o email para sabe se esta correto ou nullo

```csharp
using Blog.Data;
using Blog.Extensions;
using Blog.Models;
using Blog.Services;
using Blog.ViewModels;
using Microsoft.AspNetCore.Mvc;
using Microsoft.EntityFrameworkCore;
using SecureIdentity.Password;

namespace Blog.Controllers;

[ApiController]
public class AccountController : ControllerBase
{
    [HttpPost("v1/accounts/")]
    public async Task<IActionResult> Post(
        [FromBody] RegisterViewModel model,
        [FromServices] BlogDataContext context)
    {
        if (!ModelState.IsValid)
            return BadRequest(new ResultViewModel<string>(ModelState.GetErrors()));

        var user = new User
        {
            Name = model.Name,
            Email = model.Email,
            Slug = model.Email.Replace("@", "-").Replace(".", "-")
        };

        var password = PasswordGenerator.Generate(25);
        user.PasswordHash = PasswordHasher.Hash(password);

        try
        {
            await context.Users.AddAsync(user);
            await context.SaveChangesAsync();

            return Ok(new ResultViewModel<dynamic>(new
            {
                user = user.Email,
                password
            }));
        }
        catch (DbUpdateException)
        {
            return StatusCode(400, new ResultViewModel<string>("05X99 - Este E-mail já está cadastrado"));
        }
        catch
        {
            return StatusCode(500, new ResultViewModel<string>("05X04 - Falha interna no servidor"));
        }
    }

    [HttpPost("v1/accounts/login")]
    public async Task<IActionResult> Login(
        [FromBody] LoginViewModel model,
        [FromServices] BlogDataContext context,
        [FromServices] TokenServices tokenServices)
    {

        if (!ModelState.IsValid)
            return BadRequest(new ResultViewModel<string>(ModelState.GetErrors()));

        var user = await context
            .Users
            .AsNoTracking()
            .Include(x => x.Roles)
            .FirstOrDefaultAsync(x => x.Email == model.Email);

        if (user == null)
            return StatusCode(401, new ResultViewModel<string>("Usuário ou senha inválidos"));  // usuario ou senha null

        if (!PasswordHasher.Verify(user.PasswordHash, model.Password))    // verifica se a hash é a mesma da senha
            return StatusCode(401, new ResultViewModel<string>("Usuário ou senha inválidos"));

        try
        {
            var token = tokenServices.GenerateToken(user);
            return Ok(new ResultViewModel<string>(token, null));
        }
        catch
        {
            return StatusCode(500, new ResultViewModel<string>("05X04 - Falha interna no servidor"));
        }
    }

}
```

fizemos a construção do login.

podemos ver que nas verificações da hash o ultimo caso é o melhor, na primeira ele fica fazendo requisição e nisso gera hash diferente

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2050.png)

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2051.png)

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2052.png)

depois no postMan ele gerou um token.

---

# Gerando tokens com Claims

foi criado mais uma classe 

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2053.png)

```csharp
using Blog.Models;
using Microsoft.AspNetCore.Authorization;
using System.Security.Claims;

namespace Blog.Extensions
{
    public static class RoleClaimsExtention
    {
        public static IEnumerable<Claim> GetClaims(this User user )
        {

            var result = new List<Claim>
            {

                new(ClaimTypes.Name, user.Email)
            };
            result.AddRange(user.Roles.Select(role => new Claim(ClaimTypes.Role, role.Slug)));
            return result;
        }
    }
}
```

foi refatorado a classe tokenServices

```csharp
using Blog.Extensions;
using Blog.Models;
using Microsoft.IdentityModel.Tokens;
using System.IdentityModel.Tokens.Jwt;
using System.Security.Claims;
using System.Text;

namespace Blog.Services
{
    public class TokenServices             // finalidade dessa classe é para gerar um Token
    {

        public string GenerateToken(User user)
        {

            var tokenHandler = new JwtSecurityTokenHandler();
            var key = Encoding.ASCII.GetBytes(Configuration.JwtKey);
            var claims = user.GetClaims();
            var tokenDescriptor = new SecurityTokenDescriptor
            {
               Subject = new ClaimsIdentity(claims),
                Expires = DateTime.UtcNow.AddHours(8),    // limite de oito horas de token, pois ele pode ser descoberto por hacker e usado tbm caso ele fosse permanente
                SigningCredentials = new SigningCredentials(
                new SymmetricSecurityKey(key), 
                SecurityAlgorithms.HmacSha256Signature)
            };
            var token = tokenHandler.CreateToken(tokenDescriptor);
            return tokenHandler.WriteToken(token);

        }

    }
}
```

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2054.png)

depois de gerado o resultado foi incluido os roles no usuario

---

# Autenticação por Api Key

foi criado uma nova pasta e uma nova classe

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2055.png)

```csharp
using Microsoft.AspNetCore.Mvc;
using Microsoft.AspNetCore.Mvc.Filters;

namespace Blog.Attributes;

[AttributeUsage(validOn: AttributeTargets.Class | AttributeTargets.Method)]
public class ApiKeyAttribute : Attribute, IAsyncActionFilter
{
    public async Task OnActionExecutionAsync(
        ActionExecutingContext context,
        ActionExecutionDelegate next)
    {
        if (!context.HttpContext.Request.Query.TryGetValue(Configuration.ApiKeyName, out var extractedApiKey))
        {
            context.Result = new ContentResult()
            {
                StatusCode = 401,
                Content = "ApiKey não encontrada"
            };
            return;
        }

        if (!Configuration.ApiKey.Equals(extractedApiKey))
        {
            context.Result = new ContentResult()
            {
                StatusCode = 403,
                Content = "Acesso não autorizado"
            };
            return;
        }

        await next();
    }
}
```

na classe configuration foi refatorado para isso também

```csharp
namespace Blog
{
    public static class Configuration
    {

        // TOKEN - JWT - Json Web Token
        public static string JwtKey = "5ea2ad53-50fb-4c0f-9dc5-50fc585d54c8";
        public static string ApiKeyName = "api_key";
        public static string ApiKey = "curso_api_IlTevUM/z0ey3NwCV/unWg==";
    }
}
```

isso tudo foi criado na intenção do usuário não fica precisando de logar toda hora para o sistema gerar um novo token que está expirando a todo momento.

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2056.png)

tudo pronto agora vamos para os testes

---

como não colocamos a apikey ele gerou o erro,depois tentamos acessar a api com uma url aleatoria,

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2057.png)

 e depois acessamos com a api correta

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2058.png)

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2059.png)

isso foi basicamente somente um teste no curso, ele disse que é bastante usado no mercado de TI

---

# Entendendo o appSettings

uma das coisas que foi explicada é que no appSettings não devemos deixar dados sensiveis, e deixa os dados imputador no servidor para ninguém ter acesso e não ser hackeado,através do appSettings conseguimos incluir algumas coisas para deixar os dados mais protegido.

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2060.png)

---

# Lendo o AppSettings

foi feito toda esse configuração para que o Json do appsetings possa converter isso para uma classe.

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2061.png)

o appSettings ficou dessa forma em Json

```csharp
{
  "JwtKey": "ZmVkYWY3ZDg4NjNiNDhlMTk3YjkyODdkNDkyYjcwOGU=",
  "ApiKeyName": "api_key",
  "ApiKey": "curso_api_IlTevUM/z0ey3NwCV/unWg==",
  "SmtpConfiguration": {
    "Host": "smtp.sendgrid.net",
    "Port": "587",
    "UserName": "apikey",
    "Password": "suasenha"
  },
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AllowedHosts": "*"
}
```

o configuration foi refatorado e ficou dessa forma

```csharp
namespace Blog
{
    public static class Configuration
    {

        // TOKEN - JWT - Json Web Token
        public static string JwtKey = "5ea2ad53-50fb-4c0f-9dc5-50fc585d54c8";
        public static string ApiKeyName = "api_key";
        public static string ApiKey = "curso_api_IlTevUM/z0ey3NwCV/unWg==";
        public static SmtpConfiguration Smtp = new();
        public class SmtpConfiguration     // configuração para envio de email
                                            // esta sendo criado uma classe dentro de uma classe
        {
            public string Host { get; set; }        // precisa da porta do host
            public int Port { get; set; } = 25;     // precisa da porta do servidor
            public string UserName { get; set; }        // precisa do usuario
            public string Password { get; set; }        // precisa da senha
        }
    }
}
```

---

# Organizando o Program.cs e aplicando alguns metódos para organizar o código

antes                                                                             depois

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2062.png)

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2063.png)

bem menor e mais organizado

antes                                                                                            depois

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2064.png)

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2065.png)

antes                                                                                                    depois

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2066.png)

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2067.png)

conclusão

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2068.png)

---

# Configurando o SendGrip

depois de feito o cadastro no sendGrip, fui nas configurações criei uma ApiKey e com acesso restrito e somente para envio de email

depois foi gerado este token:

```csharp
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
```

---

# Criando um serviço de envio de Email

foi criado uma classe nova na pasta services

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2069.png)

depois foi adicionado um pacote SDK no sendGrip

```csharp
dotnet add package sendgrid
```

foi instanciado no program.cs

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2070.png)

codigo do emailService

```csharp
using System.Net;
using System.Net.Mail;

namespace Blog.Services
{
    public class EmailService
    {

        public bool Send(
        string toName,
        string toEmail,
        string subject,
        string body,
        string fromName = "testes",
        string fromEmail = "caiosilvaferreira1@outlook.com.br")
        {
            var smtpClient = new SmtpClient(Configuration.Smtp.Host, Configuration.Smtp.Port);

            smtpClient.Credentials = new NetworkCredential(Configuration.Smtp.UserName, Configuration.Smtp.Password);
            smtpClient.DeliveryMethod = SmtpDeliveryMethod.Network;    // o sendGrip sempre vai usar uma port segura que seria a 587
            smtpClient.EnableSsl = true;      // marcando que é uma porta segura
            var mail = new MailMessage();

            mail.From = new MailAddress(fromEmail, fromName);
            mail.To.Add(new MailAddress(toEmail, toName));           // seria uma lista
            mail.Subject = subject;
            mail.Body = body;
            mail.IsBodyHtml = true;

            try
            {
                smtpClient.Send(mail);       // parte do envio
                return true;                    // try e catch caso der algum erro
            }
            catch (Exception ex)
            {
                return false;
            }

        }
    }
}
```

configuração do appSettings, borrei uma parte da api pois é privado

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2071.png)

com essas credenciais ele gera uma nova senha e manda para o email.

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2072.png)

---

# Criando o PostController

foi criado essa nova classe para lista de post

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2073.png)

```csharp
using Blog.Data;
using Blog.Models;
using Blog.ViewModels;
using Blog.ViewModels.Posts;
using Microsoft.AspNetCore.Mvc;
using Microsoft.EntityFrameworkCore;

namespace Blog.Controllers;

[ApiController]
public class PostController : ControllerBase
{
    [HttpGet("v1/posts")]
    public async Task<IActionResult> GetAsync(
        [FromServices] BlogDataContext context,
        [FromQuery] int page = 0,
        [FromQuery] int pageSize = 25)
    {
        try
        {
            var count = await context.Posts.AsNoTracking().CountAsync();
            var posts = await context
                .Posts
                .AsNoTracking()
                .Include(x => x.Author)
                .Include(x => x.Category)
                .Select(x => new ListPostsViewModel
                {
                    Id = x.Id,
                    Title = x.Title,
                    Slug = x.Slug,
                    LastUpdateDate = x.LastUpdateDate,
                    Category = x.Category.Name,
                    Author = $"{x.Author.Name} ({x.Author.Email})"
                })
                .Skip(page * pageSize)
                .Take(pageSize)
                .OrderByDescending(x => x.LastUpdateDate)
                .ToListAsync();
            return Ok(new ResultViewModel<dynamic>(new
            {
                total = count,
                page,
                pageSize,
                posts
            }));
        }
        catch
        {
            return StatusCode(500, new ResultViewModel<List<Category>>("05X04 - Falha interna no servidor"));
        }
    }

    [HttpGet("v1/posts/{id:int}")]
    public async Task<IActionResult> DetailsAsync(
        [FromServices] BlogDataContext context,
        [FromRoute] int id)
    {
        try
        {
            var post = await context
                .Posts
                .AsNoTracking()
                .Include(x => x.Author)
                .ThenInclude(x => x.Roles)
                .Include(x => x.Category)
                .FirstOrDefaultAsync(x => x.Id == id);

            if (post == null)
                return NotFound(new ResultViewModel<Post>("Conteúdo não encontrado"));

            return Ok(new ResultViewModel<Post>(post));
        }
        catch (Exception ex)
        {
            return StatusCode(500, new ResultViewModel<List<Category>>("05X04 - Falha interna no servidor"));
        }
    }

    [HttpGet("v1/posts/category/{category}")]
    public async Task<IActionResult> GetByCategoryAsync(
        [FromRoute] string category,
        [FromServices] BlogDataContext context,
        [FromQuery] int page = 0,
        [FromQuery] int pageSize = 25)
    {
        try
        {
            var count = await context.Posts.AsNoTracking().CountAsync();
            var posts = await context
                .Posts
                .AsNoTracking()
                .Include(x => x.Author)
                .Include(x => x.Category)
                .Where(x => x.Category.Slug == category)
                .Select(x => new ListPostsViewModel
                {
                    Id = x.Id,
                    Title = x.Title,
                    Slug = x.Slug,
                    LastUpdateDate = x.LastUpdateDate,
                    Category = x.Category.Name,
                    Author = $"{x.Author.Name} ({x.Author.Email})"
                })
                .Skip(page * pageSize)
                .Take(pageSize)
                .OrderByDescending(x => x.LastUpdateDate)
                .ToListAsync();
            return Ok(new ResultViewModel<dynamic>(new
            {
                total = count,
                page,
                pageSize,
                posts
            }));
        }
        catch
        {
            return StatusCode(500, new ResultViewModel<List<Category>>("05X04 - Falha interna no servidor"));
        }
    }
}
```

foi criado essa classe para receber as propriedades 

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2074.png)

```csharp
namespace Blog.ViewModels.Posts;

public class ListPostsViewModel
{
    public int Id { get; set; }
    public string Title { get; set; }
    public string Slug { get; set; }
    public DateTime LastUpdateDate { get; set; }
    public string Category { get; set; }
    public string Author { get; set; }
}
```

---

# Alterando a serialização padrão do asp.net

comentei uma parte do código para desativar o select 

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2075.png)

depois colocamos esse codigo no program.cs para que ele nao desse erro de serialização no json do postman

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2076.png)

mas como podemos ver venho muitos dados e de forma bagunçada

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2077.png)

ativei o select do código novamente e coloquei um jsonIgnore para não mostrar a senha

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2078.png)

resultado com select 

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2079.png)

---

# Paginação de dados

essa parte é a paginação de dados para controlar a quantidades de dados que vai ser mostrado no json, pois ele estava mostrando todos os dados, agora ele so pega 25 dados diferentes divididos no Json

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2080.png)

aqui ele pega os dados pulando de 25 para 25, por ordem decrescente e no lastUpdateDate pegando os dados mais atuais 

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2081.png)

fazendo um count nos dados 

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2082.png)

mostrar tudo isso no json para ajuda o front end

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2083.png)

---

# Filtrando Dados

na parte de baixo do Post {int} para baixo foi feito toda a filtragem de dados pode ver que ele segue o padrao das outras partes de cima

```csharp
using Blog.Data;
using Blog.Models;
using Blog.ViewModels;
using Blog.ViewModels.Posts;
using Microsoft.AspNetCore.Mvc;
using Microsoft.EntityFrameworkCore;

namespace Blog.Controllers;

[ApiController]
public class PostController : ControllerBase
{
    [HttpGet("v1/posts")]
    public async Task<IActionResult> GetAsync(
        [FromServices] BlogDataContext context,
        [FromQuery] int page = 0,
        [FromQuery] int pageSize = 25)
    {
        try
        {
            var count = await context.Posts.AsNoTracking().CountAsync();
            var posts = await context
                .Posts
                .AsNoTracking()
                .Include(x => x.Author)
                .Include(x => x.Category)
                .Select(x => new ListPostsViewModel
                {
                    Id = x.Id,
                    Title = x.Title,
                    Slug = x.Slug,
                    LastUpdateDate = x.LastUpdateDate,
                    Category = x.Category.Name,
                    Author = $"{x.Author.Name} ({x.Author.Email})"
                })
                .Skip(page * pageSize)
                .Take(pageSize)
                .OrderByDescending(x => x.LastUpdateDate)
                .ToListAsync();
            return Ok(new ResultViewModel<dynamic>(new
            {
                total = count,
                page,
                pageSize,
                posts
            }));
        }
        catch
        {
            return StatusCode(500, new ResultViewModel<List<Category>>("05X04 - Falha interna no servidor"));
        }
    }

    [HttpGet("v1/posts/{id:int}")]   // se não passar um inteiro ele nao vai funcionar
    public async Task<IActionResult> DetailsAsync(
        [FromServices] BlogDataContext context,
        [FromRoute] int id)
    {
        try
        {
            var post = await context
                .Posts
                .AsNoTracking()
                .Include(x => x.Author)
                .ThenInclude(x => x.Roles)
                .Include(x => x.Category)
                .FirstOrDefaultAsync(x => x.Id == id);

            if (post == null)
                return NotFound(new ResultViewModel<Post>("Conteúdo não encontrado"));

            return Ok(new ResultViewModel<Post>(post));
        }
        catch (Exception ex)
        {
            return StatusCode(500, new ResultViewModel<List<Post>>("05X04 - Falha interna no servidor"));
        }
    }

    [HttpGet("v1/posts/category/{category}")]
    public async Task<IActionResult> GetByCategoryAsync(
        [FromRoute] string category,
        [FromServices] BlogDataContext context,
        [FromQuery] int page = 0,
        [FromQuery] int pageSize = 25)
    {
        try
        {
            var count = await context.Posts.AsNoTracking().CountAsync();
            var posts = await context
                .Posts
                .AsNoTracking()
                .Include(x => x.Author)
                .Include(x => x.Category)
                .Where(x => x.Category.Slug == category)
                .Select(x => new ListPostsViewModel
                {
                    Id = x.Id,
                    Title = x.Title,
                    Slug = x.Slug,
                    LastUpdateDate = x.LastUpdateDate,                   // sem esse select ele da erro de serialização, quando vem muitos dados de uma vez só
                    Category = x.Category.Name,
                    Author = $"{x.Author.Name} ({x.Author.Email})"
                })
                .Skip(page * pageSize)
                .Take(pageSize)
                .OrderByDescending(x => x.LastUpdateDate)
                .ToListAsync();
            return Ok(new ResultViewModel<dynamic>(new
            {
                total = count,
                page,
                pageSize,
                posts
            }));
        }
        catch
        {
            return StatusCode(500, new ResultViewModel<List<Category>>("05X04 - Falha interna no servidor"));
        }
    }
}
```

pode ver que coloquei o id do post e funcionou normalmente

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2084.png)

e aqui eu filtrei os dados da categoria backend e pegou todos os dados

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2085.png)

---

# Cache

uma das coisas que me impressionou foi a memoria cache, podemos desenvolver de acordo com esses códigos e a requisição fica muito rapida

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2086.png)

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2087.png)

tempo da primeira requisição 2,91s

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2088.png)

tempo da segunda requisição 13ms, incrivel 

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2089.png)

---

# Compressão

foi adicionado esse codigo no program.cs para comprimir os dados e enviar para o frontEnd

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2090.png)

no resultado do postMan não deu diferença nos bytes, pois o arquivo é muito pequeno e o zip não conseguiu fazer a compressão dos dados 

mas podemos ver nos headers que ele ativou o zip para comprimir

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2091.png)

---

# Configurações de Debug e ambiente Dev e Prod

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2092.png)

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2093.png)

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2094.png)

ele da um retorno mostrando que estamos no ambiente de desenvolvimento

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2095.png)

---

# Usando o modo release

para gerar o modo release segue o código

```csharp
dotnet build -c release
```

depois abrir a pasta usando o seguinte codigo

```csharp
ii .
```

essa pasta do modo release é gerada depois de debugada na ide, ele é bem mais otimizado e depois é enviado para area de produção.

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2096.png)

foi executado o projeto 

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2097.png)

podemos ver que agora ele rodou a parte em produção, na porta 5000 ou 5001 normalmente para ambientes para produção

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2098.png)

digite o host manualmente para verificar a resposta e tudo certo

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%2099.png)

---

# Entendendo o lauchSettings

o lauchSettings tem basicamente as configurações do projeto e do servidor IIS express

quando o lauchSettings não é configurado pelo DEV ele abre por padrao o [localhost](http://localhost) 5000 ou 5001, o próprio aspnet é inteligente suficiente para indentificar

---

# Isdevelopment

colocado uma condição se ele estiver no ambiente de desenvolvimento gerar a msg

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%20100.png)

nessa segunda imagem como ele não esta no ambiente de produção ai nao gerou nada.

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%20101.png)

---

# Forçando o HTTPS

essa parte do código força o visual studio a gerar um certificado de segurança antes de executar toda a aplicação

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%20102.png)

---

# ConnectionStrings

ele passou uma forma diferente de conectar no banco, mas estou utilizando agora o docker composite, que ja deixar toda a conexão conectada automaticamente

---

# OpenAPi

foi colocado esses codigo marcado para que o código funcionasse em swagger

![Untitled](ASP%20NET%2042d7ca21dd4449379dea52df80a7f0e5/Untitled%20103.png)
