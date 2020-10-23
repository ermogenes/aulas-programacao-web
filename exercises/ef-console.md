# Exercícios: Entity Framework em console

Para cada exercício abaixo crie um repositório com o nome indicado contendo um projeto do tipo `console` em C#.

As strings de conexão deverão apontar preferencialmente para o servidor `localhost` na porta `3306`, com usuário `root` e senha `root`, _para facilitar a correção_.

**Bancos**:

O banco de dados `employees` foi visto [nessa aula](https://github.com/ermogenes/aulas-programacao-web/blob/master/content/orm-ef-mysql.md).

O banco de dados `hamburgueria` foi visto [nessa aula](https://github.com/ermogenes/aulas-programacao-web/blob/master/content/relacionamentos.md).

---
## Exercício `IngredientesExtras`

Faça um programa que consulte o banco `hamburgueria` e exiba todos os ingredientes do tipo "Extra" em ordem alfabética de nome de ingrediente.

---
## Exercício `MixDaCasa`

Faça um programa que consulte o banco `hamburgueria` e exiba os nomes dos burguers que levam o ingrediente "Burguer Mix da Casa", os mais baratos primeiro.

---
## Exercício `CadastroIngredientes`

Faça um programa que permita que o usuário cadastre um novo ingrediente no banco `hamburgueria`. Solicite que ele digite o nome do ingrediente e o tipo (1, 2 ou 3).

O código do ingrediente é um [GUID](https://pt.wikipedia.org/wiki/Identificador_%C3%BAnico_universal) e deve ser gerado pela aplicação usando o comando `Guid.NewGuid().ToString()`.

---
## Exercício `Seniors`

Faça um programa que consulte o banco `employees` e exiba o nome completo (no formato SOBRENOME, Nome) do funcionário mais antigo do sexo masculino, e também do sexo feminino.

Tabela `employees` (funcionários):
- `first_name` - nome
- `last_name` - sobrenome
- `gender` - sexo
- `hire_date` - data de contratação

---
## Exercício `DeptManager`

Faça um programa que consulte o banco `employees`. Peça que o usuário entre com o código do departamento (`departments.dept_no`). Descubra o seu gerente (o primeiro `dept_manager.emp_no` ordenado em ordem descendente de `to_date`). Exiba no seguinte formato:

- Se for um homem, `Production: Managed by Mr. Smith.`.
- Se for uma mulher, `Research: Managed by Mrs. Taylor.`.

---
## Exercício `DepartmentsCRUD`

Faça um programa que permita a manutenção da tabela `departments` do banco de dados `employees`.

A aplicação deve ter um menu com as seguintes opções:

- `Listar departamentos`: deve exibir código e nome de todos os departamentos, em ordem alfabética.
- `Consultar departamento por código`: deve solicitar que o usuário entre com o código, buscar e, se ele existir, exibir o seu nome.
- `Consultar departamento por nome`: deve solicitar que o usuário entre com um texto, buscar departamentos cujo nome contenha o texto, e se existir algum exibir a listagem com código e nome.
- `Cadastrar novo departamento`: deve solicitar entrada de código e nome do departamento e cadastrá-lo se o código ainda não existir.
- `Alterar departamento`: deve solicitar que o usuário entre com o código, buscar, e se ele existir, exibir o nome e solicitar o novo nome, que deverá ser salvo.
- `Excluir departamento`: deve solicitar que o usuário entre com o código e buscar o registro. Caso ele exista, verificar se ele possui algum funcionário (em `dept_emp`) ou algum gerente (em `dept_manager`). Se não possuir nenhum dos dois, perguntar se ele deseja excluir, e efetivar a exclusão somente se confirmado.

---

## 🏁 Orientações para entrega (alunos do curso presencial)

Confira no Teams o link da tarefa equivalente. Lá você postará o link dos repositórios que você criou, um para cada exercício.

**Repositório de exemplo:**
[Exercício `EtecAB` (Saída em console)](https://github.com/ermogenes/EtecAB)

Exemplo de link a ser postado: https://github.com/ermogenes/EtecAB