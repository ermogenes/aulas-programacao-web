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
