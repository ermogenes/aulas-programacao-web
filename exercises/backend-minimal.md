# Exercícios: _Backend_ com Minimal APIs

Para cada exercício abaixo crie um repositório com o nome indicado contendo um projeto do tipo `web` em C#.

Adicione suporte a OpenAPI (Swagger) em todos eles.

---
## Exercício `HelloWorldAPI`

Escreva uma API com o _endpoint_ `GET /hello-world` que retorne:

`GET /hello-world --> HTTP 200 SUCCESS`
```json
{
    "mensagem": "Hello, World!"
}
```

---
## Exercício `SomaAPI`

Escreva uma API com o _endpoint_ `GET /soma`, com os parâmetros `a` e `b` na _query string_ (ex.: `/soma?a=5&b=7`). Retorne:

`GET /soma?a=5&b=7 --> HTTP 200 SUCCESS`
```json
{
    "a": 5,
    "b": 7,
    "soma": 12
}
```

---
## Exercício `DivisaoAPI`

Escreva uma API com o _endpoint_ `GET /divisao`, com os parâmetros `numerador` e `denominador` na _query string_ (ex.: `/divisao?numerador=5&denominador=7`). Retorne:

`GET /divisao?numerador=1&denominador=2 --> HTTP 200 SUCCESS`
```json
{
    "numerador": 1,
    "denominador": 2,
    "resultado": 0.5
}
```

ou então

`GET /divisao?numerador=5&denominador=0 --> HTTP 400 BAD REQUEST`
```json
{
    "mensagem": "Denominador não pode ser zero."
}
```

---
## Exercício `DadoAPI`

Escreva uma API com um _endpoint_ para rolagem de dados (aleatório).

Exemplos de chamadas:

- `GET /dado/d6` - rola um dado de 6 faces (sorteio entre 1 e 6).
- `GET /dado/d20` - rola um dado de 20 faces (sorteio entre 1 e 20).

Aceitar somente número de faces maior do que zero (retornar `HTTP 400`).

Exemplos de retorno:

`GET /dado/d12 --> HTTP 200 SUCCESS`
```json
{
  "dado": "d12",
  "rolagem": 12
}
```

`GET /dado/d12 --> HTTP 200 SUCCESS`
```json
{
  "dado": "d12",
  "rolagem": 5
}
```

`GET /dado/d0 --> HTTP 400 BAD REQUEST`

---
## Exercício `DadosAPI`

Escreva uma API com um _endpoint_ para rolagem de dados (aleatórios).

Exemplos de chamadas:

- `GET /dados/5d6` - rola 5 dados de 6 faces (sorteios entre 1 e 6).
- `GET /dados/4d20` - rola 4 dados de 20 faces (sorteios entre 1 e 20).

Aceitar somente quantidade e número de faces maiores do que zero (retornar `HTTP 400`).

Exemplos de retorno:

`GET /dados/5d6 --> HTTP 200 SUCCESS`
```json
{
  "dados": "5d6",
  "rolagens": [
    1,
    5,
    1,
    3,
    2
  ]
}
```

`GET /dados/5d6 --> HTTP 200 SUCCESS`
```json
{
  "dados": "5d6",
  "rolagens": [
    3,
    4,
    2,
    4,
    6
  ]
}
```

`GET /dados/0d20 --> HTTP 400 BAD REQUEST`

---

## 🏁 Orientações para entrega (alunos do curso presencial)

Confira no Teams o link da tarefa equivalente. Lá você postará o link dos repositórios que você criou, um para cada exercício.

**Repositório de exemplo:**
[Exercício `EtecAB` (Saída em console)](https://github.com/ermogenes/EtecAB)

Exemplo de link a ser postado: https://github.com/ermogenes/EtecAB

<!-- 

using Microsoft.AspNetCore.Mvc;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddSwaggerGen();
builder.Services.AddEndpointsApiExplorer();

var app = builder.Build();

app.UseSwagger();
app.UseSwaggerUI();

// Ex 1
app.MapGet("/hello-world", () =>
{
    return Results.Ok(new
    {
        mensagem = "Hello, World!"
    });
});

// Ex 2
app.MapGet("/soma", ([FromQuery] int a, [FromQuery] int b) =>
{
    return Results.Ok(new
    {
        a,
        b,
        soma = a + b,
    });
});

// Ex 3
app.MapGet("/divisao", ([FromQuery] int numerador, [FromQuery] int denominador) =>
{
    if (denominador == 0)
    {
        return Results.BadRequest(new
        {
            mensagem = "Denominador não pode ser zero.",
        });
    }

    return Results.Ok(new
    {
        numerador,
        denominador,
        resultado = (double)numerador / denominador,
    });
});

// Ex 4
app.MapGet("/dado/d{faces}", ([FromRoute] int faces) =>
{
    if (faces < 1){
        return Results.BadRequest();
    }

    Random gerador = new Random();

    var dado = new {
        dado = $"d{faces}",
        rolagem = gerador.Next(1, faces + 1),
    };

    return Results.Ok(dado);
});

// Ex 5
app.MapGet("/dados/{qtd}d{faces}", ([FromRoute] int qtd, [FromRoute] int faces) =>
{
    if (faces < 1 || qtd < 1){
        return Results.BadRequest();
    }

    Random gerador = new Random();

    List<int> rolagens = new();

    for (int i = 1; i <= qtd; i++)
    {
        rolagens.Add(gerador.Next(1, faces + 1));
    }

    var resultado = new {
        dados = $"{qtd}d{faces}",
        rolagens,
    };

    return Results.Ok(resultado);
});

app.Run();

 -->