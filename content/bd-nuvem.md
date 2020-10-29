# Bancos de dados na nuvem

[📽 Veja esta vídeo-aula no Youtube](#) _Em breve..._

Precisamos agora de uma instância de produção do nosso banco de dados, acessível através de nossa aplicação.

Vamos então criar um banco local para servir o ambiente de desenvolvimento, desenvolver a aplicação de forma a manter a _string de conexão_ segura, provisionar o servidor e fazer a implantação do banco na nuvem, provisionar e implantar a aplicação, e, por fim, configurar a aplicação para utilizar o banco de dados de produção na nuvem.

Nsse material usaremos o banco de dados de exemplo `boardgames`.

- Banco: [ermogenes/boardgames-mysql](https://github.com/ermogenes/boardgames-mysql).
- Código-fonte: [ermogenes/boardgames-web](https://github.com/ermogenes/boardgames-web)
- Aplicação publicada: []()

## Criando o banco de desenvolvimento

Crie o banco de dados indicado acima em seu servidor local. Se ele estiver funcional, você deve ter as configurações semelhantes a essas (mas não necessariamente iguais):

- Servidor (local): `localhost`
- Porta: `3306`
- Usuário: `root` _(isso é somente um exemplo!)_
- Senha: `root` _(isso é somente um exemplo!)_
- Banco: `boardgames`

Isso implicará a seguinte _string de conexão_ de desenvolvimento:

```
server=localhost;port=3306;user=root;password=root;database=boardgames
```

Caso alguma configuração local sua seja diferente, ajuste a _string de conexão_. Anote em um local de fácil acesso.

## Criando o repositório para o código-fonte

Crie um repositório no GitHub com arquivo `README.md` e, _importante_, com `.gitignore` do tipo `VisualStudio`.

Clone esse repositório localmente e o acesse no VsCode. Ele conterá a sua aplicação.

## Ajustando o `.gitignore`

Antes de criarmos a aplicação usando `dotnet new`, vamos alterar o `.gitignore` para garantir que nenhuma informação sigilosa acabe subindo para o GitHub por engano.

Como vamos colocar a _string de conexão_ em um arquivo de configuração, vamos adicionar o nome dele na lista de arquivos a não serem versionados. Abra o `.gitignore` e adicione no final as seguintes linhas:

```
# ignorar arquivos de configuração
**/appsettings.development.json
**/appsettings.staging.json
**/appsettings.production.json
```

Se assim desejar, faça um _commit_ com essa versão.

## Criando a aplicação

Use `dotnet new webapi` para criar a aplicação com o _template_ padrão. Exclua os arquivos desnecessários `WeatherForecast.cs` e `Controllers\WeatherForecastController.cs`.

Confira quais arquivos estão sujeitos a versionamento usando `git status`. Certifique-se de que `appsettings.development.json` foi ignorado.

Se assim desejar, faça um _commit_ com essa versão.

## Desativando o redirecionamento HTTPS

Abra `Startup.cs` e comente (ou exclua) a linha abaixo:

```cs
app.UseHttpsRedirection();
```

Se assim desejar, faça um _commit_ com essa versão.

## Fazendo _scaffolding_ do banco local

Instale os pacotes necessários.

```
dotnet add package Microsoft.EntityFrameworkCore
dotnet add package Microsoft.EntityFrameworkCore.Design
dotnet add package MySql.Data.EntityFrameworkCore
```

Faça o _scaffolding_ usando a _string de conexão_ anotada anteriormente.

```
dotnet ef dbcontext scaffold "__" MySql.Data.EntityFrameworkCore -o __ -f
```

No meu exemplo ficará `dotnet ef dbcontext scaffold "server=localhost;port=3306;user=root;password=root;database=boardgames" MySql.Data.EntityFrameworkCore -o db -f`.

NÃO FAÇA AINDA _commit_ com essa versão. Ela contém usuário e senha do seu banco!

## Removendo a _string de conexão_ do contexto

A _string de conexão_ fica escrita literalmente no arquivo do contexto (No exemplo, fica em `db\boardgamesContext.cs`). Com os procedimentos abaixo vamos removê-la e guardá-la em um local seguro.

Abra o seu arquivo com a classe de contexo gerada pelo _scaffolding_. Localize o método `OnConfiguring`. Perceba que ele contém dados sigilosos. Remova as linhas existentes, deixando algo assim:

```cs
protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
{
    // remova os comandos existentes aqui
}
```

Ok, senhas seguras. O problema agora é que a aplicação não sabe mais como acessar o banco de dados.

A estratégia será criar no arquivo de configuração `appsettings.json` uma _string de conexão_ _fake_ que poderá ser versionada e publicada no GitHub, e em  `appsettings.development.json`, que não será versionado, guardaremos a _string de conexão_ verdadeira para o ambiente de desenvolvimento. Em produção, podemos criar uma configuração no Azure para substituir esse arquivo, apontando para o banco de produção.

Abra `appsettings.json` e adicione o seguinte objeto:

```cs
"ConnectionStrings" : {
    "boardgamesConnection": "<sua connection string vai aqui>"
}
```

Onde:

- `boardgamesConnection` é o identificador da nossa _string de conexão_.
- `<sua connection string vai aqui>` é um texto explicativo. **Não escreva sua _string de conexão_ real aqui**, use qualquer texto informativo.

Abra `appsettings.development.json` e adicione o seguinte objeto:

```cs
"ConnectionStrings" : {
    "boardgamesConnection": "<string de conexão real de desenvolvimento>"
}
```

- `<string de conexão real de desenvolvimento>`: aqui sim use a _string de conexão_ real, já que esse arquivo não será versionado.

Quem fizer o clone do repositório e quiser rodar localmente terá que copiar `appsettings.json` com o nome `appsettings.development.json` e ajustar a _string de conexão_ para o seu caso específico.

Na implantação orientaremos o Azure disponibilizar a _string de conexão_ de outra maneira.

Agora vamos orientar a aplicação a buscar e usar a _string de conexão_, mas não no contexto e sim em um serviço que ficará disponível em todas as _controllers_, facilitando o seu uso.

Vá em `Startup.cs` e procure o método `ConfigureServices`. Ele deve ter somente um comando que indica que vamos usar _controllers_ em nossa aplicação. Adicione antes desse comando o seguinte:

```cs
services.AddDbContext<db.boardgamesContext>(options => 
    options.UseMySQL(Configuration.GetConnectionString("boardgamesConnection"))
);
```

Onde `db.boardgamesContext` é a classe de contexto (que será diferente em cada projeto).

Será necessário adicionar a seguinte referência:

```cs
using Microsoft.EntityFrameworkCore;
```

## Criando _controllers_ com acesso ao contexto

Precisamos agora mudar a maneira que acessamos o nosso contexto de banco de dados. Em todas as _controllers_ que necessitarem do contexto, vamos obtê-lo diretamente em seu construtor, e salvá-lo em uma propriedade privada. Como o objeto é construído e destruído a cada execução, isso economizará recursos e facilitará a integração em aplicações mais complexas.

Nesse exemplo, vamos criar uma _controller_ chamada `BoardgamesController`. Criaremos nela uma propriedade privada chamada `_db` do tipo `db.boardgameContext` onde gravaremos o contexto recebido no construtor. Para isso, adicione código semelhante a esse na sua classe:

```cs
private boardgameContext _db { get; set; }
public BoardgamesController(boardgameContext contexto)
{
    _db = contexto;
}
```

Agora não será mais necessário usar a construção `using(...contexto...) { ... }` para acessar seu banco. Ele sempre estará acessível nessa classe através de `_db`.

Crie um método que atenda à rota `/Boardgames` retorne uma lista com todos os board games cadastrados em ordem de decrescente de nota.

```cs
[HttpGet]
public List<Boardgames> Get()
{
    var todosOsBoardGames = _db.Boardgames
        .OrderBy(bg => bg.nota)
        .ThenBy(bg => bg.ano)
        .ThenBy(bg => bg.nome);
    return todosOsBoardGames;
}
```

Teste sua API e se estiver funcionando corretamente, nosso backend está concluído e podemos prosseguir para o frontend.

Se assim desejar, faça um _commit_ com essa versão.

## Adicionando o suporte a arquivos estáticos

Em `Startup.cs` no método `Configure`, antes de `app.UseRouting()`, adicione as seguintes linhas:

```cs
app.UseDefaultFiles();
app.UseStaticFiles();
```

Isso garante que os arquivos em `wwwroot` serão entregues quando solicitados, e que caso uma pasta seja indicada em vez de um arquivo, será entregue o arquivo padrão (geralmente `index.html`).

Crie `wwwroot\index.html` com um conteúdo inicial bem simples, e teste. Caso esteja tudo certo, prossiga.

Se assim desejar, faça um _commit_ com essa versão.

## Criando o _frontend_

Faça uma página que consuma o _endpoint_ criado e exiba os board games retornados de uma maneira agradável ao usuário.

Teste e, se tudo estiver ok, a nossa aplicação estará pronta.

Faça um _commit_ com essa versão e faça o _push_ para o GitHub.

## Escolhendo a infraestrutura

Precisaremos do **Serviço de Aplicativos** para hospedar a aplicação, e de um servidor **Banco de Dados do Azure para MySQL** para hospedar o banco de dados.

Vamos simular os custos em [https://azure.microsoft.com/pt-br/pricing/calculator/](https://azure.microsoft.com/pt-br/pricing/calculator/).

Minha escolha foi:

- **Serviço de Aplicativos**: 
  - Região: `Oeste do EUA` (_West US_)
  - SO: `Windows`
  - Camada: `Gratuito`
  - Instância: `F1`
  - Custo: **Gratuito**
- **Banco de Dados do Azure para MySQL**
  - Região: `Oeste do EUA 2` (_West US 2_)
  - Camada: `Básico`
  - Computação: `Gen 5, 1 vCore`
  - Armazenamento: `5 GB`
  - Armazenamento adicional de backup: `0 GB`
  - Custo: **US$ 25,32/mês** (cobrados por hora de uso).

Perceba que não há opção de servidores MySQL gratuitos. Para esses exemplos, use a menor configuração que conseguir encontrar, pois não há nenhum requisito de desempenho envolvido. Certamente seus custos serão diferentes.

_💡 Use seus créditos com parcimônia, mas não fique com dó de usá-los para aprender. Quando não precisar mais da aplicação, exclua seu grupo de recursos para parar as cobranças._

Anote suas configurações escolhidas.

## Implantando a aplicação

Acesse o [Portal](https://portal.azure.com/) e crie o Serviço de Aplicativos integrado ao repositório do GitHub com os fontes da aplicação. Você deve ser capaz de acessar e visualizar as páginas do _frontend_, porém os _fetchs_ estarão recebendo um erro `500`, já que ainda não temos um banco de dados e a aplicação não conhece a _string de conexão_ a utilizar.

## Provisionando o servidor de banco de dados

## Criando a estrutura do banco

## Liberando o acesso à aplicação

## Obtendo a _string de conexão_ de produção

## Adicionado a _string de conexão_ na aplicação

## Ativando o _log_ para investigar erros