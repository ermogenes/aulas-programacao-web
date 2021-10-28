
# Web Storage API

📽 Veja esta vídeo-aula no Youtube: _Em breve..._

Você pode manipular um armazenamento local, utilizando Javascript, para diversos fins, para manipular informações de uma página ou até mesmo estilos.

Este é o conceito de [_storage_](https://developer.mozilla.org/pt-BR/docs/Web/API/Storage), que possui os seguintes formatos:
-  [_localStorage_](https://developer.mozilla.org/pt-BR/docs/Web/API/Window/localStorage), aonde os dados armazenados não expiram, ou seja, os dados são **persistentes** até que um script o manipule ou o usuário limpe os dados através de ações do navegador.
- [_sessionStorage_](https://developer.mozilla.org/pt-BR/docs/Web/API/Window/localStorage), este segundo é menos utilizado, aonde os dados são **transientes**, que são excluídos após a sessão da página expirar.

## Disponibilidade
O acesso a ambos os armazenamentos são para um *domínio específico*, seja o armazenamento local ou o armazenamento de sessão, permitindo que você adicione, modifique ou exclua itens de dados armazenados.
Por exemplo:
- diegoneri.github.io terá um armazenamento específico de ermogenes.github.io, pois são considerados como domínios (subdomínio + domínio) distintos para o Storage.
- https://diegoneri.github.io terá o **mesmo** armazenamento de https://diegoneri.github.io/LocalStoragePokedex, por serem do mesmo domínio, diegoneri.github.io

> O uso de [_storage_](https://developer.mozilla.org/pt-BR/docs/Web/API/Storage) não é considerado substituto a uma opção *persistente* de armazenamento de dados, como um banco de dados relacional.

## Manipulação

* Armazenamento de sessão para um domínio: `Window.sessionStorage`
* Armazenamento local: `Window.localStorage`.

## Funções disponíveis

`Storage.key(<indiceChave>)`
> Quando passado um número n qualquer, maior ou igual a zero, este método retornará o nome da n-ésima chave no armazenamento.

`Storage.chave` ou `Storage.getItem(<chave>)`
> Utilizado para retornar o valor dessa chave.

`Storage.chave = <valor>` ou  `Storage.setItem(<valor>)`  
> Quando passado um nome de chave e valor, irá adicionar essa chave para o armazenamento, ou atualizar o valor dessa chave, se já existir.

`Storage.removeItem(<chave>)`
> Quando passado um nome de chave, irá remover essa chave do armazenamento.

`Storage.clear()`
> Quando chamado, irá esvaziar todas as chaves fora do armazenamento.

Aonde `Storage` = localStorage _ou_ sessionStorage.

## Exemplos

### Definindo chaves 
```
localStorage.corFundoDark = '#1C1C1C';
localStorage.corFonteDark = '#F0F8FF';

localStorage.corFundoClear = '#1C1C1C';
localStorage.corFonteClear = '#F0F8FF';

localStorage.nomeTema = 'Dark';
```
### Atribuindo a elementos da página
```
document.querySelector('html').style.backgroundColor  =  localStorage.corFundo;
document.querySelector('html').style.color  =  localStorage.corFonte;
```
### Utilizando em outras situações
```
const aplicaTema = () => {
    var tema = localStorage.nomeTema;
    if (tema = "Dark") {
        document.querySelector('html').style.backgroundColor  =  localStorage.corFundoDark;
        document.querySelector('html').style.color  =  localStorage.corFonteDark;
    }else{
        document.getElementById('bgColor').value  =  localStorage.corFundoClear;
        document.querySelector('html').style.color  =  localStorage.corFonteClear;        
    }
}
```
ou
```
const aplicaTema = () => {
    var tema = localStorage.nomeTema;
    document.querySelector('html').style.backgroundColor = localStorage.getItem('corFundo'.concat(tema));
    document.querySelector('html').style.color = localStorage.getItem('corFonte'.concat(tema));
}
```

## Exemplo completo
Código-Fonte: https://github.com/diegoneri/LocalStoragePokedex
Exemplo: https://diegoneri.github.io/LocalStoragePokedex/
