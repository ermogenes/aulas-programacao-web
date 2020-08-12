# Marcação HTML

[📽 Veja esta vídeo-aula no Youtube](https://youtu.be/5-2U1Tk2rHI)

Escrevemos páginas utilizando arquivos de texto com a extensão `.html` (ou `.htm`) onde é escrito código de marcação em linguagem HTML. Na web, tudo é hipertexto: texto aumentado com imagens, sons, vídeos e outras mídias, todos conectados através de [hyper]links.

HTML é uma sigla para _**H**yper**T**ext **M**arkup **L**anguage_, linguagem de marcação de hipertexto. Com ela definimos as páginas e seus conteúdos, bem como os links entre elas.

## Como funciona o HTML

Marcações são feitas em partes do documento utilizando _tags_. Uma _tag_ é um bloco escrito entre colchetes angulares `<` e `>`, em um estilo herdado da mais abrangente linguagem XML.

Por exemplo, no texto abaixo vemos uma marcação de parágrafo, contendo um texto:

```html
<p>Não existem métodos fáceis para resolver problemas difíceis.</p>
```
Dizemos que:

- a _tag_ `p` é um elemento de parágrafo e contém o elemento de texto `Não existem ... difíceis.`;
- `<p>` é a marcação de abertura da _tag_;
- `</p>` é a marcação de fechamento da _tag_.

Elementos de texto são exibidos pelos navegadores de maneira a simplificar a leitura. Não são considerados espaços além do primeiro, nem quebras de linha. Podemos adicionar uma quebra de linha usando a _tag_ `br`:

```html
<p>
    Não existem métodos fáceis para resolver problemas difíceis.
    <br />
    René Descartes
</p>
```

- A _tag_ `br` não pode conter nenhum elemento. Quando uma _tag_ possui essa característica simplificamos a abertura/fechamento com a sintaxe `<tag />`.

Podemos escrever _tags_ aninhadas (dentro) de outras _tags_. Veja um exemplo usando a _tag_ `strong`, que denota que um trecho é importante:

```html
<p>
    <strong>Não existem métodos fáceis para resolver problemas difíceis.</strong>
    <br />
    René Descartes
</p>
```

Agora a primeira frase foi marcada como importante, e o navegador vai destacá-la em negrito. Futuramente poderemos estilizar como quisermos.

Devemos sempre fechar as _tags_ na ordem que abrimos, mantendo a árvore coesa. O seguinte exemplo **não deve ser seguido**:

```html
<p>Texto <strong>inicial, que continua...</p>
<p>... em outro</strong> parágrafo.</p>
```

_Tags_ não são _case-sensitive_, porém devemos utilizá-las sempre em letras minúsculas.

**Sempre feche as _tags_!**

Algumas _tags_ podem ter seu conteúdo modificado utilizando atributos. No exemplo abaixo:

```html
    <img src="logo.png" alt="Logotipo do Dev Web" />
```

- A _tag_ `img` indica uma imagem, e deve ser fechada na sintaxe reduzida.
- O atributo `src` indica o URL de origem da imagem, no caso um arquivo localizado na mesma pasta com o nome `logo.png`.
- O atributo `alt` indica um texto alternativo para quando a imagem não puder ser exibida.

Outro exemplo de atributo, é `border` da _tag_ `table`. Ele indica que a tabela deve ser renderizada com bordas, com a sua presença indicando um valor _booleano_ _verdadeiro_ e sua ausência, _falso_.

```html
<table border>
    ...
</table>
```

**Sempre escrevemos os valores de um atributo entre aspas duplas,** mesmo que seja um valor numérico.

### Comentários

São escritos entre `<!--` e `-->`, e podem se estender por várias linhas.

```html
    <!-- Comentário de uma linha -->
    
    <!-- Comentário de
    várias linhas -->
```

## Documento mínimo

Existem vários _templates_ de documento mínimo para uma página, e esses padrões mudam conforme a linguagem e os navegadores evoluem. Para este curso, utilizaremos o _template_ padrão do Emmet:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    
</body>
</html>
```

- `<!DOCTYPE html>` é obrigatório em todo documento, e indica que ele está escrito na versão 5 do HTML.
- A _tag_ `html` é colocada em torno do restante do documento. Nada deve ser escrito fora.
  - `lang="en"` indica aos mecanismos de busca e leitores de tela que o texto estará escrito em inglês. Para português, use `lang="pt-BR"`.
- O elemento `head` agrupa informações sobre o documento, como configurações, links a recursos externos e metadados destinados a motores de busca.
- O elemento `body` acolhe todo o conteúdo exibível do documento. É aqui que escreveremos a maioria de nossa marcação.

## `head`

As _tags_ mais comuns do cabeçalho são:

- `title` é obrigatório e contém o título de identificação do documento.
- `meta` permite realizar diversas configurações e difinições de metadados. Várias outras posuem o padrão `name` para o nome da configuração, e `content` para o seu valor.
    - `charset="UTF-8"` indica que o arquivo será escrito em UTF-8, o que nos permite usar acentuação e _emojis_, por exemplo.
    - `viewport` configura a janela do usuário. No exemplo, para usar toda a tela disponível (`width=device-width`) e manter o _zoom_ inicial em 100% (`initial-scale=1.0`).
    - `author` contém o nome do autor do documento.
    - `description` contém uma descrição da página para motores de busca.
    - `keywords` contém uma lista separada por vírgulas de palavras-chave, para motores de busca.
- `link` permite instruir o navegador a baixar outros recursos, como arquivos de estilização.
- `style` permite definir estilos válidos somente pra auma página (e não para o site todo).
- `script` permite criar códigos dinâmicos para interação com o usuário.

## Elementos do corpo do documento - `body`

Os elementos citados a seguir só devem ser utilizados dentro de `body`.

### Texto

Use `h1` ... `h6` para definir títulos em 6 níveis/sub-níveis. Exemplo:

```html
    <h1>História</h1>
    <p>...</p>
    <h2>História do Brasil</h2>
    <p>...</p>
    <h3>Guerra de Canudos</h3>
    <p>...</p>
    <h3>Diretas Já</h3>
    <p>...</p>
    <h2>História do Japão</h2>
    <p>...</p>
```

Esse código gerará uma árvore de subtítulos estruturalmente semelhante a:

- História
  - História do Brasil
    - Guerra de Canudos
    - Diretas Já
  - História do Japão

Use `p` para definir parágrafos. Parágrafos subsequentes são espaçados por uma linha por padrão. Não há tabulação, como em português.

Use `br` para quebrar uma linha forçadamente dentro de um parágrafo. `hr` faz o mesmo, e ainda traça uma linha horizontal.

💡 Use _Lorem Ipsum_ para preencher espaços de parágrafo enquanto não possui o texto final. Isso ajuda a visualizar o seu _design_. No VsCode, digite `lorem` e pressione `Tab` ou `Enter` para inserir.

#### Elementos semânticos de texto

- `strong` indica que o trecho é importante, e por padrão é renderizado em **negrito**.
- `em` indica uma ênfase no trecho, e por padrão é renderizado em _itálico_.
- `del` indica que o texto foi removido, e por padrão é renderizado ~~riscado~~.
- `sup` e `sub` indicam sobrescrito (acima, como em ² e ³) e subescrito (abaixo).

Há muito outros, mas sempre tome cuidado para não utilizá-los como formatação, e sim como indicação do seu significado.

### Imagens

Usamos a _tag_ `img`.

- `src` indica a origem da imagem, e pode ser um URL ou o caminho relativo ao arquivo.
- `alt` é obrigatório e indica um texto alternativo para quando a imagem não puder ser exibida.

Exemplo (com imagem hospedada externamente): 

```html
<img src="http://eteab.com.br/cms/wp-content/uploads/2014/07/banner_logo2.png" alt="Banner da Etec" />
```

### Links

Usamos a _tag_ `a`, com o atributo `href`.

- `href` indica o destino do link. Caso seja um arquivo não exibível (`.zip`, por exemplo), o navegador oferecerá a realização de _download_.
- `title` indica o _tooltip_ opcional (texto exibido ao parar o ponteiro do _mouse_ sobre o link).
- `target="_blank"` permite indicar que o link deverá abrir em uma nova janela.

Todo o conteúdo entre `<a ...>` e `</a>` será clicável e remeterá ao URL indicado. Pode ser texto, imagem ou qualquer outra _tag_.

Se for uma URL completa, o usuário para lá será redirecionado. Se for um nome de arquivo, ele será procurado na mesma pasta (ou no caminho relativo). Use essa característica para criar várias páginas no seu site!

Exemplo de link com imagem de um gato, que abre outra aba com site externo (página do autor da foto):

```html
    <a href="https://www.pexels.com/pt-br/@kerber" target="_blank">
        <img src="pexels-marko-blazevic-774731.jpg" alt="Imagem de um gato">
    </a>
```

### Listas

Uma lista pode ser ordenada `ol` ou não ordenada `ul`, e pode conter itens e/ou outras listas.

_Exemplo 1_:

```html
    <ol>
        <li>Senna</li>
        <li>Schumacher</li>
        <li>Prost</li>
    </ol>
```

Indica algo como:

1. Senna
1. Schumacher
1. Prost

_Exemplo 2_:

```html
    <ul>
        <li>HTML</li>
        <li>CSS</li>
        <li>JavaScript</li>
    </ul>
```

Indica algo como:

- HTML
- CSS
- JavaScript

_Exemplo 3_:

```html
    <ol>
        <li>Item numerado</li>
        <li>Item numerado</li>
        <ul>
            <li>Sub-item não numerado</li>
            <li>Sub-item não numerado</li>
            <li>Sub-item não numerado</li>
        </ul>
        <li>Item numerado</li>
    </ol>
```
Indica algo como:

1. Item numerado
1. Item numerado
   - Sub-item não numerado
   - Sub-item não numerado
   - Sub-item não numerado
1. Item numerado

### Tabelas

Veja o exemplo:

```
    <table border>
        <thead>
            <tr>
                <th>Coluna 1</th>
                <th>Coluna 2</th>
                <th>Coluna 3</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>C1 x L1</td>
                <td>C2 x L1</td>
                <td>C3 x L1</td>
            </tr>
            <tr>
                <td>C1 x L2</td>
                <td>C2 x L2</td>
                <td>C3 x L2</td>
            </tr>
            <tr>
                <td>C1 x L3</td>
                <td>C2 x L3</td>
                <td>C3 x L3</td>
            </tr>
        </tbody>
    </table>
```

- `table` indica que o conteúdo é tabular (em formato de tabela, com linhas e colunas).
    - `border` indica que a tabela deve ser renderizada com bordas.
- `thead` contém o cabeçalho da tabela.
    - use um `tr` para cada linha.
    - cada `th` dentro de um `tr` é uma célula de cabeçalho (um título de coluna).
- `tbody` contém o corpo (células) da tabela.
    - use um `tr` para cada linha.
    - cada `td` dentro de um `tr` é uma célula da tabela.

A tabela acima indica algo como:

| **Coluna 1** | **Coluna 2** | **Coluna 3** |
| --- | --- | --- |
| C1 x L1 | C2 x L1 | C3 x L1 |
| C1 x L2 | C2 x L2 | C3 x L2 |
| C1 x L3 | C2 x L3 | C3 x L3 |

Células podem conter qualquer tipo de conteúdo, inclusive outras tabelas. Porém, **não use isso para definir um leiaute para seu site**. Há ferramentas muito melhores para isso!
