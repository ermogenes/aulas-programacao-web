# HTTP e REST

📽 Veja esta aula no YouTube:
* [📺 Parte 1 - Introdução](https://youtu.be/TOxRXH7ACiE)
* [📺 Parte 2 - Estrutura da aplicação](https://youtu.be/woUBgzJnt48)
* [📺 Parte 3 - GET (listagem e filtro)](https://youtu.be/lXisL_k4KC4)
* [📺 Parte 4 - GET (item único)](https://youtu.be/Jv5_CmRHHCA)
* [📺 Parte 5 - DELETE](https://youtu.be/TFNS8nQA3Ww)
* [📺 Parte 6 - POST](https://youtu.be/y0K7rNNExWE)
* [📺 Parte 7 - PUT](https://youtu.be/VJIu6kv8hNg)
* [📺 Parte 8 - PATCH](https://youtu.be/sxWqJir3hjU)

O [HTTP (Hypertext Transfer Protocol)](https://developer.mozilla.org/pt-BR/docs/Web/HTTP) é o protocolo de comunicação sobre o qual a web funciona. Com ele navegadores, servidores, aplicativos _mobile_ e qualquer outro tipo de aplicação podem trocar informações de maneira simples e direta.

Por exemplo, quando você quer acessar um _site_, você digita seu endereço (ou URL) em um navegador (cliente HTTP) e ele envia seu pedido (GET) para o servidor indicado na URL, que responde e esse resultado é exibido pelo navegador. Porém, HTTP é muito mais que isso, suportando muitos tipos de tráfego de informação.

Uma requisição (_request_) usa um método (_method_) ou verbo que indica a ação desejada e aponta para um URL (com um caminho de recurso, em um servidor). Pode conter um conjunto de cabeçalhos (_headers_) com a configuração da comunicação, e um corpo com informações adicionais. A resposta (_response_) possui um código de status indicando o sucesso/fracasso da comunicação, cabeçalhos opcionais, e o corpo da mensagem contendo o conteúdo requisitado.

## HTTP Status Codes

Os códigos de status seguem uma tabela numérica, com o seguinte agrupamento:

* Respostas de informação (100-199)
* Respostas de sucesso (200-299)
* Redirecionamentos (300-399)
* Erros do cliente (400-499)
* Erros do servidor (500-599)

Por exemplo:
* `200 OK` caso a solicitação seja válida e o resultado seja enviado com sucesso
* `404 NOT FOUND` caso o recurso não exista
* `400 BAD REQUEST` caso a solicitação seja inválida (por erro do cliente)
* `500 INTERNAL SERVER ERROR` caso ocorra um problema (por erro do servidor)

Veja uma tabela completa [aqui](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Status). Veja também [🐱 aqui](https://www.flickr.com/photos/girliemac/sets/72157628409467125) e [🐶 aqui](https://httpstatusdogs.com/).

## Clientes HTTP

Usamos clientes HTTP toda vez que fazemos uma requisição a um servidor usando esse protocolo. O tipo mais conhecido é o navegador (_browser_), mas ele tem um comportamento com finalidade específica, e não serve para tudo que precisamos como desenvolvedor. Podemos fazer nossas chamadas manualmente com JavaScript usando Fetch, mas isso não é nada prático para testar as nossas comunicações com os backends.

Caso seja necessário baixe um cliente HTTP dedicado para desenvolvedores chamado [Insomnia](https://insomnia.rest/). Com ele podemos entender em detalhes o que acontece na comunicação. Baixe-o e instale-o acessando [https://insomnia.rest/download/](https://insomnia.rest/download/), opção _Insomnia Core_. Outra opção bastante utilizada é o [Postman](https://www.postman.com/downloads/).

## REST

Existe um estilo de arquitetura de sistemas criado para utilizar todo o potencial do protocolo HTTP chamado [REST (REpresentational State Transfer)](https://restfulapi.net/). Ele é muito popular hoje em dia e o utilizaremos neste material.

O REST define regras e boas práticas para uso de HTTP em aplicações. Vejamos como usar os verbos, cabeçalhos, status e corpo das mensagens para integrar aplicações.

### GET

Obtém do servidor um recurso único ou uma lista de recursos. Usado para buscar imagens ou arquivos HTML, e também objetos JSON com informações do backend.

Exemplos:
* `GET /Alunos` para buscar uma lista de alunos.
* `GET /Alunos/98765` para buscar um aluno específico.

Resultados comuns:
* `200 OK` indica sucesso, com o resultado no corpo da mensagem (que pode ser vazio no caso da lista).
* `404 NOT FOUND` em caso de não encontrar o recurso (único) solicitado.

Observações:
* Use _query string_ para realizar filtros, ordenação e paginação. Esses parâmetros não são automáticos e devem ser tratados pelo backend um a um. Exemplos:
  * `GET /Alunos?nome=Fabi` para filtrar a lista de alunos pelo nome.
  * `GET /Alunos?ordem=idade` para colocar em ordem de idade.
  * `GET /Alunos?inicio=11&quantidade=10` para colocar acessar a segunda página de 10 itens cada.

### POST

Cria um recurso em uma lista de recursos. Os dados a serem cadastrados vão no corpo da requisição.

Exemplo:
* `POST /Alunos` para incluir um novo aluno na lista de alunos. Os dados a serem cadastrados devem ir no corpo da mensagem.

Resultados comuns:
* `200 OK` caso o recurso seja criado e não possua URL próprio.
* `201 CREATED` caso o recurso seja criado e possua URL próprio. Nesse caso, o recurso criado volta no corpo da mensagem, e o seu URL no _header_ `Location`.
* `400 BAD REQUEST` caso a solicitação seja inválida.

### PUT

Substitui (altera) um recurso por inteiro. Deve ser chamado referenciando um recurso existente (como em `GET`) e enviando os novos dados no corpo da mensagem (como em `POST`).

Exemplos:
* `PUT /Alunos/98765` para alterar todos os dados de um aluno específico. Os novos dados a serem gravados devem ir no corpo da mensagem.

Resultados comuns:
* `200 OK` indica sucesso, com o resultado (recurso alterado) no corpo da mensagem.
* `404 NOT FOUND` em caso de não encontrar o recurso solicitado.
* `400 BAD REQUEST` caso a solicitação seja inválida.

### PATCH

Altera/corrige parte de um registro.

Exemplos:
* Não há um consenso sobre a maneira correta de utilizar esse método. De maneira geral, é executado sobre um recurso único (com em `PATCH /Alunos/98765`), porém a maneira que os dados são recebidos e retornados é ajustado caso a caso.

Resultados comuns:
* `200 OK` indica sucesso.
* `404 NOT FOUND` em caso de não encontrar o recurso solicitado.
* `400 BAD REQUEST` caso a solicitação seja inválida.

### DELETE

Exclui um recurso.

Exemplos:
* `DELETE /Alunos/98765` para excluir um aluno específico.

Resultados comuns:
* `200 OK` indica sucesso, com o corpo da mensagem vazio.
* `404 NOT FOUND` em caso de não encontrar o recurso solicitado.

## Exemplo de aplicação usado na aula

Vamos utilizar o banco de dados `top5` contido [aqui](https://github.com/ermogenes/top5-mysql). Siga as instruções para criá-lo na sua máquina.

Inicie seu projeto `webapi` chamando `top5`, faça o _scaffolding_ do banco e configure a aplicação para ler a _string de conexão_ do arquivo _appsettings.json_ e injetar o contexto. Todos esses passos estão [nesta aula](https://github.com/ermogenes/aulas-programacao-web/blob/master/content/bd-nuvem.md).

Vamos agora implementar nossa(s) _controller(s)_. Se preferir acompanhar vendo o programa pronto, ele está disponível [aqui](#código-completo).

## Backend - Implementação das _controllers_

Vamos usar as recomendações REST para criar nossas _controllers_ de API. Primeiramente, vamos criar a classe e prepará-la para obter o contexto do mecanismo de injeção de dependência.

Crie `Controllers\TopsController.cs` com o namespace `top5.Controllers`. Já adicione as referências utilizadas nessa aula. Configure-a a sua rota para que ela atenda a `/api/Tops`.

Você deverá ter algo como isto:

```cs
using System;
using Microsoft.AspNetCore.Mvc;
using Microsoft.EntityFrameworkCore;
using System.Collections.Generic;
using System.Linq;
using top5.db;

namespace top5.Controllers
{
    [ApiController]
    [Route("api/[controller]")]
    public class TopsController : ControllerBase
    {
        private readonly top5Context _db;

        public TopsController(top5Context contexto)
        {
            _db = contexto;
        }
    }
}
```

Observações:

* `[Route("api/[controller]")]` define um padrão `api/Tops` para todas as rotas atendidas por essa classe.
* `private readonly top5Context _db` é uma maneira elegante de disponibilizar o contexto a todos os métodos da classe. Tem o mesmo uso que `private top5Context _db { get; set; }`.

Feito isso, podemos começar a programar nossos métodos para responder às chamadas dos clientes REST nos _endpoints_ desejados.

Neste exemplo, optamos por criar _models_ somente quando necessário, usando as classes do Entity Framework quando possível.

### Obtendo vários registros (listagens)

Precisamos de um _endpoint_ para obter os nossos tops. Ela deve retornar uma lista de tops com todos os dados pertinentes.

Vamos atender a chamadas GET, e retornar um arranjo de objetos com todos os tops encontrados (ou uma lista vazia caso não exista nenhum). Vamos usar o código de retorno `200 OK`.

```cs
// O método atende a GET /api/Tops
[HttpGet]
public ActionResult<List<Top>> ObtemTops()
{
    // Traz todos os tops do banco de dados
    var tops = _db.Top.ToList<Top>();

    // Retorna 200 OK com o resultado no corpo da mensagem
    return Ok(tops);
}
```

* `[HttpGet]` indica que responderá ao verbo GET.
* Ao retornar um `ActionResult<...>` podemos indicar o status HTTP da resposta.
* `return Ok(tops)` indica um resultado `200 OK`, com a lista `tops` convertida em JSON no corpo da mensagem.

Exemplo: `GET /api/Tops`

Caso não possua nenhum registro:

`200 OK`
```json
[]
```

Caso possua registros:

`200 OK`
```json
[
  {
    "id": "31319dcf-d281-4f92-a834-8aa166be2a9c",
    "titulo": "Pratos Japoneses",
    "curtidas": 0,
    "item": []
  },
  {
    "id": "eaf375a4-59e6-40c4-8ce3-2b58820b74f4",
    "titulo": "Linguagens de Programação",
    "curtidas": 0,
    "item": []
  }
]
```

#### Incluindo os dados dos itens

Podemos fazer os `Include`s necessários para retornar objetos com múltiplos níveis no JSON.

```cs
var tops = _db.Top
    .Include(top => top.Item)
    .ToList<Top>();
```

Quando executamos, porém, nossa aplicação quebra e retorna a seguinte mensagem:

`500 INTERNAL SERVER ERROR`
```
System.Text.Json.JsonException: A possible object cycle was detected which is not supported. This can either be due to a cycle or if the object depth is larger than the maximum allowed depth of 32.
```

Isso se deve à referência circular existente entre tops (em Top.Item) e itens (em Item.Top). A biblioteca de conversão para JSON usada pelo ASP.NET não suporta essa situação por padrão. Devemos ativá-la.

Vamos instalar o pacote `Microsoft.AspNetCore.Mvc.NewtonsoftJson`:

```
dotnet add package Microsoft.AspNetCore.Mvc.NewtonsoftJson
```

E trocar, em `ConfigureServices` no arquivo `Startup.cs` o comando...

```cs
services.AddControllers();
```

... por...

```cs
services.AddControllers().AddNewtonsoftJson(options =>
    options.SerializerSettings.ReferenceLoopHandling = Newtonsoft.Json.ReferenceLoopHandling.Ignore
);
```

Agora ele ignora essa situação e funciona como esperado.

`200 OK`
```json
[
  {
    "id": "31319dcf-d281-4f92-a834-8aa166be2a9c",
    "titulo": "Pratos Japoneses",
    "curtidas": 0,
    "item": [
      {
        "topId": "31319dcf-d281-4f92-a834-8aa166be2a9c",
        "posicao": 1,
        "nome": "Temaki",
        "curtidas": 0
      },
      {
        "topId": "31319dcf-d281-4f92-a834-8aa166be2a9c",
        "posicao": 2,
        "nome": "Oniguiri",
        "curtidas": 0
      },
      {
        "topId": "31319dcf-d281-4f92-a834-8aa166be2a9c",
        "posicao": 3,
        "nome": "Sashimi",
        "curtidas": 0
      },
      {
        "topId": "31319dcf-d281-4f92-a834-8aa166be2a9c",
        "posicao": 4,
        "nome": "Tempura",
        "curtidas": 0
      },
      {
        "topId": "31319dcf-d281-4f92-a834-8aa166be2a9c",
        "posicao": 5,
        "nome": "Uramaki",
        "curtidas": 0
      }
    ]
  },
  {
    "id": "eaf375a4-59e6-40c4-8ce3-2b58820b74f4",
    "titulo": "Linguagens de Programação",
    "curtidas": 0,
    "item": [
      {
        "topId": "eaf375a4-59e6-40c4-8ce3-2b58820b74f4",
        "posicao": 1,
        "nome": "C#",
        "curtidas": 0
      },
      {
        "topId": "eaf375a4-59e6-40c4-8ce3-2b58820b74f4",
        "posicao": 2,
        "nome": "JavaScript",
        "curtidas": 0
      },
      {
        "topId": "eaf375a4-59e6-40c4-8ce3-2b58820b74f4",
        "posicao": 3,
        "nome": "Python",
        "curtidas": 0
      },
      {
        "topId": "eaf375a4-59e6-40c4-8ce3-2b58820b74f4",
        "posicao": 4,
        "nome": "Scala",
        "curtidas": 0
      },
      {
        "topId": "eaf375a4-59e6-40c4-8ce3-2b58820b74f4",
        "posicao": 5,
        "nome": "Elixir",
        "curtidas": 0
      }
    ]
  }
]
```

#### Adicionando filtro

Queremos que nossa listagem de tops possa ser filtrada pelo seu título, exibindo somente os títulos que contenham um texto indicado pelo usuário. Parâmetros desse tipo devem ser enviado na URL no formato chamado de _query string_.

Ela vai após a rota iniciada por um `?` e formada por pares de chave e valor separadas por `&`.

Formato: `?chave1=valor1&chave2=valor2&chave3=valor3`...

Exemplo: `GET /api/Tops?titulo=jap`, indicando que o parâmetro `titulo` possui o valor `jap`.

Vamos usar isso para filtrar nossos tops.

```cs
// ...
public ActionResult<List<Top>> ObtemTops(string titulo) // Argumento
{
// ...
    var tops = _db.Top
        .Include(top => top.Item)
        .Where(top => top.Titulo.Contains(titulo)) // Filtro
        .ToList<Top>();
// ...
}
```

* `ObtemTops(string titulo)` indica que esse método possui um argumento chamado `titulo` que receberá o parâmetro de mesmo nome enviado pelo cliente.

Fazendo `GET /api/Tops?titulo=jap`, temos uma lista com um único resultado:

`200 OK`
```json
[
  {
    "id": "31319dcf-d281-4f92-a834-8aa166be2a9c",
    "titulo": "Pratos Japoneses",
    "curtidas": 0,
    "item": [...]
  }
]
```

Fazendo `GET /api/Tops?titulo=X`, temos uma lista vazia:

`200 OK`
```json
[]
```

Fazendo `GET /api/Tops?titulo=a`, temos uma lista com vários resultados:

`200 OK`
```json
[
  {
    "id": "31319dcf-d281-4f92-a834-8aa166be2a9c",
    "titulo": "Pratos Japoneses",
    "curtidas": 0,
    "item": [...]
  },
  {
    "id": "eaf375a4-59e6-40c4-8ce3-2b58820b74f4",
    "titulo": "Linguagens de Programação",
    "curtidas": 0,
    "item": [...]
  }
]
```

O problema é que uma chamada sem nenhum filtro retornará uma lista vazia, pois nenhum top possui título vazio. Precisamos torná-lo um argumento opcional.

#### Filtro opcional

Fazemos com que cada linha do banco seja incluída no resultado se não houver filtro ou se ela contiver o valor do filtro.

```cs
var tops = _db.Top
    .Include(top => top.Item)
    .Where(top => String.IsNullOrEmpty(titulo) || top.Titulo.Contains(titulo))
    .ToList<Top>();
```

* `String.IsNullOrEmpty(variavelString)` retorna `true` somente se `variavelString` for vazia (`""`) ou nula.

## Código final

```cs
// GET api/Tops
// GET api/Tops?titulo=valorDesejado
[HttpGet]
public ActionResult<List<Top>> ObtemTops(string titulo)
{
    // Obtém todos os tops que contém o título indicado
    // ou todos, se não for indicado nenhum
    var tops = _db.Top
        .Include(top => top.Item) // ver ***
        .Where(top => String.IsNullOrEmpty(titulo) || top.Titulo.Contains(titulo))
        .ToList<Top>();

    // 200 OK
    return Ok(tops);
}
```

### Consulta a um registro único

Precisamos de um _endpoint_ que retorne os dados de um registro único, caso já tenhamos o seu identificador. Para isso, passaremos o `id` do top diretamente na rota solicitada. Só temos que indicar que o novo método que atenderá a rota saiba em que ponto da URL estará o valor do parâmetro.

Queremos atender a algo do tipo `GET /api/Tops/identificador-do-registro`.

Nesse caso, precisamos responder `404 NOT FOUND` quando o registro não for encontrado.

```cs
// GET api/Tops/id-top-desejado
[HttpGet("{id}")]
public ActionResult<Top> ObtemTop(string id)
{
    // Obtém um top que possua o id indicado
    var top = _db.Top
        .Include(top => top.Item)
        .SingleOrDefault(top => top.Id == id);

    if (top == null)
    {
        // 404 NOT FOUND
        return NotFound();
    }

    // 200 OK
    return Ok(top);
}
```

* `[HttpGet("{id}")]` e `ObtemTop(string id)` indicam que o valor indicado no final da rota será mapeado para o parâmetro `id`.
* `ActionResult<Top>` indica o retorno de um objeto único, e não uma lista.
* `.SingleOrDefault(top => top.Id == id)` filtra nossa lista pelo `Id` retornando um registro único ou então `null`.
* `return NotFound()` produz `404 NOT FOUND`.

Exemplo: `GET /api/Tops/31319dcf-d281-4f92-a834-8aa166be2a9c`

Caso não possua nenhum registro com esse `id`:

`404 NOT FOUND` (sem corpo de mensagem)

Caso possua o registro:

`200 OK`
```json
{
  "id": "31319dcf-d281-4f92-a834-8aa166be2a9c",
  "titulo": "Pratos Japoneses",
  "curtidas": 0,
  "item": [
    {
      "topId": "31319dcf-d281-4f92-a834-8aa166be2a9c",
      "posicao": 1,
      "nome": "Temaki",
      "curtidas": 0
    },
    {
      "topId": "31319dcf-d281-4f92-a834-8aa166be2a9c",
      "posicao": 2,
      "nome": "Oniguiri",
      "curtidas": 0
    },
    {
      "topId": "31319dcf-d281-4f92-a834-8aa166be2a9c",
      "posicao": 3,
      "nome": "Sashimi",
      "curtidas": 0
    },
    {
      "topId": "31319dcf-d281-4f92-a834-8aa166be2a9c",
      "posicao": 4,
      "nome": "Tempura",
      "curtidas": 0
    },
    {
      "topId": "31319dcf-d281-4f92-a834-8aa166be2a9c",
      "posicao": 5,
      "nome": "Uramaki",
      "curtidas": 0
    }
  ]
}
```

## Incluindo um registro

Esse _endpoint_ usará o método POST para receber os dados a serem cadastrados através do corpo da mensagem (um objeto JSON).

O procedimento de inclusão exige alguns passos:
* validar os dados recebidos;
* incluir o registro no banco de dados com um `id` gerado pela aplicação;
* retornar o objeto criado no corpo da mensagem;
* retornar o URL do objeto criado no _header_ `Location`.

Vamos primeiro criar um método de validação que será usado para a inclusão e para a alteração. Ele receberá um `Top` e retornará uma _string_ descrevendo o erro, ou então uma _string_ vazia caso não encontre erro. _Perceba que o método é privado, e não responde a nenhum método/rota. Ele não pode ser chamado pela nossa API, somente pela nossa aplicação._

```cs
private string ValidaTop(Top topAValidar)
{
    if (String.IsNullOrEmpty(topAValidar.Titulo))
    {
        return "Título não informado.";
    }

    if (topAValidar.Curtidas < 0)
    {
        return "Curtidas devem ser positivas.";
    }

    if (topAValidar.Item.Count() != 5)
    {
        return "São esperados exatos 5 itens.";
    }

    int posicaoEsperada = 1;
    foreach(var item in topAValidar.Item.OrderBy(i => i.Posicao))
    {
        if (item.Posicao != posicaoEsperada)
        {
            return $"Não foi informado item {posicaoEsperada}.";
        }

        if (String.IsNullOrEmpty(item.Nome))
        {
            return $"Não foi informado o nome do item {item.Posicao}.";
        }

        if (item.Curtidas < 0)
        {
            return $"Curtidas do item {item.Posicao} devem ser positivas.";
        }

        posicaoEsperada++;
    }

    return "";
}
```

Usaremos esse método para verificar a consistência do registro. Abaixo, o código completo.

```cs
// POST api/Tops
// body: objeto do tipo Top
[HttpPost]
public ActionResult<Top> IncluiTop(Top topInformado)
{
    if (topInformado.Id != null)
    {
        // 400 BAD REQUEST
        return BadRequest(new { mensagem = "Id não pode ser informado." });
    }

    // Validação
    var mensagemErro = ValidaTop(topInformado);

    if (!String.IsNullOrEmpty(mensagemErro))
    {
        // 400 BAD REQUEST
        return BadRequest(new { mensagem = mensagemErro });
    }

    // Gera novo identificador único
    topInformado.Id = Guid.NewGuid().ToString();

    // Salva o novo registro
    _db.Add(topInformado);
    _db.SaveChanges();

    // 201 CREATED
    // Location: url do novo registro
    return CreatedAtAction(nameof(ObtemTop), new { id = topInformado.Id }, topInformado);
}
```

* ` [HttpPost]` indica que reponderá a chamadas POST.
* `IncluiTop(Top topInformado)` indica que o conteúdo JSON do corpo da requisição será convertido em um objeto do tipo `Top` com o nome `topInformado`.
* `return BadRequest()` indica um retorno de status `400 BAD REQUEST` vazio. Ao adicionar um objeto no retorno, ele será enviado no corpo da resposta. `new { mensagem = mensagemErro }` indica um objeto anônimo (sem tipo definido), contendo a mensagem de erro.
* `Guid.NewGuid().ToString()` gera uma _string_ de 36 posições no formato [GUID](https://en.wikipedia.org/wiki/Universally_unique_identifier).
* `return CreatedAtAction(ação, parâmetros, corpo)` indica um retorno `201 CREATED`, com o _header_ `Location` preenchido com a URL do recurso criado (uma _string_ dizendo a rota necessária para acessar _ação_ com os valores de `parâmetros`).

Exemplo: `POST /api/Tops`, contendo no corpo da requisição:

```json
{
  "titulo": "Viagens mais desejadas",
  "curtidas": 5,
  "item": [
    {
      "posicao": 1,
      "nome": "Londres"
    },
    {
      "posicao": 3,
      "nome": "Paris"
    },
    {
      "posicao": 4,
      "nome": "Santiago"
    },
    {
      "posicao": 5,
      "nome": "Gramado"
    },
    {
      "posicao": 2,
      "nome": "Nova Iorque"
    }
  ]
}
```

Registro criado com sucesso:

`201 CREATED`

_header_: `Location	https://localhost:5001/api/Tops/b23366ff-bc4b-4f09-a75b-f07045322a1e`
```json
{
  "id": "b23366ff-bc4b-4f09-a75b-f07045322a1e",
  "titulo": "Viagens mais desejadas",
  "curtidas": 5,
  "item": [
    {
      "topId": "b23366ff-bc4b-4f09-a75b-f07045322a1e",
      "posicao": 1,
      "nome": "Londres",
      "curtidas": 0
    },
    {
      "topId": "b23366ff-bc4b-4f09-a75b-f07045322a1e",
      "posicao": 3,
      "nome": "Paris",
      "curtidas": 0
    },
    {
      "topId": "b23366ff-bc4b-4f09-a75b-f07045322a1e",
      "posicao": 4,
      "nome": "Santiago",
      "curtidas": 0
    },
    {
      "topId": "b23366ff-bc4b-4f09-a75b-f07045322a1e",
      "posicao": 5,
      "nome": "Gramado",
      "curtidas": 0
    },
    {
      "topId": "b23366ff-bc4b-4f09-a75b-f07045322a1e",
      "posicao": 2,
      "nome": "Nova Iorque",
      "curtidas": 0
    }
  ]
}
```

Dados inválidos (com -5 curtidas):

`400 BAD REQUEST`

```json
{
  "mensagem": "Curtidas devem ser positivas."
}
```

## Alterando um registro (por inteiro) 

Para alterar os dados de um registro, precisamos de um _endpoint_ que aponte para um registro (como em GET) e receba os novos dados a serem gravados (como em POST).

O método usado é PUT, com o registro a ser alterado indicado na rota e os dados recebidos via corpo da mensagem. Retornará `200 OK` caso o registro esteja correto, `400 BAD REQUEST` para registros inválidos e `404 NOT FOUND` caso o registro solicitado não exista.

```cs
// PUT api/Tops/id-top-desejado
// body: objeto do tipo Top
[HttpPut("{id}")]
public ActionResult<Top> AlteraTop(string id, Top topAlterado)
{
    if (topAlterado.Id != id)
    {
        // 400 BAD REQUEST
        return BadRequest(new { mensagem = "Id inconsistente." });
    }

    // Obtém um top que possua o id indicado
    var top = _db.Top
        .Include(top => top.Item) // ver ***
        .SingleOrDefault(top => top.Id == id);

    if (top == null)
    {
        // 404 NOT FOUND
        return NotFound();
    }

    // Validação
    var mensagemErro = ValidaTop(topAlterado);

    if (!String.IsNullOrEmpty(mensagemErro))
    {
        // 400 BAD REQUEST
        return BadRequest(new { mensagem = mensagemErro });
    }

    // Altera para os novos valores
    top.Titulo = topAlterado.Titulo;
    for(int posicao = 1; posicao <=5; posicao++)
    {
        string nomeAlterado = topAlterado.Item
            .SingleOrDefault(i => i.Posicao == posicao)
            .Nome;
        top.Item
            .SingleOrDefault(i => i.Posicao == posicao)
            .Nome = nomeAlterado;
    }
    _db.SaveChanges();

    // 200 OK
    return Ok(top);
}
```

* `[HttpPut("{id}")]` e `AlteraTop(string id, Top topAlterado)` indicam os parâmetros `id` (na rota) e `topAlterado` (no corpo da mensagem).

## Alterando parte de um registro

Quando necessitamos alterar ou corrigir somente parte de um registro, como em uma atualização de status, ou confirmação de uma ação, não usamos PUT e sim PATCH.

O recurso é indicado na rota, bem como a ação aser executada, e os dados pertinentes, quando existentes, no corpo da requisição. Retornará `200 OK` se a ação teve sucesso, ou `400 BAD REQUEST` nos demais casos.

Neste exemplo usamos PATCH quando o usuário curte um top ou um item de top. Retornamos o novo número de curtidas no corpo da resposta, em caso de sucesso. Para esse retorno, optamos pela criação de uma classe para definição de contrato de comunicação, sendo que todos os _endpoints_ com a ação de curtir retornam o mesmo tipo de objeto (do tipo `top5.Models.CurtidasModel`). Esse tipo de objeto é frequentemente chamado _Data Transfer Object_, ou DTO.

Veja a classe Model:

```cs
namespace top5.Models
{
    public class CurtidasModel
    {
        public int Curtidas { get; set; }
    }
}
```

Os métodos agora podem utilizá-la para definir o seu tipo de retorno.

Abaixo, o método que permite curtir um top. Ele verifica a sua existência, acrescenta um no número de curtidas e retorna o valor atualizado.

```cs
// PATCH api/Tops/id-top-desejado/curtir
[HttpPatch("{id}/curtir")]
public ActionResult<CurtidasModel> CurteTop(string id)
{
    // Obtém um top que possua o id indicado
    var top = _db.Top
        .Include(top => top.Item) // ver ***
        .SingleOrDefault(top => top.Id == id);
    
    if (top == null)
    {
        // 400 BAD REQUEST
        return BadRequest();
    }

    // Acrescenta uma curtida
    top.Curtidas += 1;
    _db.SaveChanges();

    // Retorna o novo número de curtidas
    var retorno = new CurtidasModel { Curtidas = top.Curtidas };

    // 200 OK
    return Ok(retorno);
}
```

Exemplo: `PATCH http://localhost:5000/api/tops/26fdcb96-ae06-4cf8-be91-62b50d944e32/curtir`

Curtidas alteradas com sucesso:

`200 OK`, com o novo número de curtidas

```json
{
  "curtidas": 12
}
```

Nos itens, recebemos na rota além do identificador do top, também a posição a ser curtida.

```cs
// PATCH api/Tops/id-top-desejado/Itens/posicao-desejada/curtir
[HttpPatch("{id}/Itens/{posicao}/curtir")]
public ActionResult<CurtidasModel> CurteItem(string id, int posicao)
{
    // Obtém um top que possua o id indicado
    var top = _db.Top
        .Include(top => top.Item) // ver ***
        .SingleOrDefault(top => top.Id == id);
    
    if (top == null)
    {
        // 400 BAD REQUEST
        return BadRequest();
    }

    // Busca pelo item da posição indicada
    var item = top.Item.SingleOrDefault(item => item.Posicao == posicao);

    if (item == null)
    {
        // 400 BAD REQUEST
        return BadRequest();
    }

    // Acrescenta uma curtida ao item
    item.Curtidas += 1;
    _db.SaveChanges();

    // Retorna o novo número de curtidas
    var retorno = new CurtidasModel { Curtidas = item.Curtidas };

    // 200 OK
    return Ok(retorno);
}
```

Exemplo: `PATCH http://localhost:5000/api/tops/26fdcb96-ae06-4cf8-be91-62b50d944e32/itens/2/curtir`

Curtidas alteradas com sucesso:

`200 OK`, com o novo número de curtidas

```json
{
  "curtidas": 7
}
```

Top inexistente:

Exemplo (a): `PATCH http://localhost:5000/api/tops/abc123/curtir`

`400 BAD REQUEST`

Item inexistente:

Exemplo (b): `PATCH http://localhost:5000/api/tops/26fdcb96-ae06-4cf8-be91-62b50d944e32/itens/-18/curtir`

`400 BAD REQUEST`

```json
{
  "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
  "title": "Bad Request",
  "status": 400,
  "traceId": "|22f3a262-49620fc9d85708e9."
}
```

## Excluindo um registro

A implementação da exclusão é muito parecida com a da consulta a um recurso único, com duas diferenças:

* O retorno não inclui dados do recurso (no exemplo, `ActionResult<Top>` se torna somente `ActionResult`);
* É efetuada a exclusão do recurso.

```cs
// DELETE api/Tops/id-top-desejado
[HttpDelete("{id}")]
public ActionResult ExcluiTop(string id)
{
    // Obtém um top que possua o id indicado
    var top = _db.Top
        .Include(top => top.Item) // ver ***
        .SingleOrDefault(top => top.Id == id);

    if (top == null)
    {
        // 404 NOT FOUND
        return NotFound();
    }

    // Exclui todos os itens, e depois o top
    top.Item.Clear();
    _db.Remove(top);
    _db.SaveChanges();

    // 200 OK
    return Ok();
}
```

Exclusão efetuada com sucesso:

Exemplo: `DELETE http://localhost:5000/api/tops/26fdcb96-ae06-4cf8-be91-62b50d944e32`

Não encontrado:

`200 OK`

Exemplo: `DELETE http://localhost:5000/api/tops/xyz-3457686`

`404 NOT FOUND`

## Fetch de APIs REST

Precisamos agora estudar um pouco mais aprofundadamente a Fetch API para que possamos consumir o nosso backend em todas as suas nuances.

A função `fetch` pode receber um segundo parâmetro indicando as opções da requisição (_request_): `fetch(url, request)`. Esse objeto vai conter as configurações e os dados a serem enviados na requisição:

* `method` indica o método a ser utilizado, como `GET` ou `POST`.
* `headers` contém um objeto cujas propriedades serão enviadas no cabeçalho da requisição.
* `body` contém uma string ou campos de formulário enviados no corpo da requisição.

### Chamadas REST

`GET`, sem parâmetro de _query string_:

```js
// ...
fetch("/api/Tops")
// ...
```

`GET`, com parâmetro de _query string_:

```js
// ...
fetch(`/api/Tops?titulo=${tituloDesejado}`)
// ...
```

`POST`:

```js
// ...
fetch("/api/Tops", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify(novoTop),
})
// ...
```

`PUT`:

```js
// ...
fetch(`/api/Tops/${id}`, {
  method: "PUT",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify(topAlterado),
})
// ...
```

`PATCH`:

```js
// ...
fetch(`/api/Tops/${id}/Itens/${posicao}/curtir`, { method: "PATCH" })
// ...
```


`DELETE`:

```js
// ...
fetch(`/api/Tops/${id}`, { method: "DELETE" })
// ...
```

### Entendendo os resultados

Após a requisição, o objeto retornado possui todo o conteúdo da resposta.

* `.status` possui o código de status do retorno (ex.: `404`);
* `.statusText` possui a descrição textual do status de retorno (ex.: `NOT FOUND`);
* `.ok` é `true` se o resultado possui status de sucesso (entre 200 e 299, inclusive);
* `.json()` obtém um objeto JavaScript equivalente ao conteúdo JSON recebido.

Exemplo:

```js
// ...
const response = await fetch(url, requestOptions);
if (response.ok) {
  // Sucesso
  const result = await response.json();
  // ...
} else {
  // Erro
  alert(`Erro: ${response.status} - ${response.statusText}`);
}
// ...
```

## Código completo

Complemente seus estudos vendo o programa pronto e estudando seu conteúdo. Ele está disponível [aqui](https://github.com/ermogenes/top5).