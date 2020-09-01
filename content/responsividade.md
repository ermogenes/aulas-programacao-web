# Responsividade

[📽 Veja esta vídeo-aula no Youtube](#) _em breve..._

Trata-se da capacidade de um _site_ de se adaptar graciosamente ao diferentes tamanhos de tela dos agentes de usuário (_viewport_).

Existem diversas técnicas para adaptar o conteúdo de acordo com o tipo do dispositivo e tamanho da _viewport_. Quase todas elas utilizam como base as _media queries_.

## _Media query_

Podemos criar estilos que só serão aplicados se passarem por um teste de capacidade (e estado) do dispositivo. Podemos consultar se é uma tela ou mídia de impressão, se o dispositivo está em modo retrato ou paisagem, se o dispositivo permite _hover_, se a tela está com um determinada largura, entre tantas outras características.

A sintaxe indica uma condição para a aplicação das regras dos seletores internos à _media query_, e é utilizada da seguinte maneira:

```css
@media tipo-de-midia (funcionalidade: valor) {
    /* seletores e regras a serem aplicadas se <query> for verdadeira */
}
```

* `tipo-de-midia` - o tipo da mídia do usuário
* `funcionalidade` - uma funcionalidade do dispositivo do usuário
* `valor` - um valor desejado para a funcionalidade

Vejamos alguns exemplos.

### Tipo de mídia

- `screen` - uma tela de qualquer tipo
- `handheld` - um dispositivo portátil
- `tv` - uma televisão
- `print` - uma mídia impressa
- `speech` - mídia de voz (leitores de tela, por exemplo)
- `all` - todos os tipos de mídia

### Funcionalidades (_features_)

- `width: 700px` - exatamente 700px de largura
- `min-width: 700px` - pelo menos 700px de largura (ou mais)
- `max-width: 700px` - no máximo 700px de largura (ou menos)
- `color` - indica que o dispositivo exibe em cores
- `monochrome` - indica que o dispositivo exibe em tons de cinza
- `orientation: portrait` - dispositivo em modo retrato
- `orientation: landscape` - dispositivo em modo paisagem
- `hover: none` - o dispositivo não permite `hover`
- `hover: hover` - o dispositivo permite `hover`

Podemos indicar mais de uma condição usando `and`.

## `Media queries` e responsividade

Podemos criar estilos de acordo com o tamanho atual da _viewport_ do usuário.

No exemplo abaixo, o elemento receberá a cor azul em  _viewports_ entre 0 e 500px, a cor verde para _viewports_ entre 500 e 850px, e a cor vermelha para _viewports_ maiores de 850px:

```css
#elemento-responsivo {
    color: blue;
}

@media (min-width: 500px) and (max-width: 850px) {
    #elemento-responsivo {
        color: green;
    }
}

@media (min-width: 850px) {
    #elemento-responsivo {
        color: red;
    }
}
```

## Estilos de impressão

Podemos controlar o estilo de elementos a serem impressos:

```css
@media print {
    .nao-imprimivel {
        display: none;
    }
}
```

## Alternativas para dispositivos sem alguma capacidade

Podemos prover estilos alternativos caso o dispositivo não possua alguma capacidade:

```css
@media (hover: none) {
    /* seletores e regras que substituem algum elemento visual com hover */
}
```

## Imagens responsivas

Existem diversas técnicas para imagens responsivas, mas a técnica mais utilizada hoje em dia é prover imagens de um tamanho suficientemente grande (mas não maior que o maior uso) e permitir que ela ocupe o espaço disponível e reduza, se necessário.

Podemos fazer isso aplicando em imagens a regra `max-width: 100%;`.

Exemplo do comportamento padrão:

![](000100.gif)

Exemplo do comportamento com `max-width: 100%;`:

![](000099.gif)

## _Mobile-first_

É um consenso na comunidade que devemos criar nossos leiautes pensando primeiro em dispositivos pequenos, móveis, e adaptá-los para ocupar os espaços adicionais disponíveis em dispositivos maiores como monitores e televisores.