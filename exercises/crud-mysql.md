# Exercícios: CRUD com MySQL

Para cada exercício abaixo crie um repositório com o nome indicado contendo um projeto do tipo `console` em C#.

As strings de conexão deverão apontar preferencialmente para o servidor `localhost` na porta `3306`, com usuário `root` e senha `root`, _para facilitar a correção_.

**Bancos**:

O banco de dados `employees` foi visto [nessa aula](https://github.com/ermogenes/aulas-programacao-csharp/blob/master/content/db-mysql.md).

O banco de dados `agenda` foi visto [nessa aula](https://youtu.be/D78qNi-Pff0).

O banco de dados `tarefas` foi visto [nessa aula](https://youtu.be/JI1-f04navk) e depois [nessa](https://youtu.be/tLkxJHqUDxk).

---
## Exercício `Seniors`

Faça um programa que consulte o banco `employees` e exiba o nome completo (no formato SOBRENOME, Nome) do funcionário mais antigo do sexo masculino, e também do sexo feminino.

Tabela `employees` (funcionários):
- `first_name` - nome
- `last_name` - sobrenome
- `gender` - sexo
- `hire_date` - data de contratação

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
## Exercício `Agenda`

Crie um repositório baseado [neste template](https://github.com/ermogenes/agenda-template).

Crie um banco de dados com a estrutura contida no arquivo `scripts/agenda.sql`:

```sql
DROP SCHEMA IF EXISTS `agenda` ;

CREATE SCHEMA IF NOT EXISTS `agenda` DEFAULT CHARACTER SET utf8 ;
USE `agenda` ;

DROP TABLE IF EXISTS `contato` ;

CREATE TABLE IF NOT EXISTS `contato` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `nome` VARCHAR(50) NOT NULL,
  `fone` VARCHAR(20) NULL,
  `estrelas` INT NULL,
  PRIMARY KEY (`id`),
  UNIQUE INDEX `nome_UNIQUE` (`nome` ASC) VISIBLE)
ENGINE = InnoDB;
```

Implemente as funções indicadas no menu, salvando no banco de dados criado.

---
## Exercício `Tarefas`

Crie um repositório baseado [neste template](https://github.com/ermogenes/tarefas-cs-console-template).

Crie um banco de dados com [esta](https://github.com/ermogenes/tarefas-mysql) estrutura:

```sql
CREATE SCHEMA `tarefas` DEFAULT CHARACTER SET utf8 ;

CREATE TABLE IF NOT EXISTS `tarefas`.`tarefa` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `descricao` VARCHAR(200) NOT NULL,
  `concluida` TINYINT(1) NOT NULL DEFAULT 0,
  PRIMARY KEY (`id`))
ENGINE = InnoDB;
```

Implemente as funções indicadas no menu, salvando no banco de dados criado.

---

## 🏁 Orientações para entrega (alunos do curso presencial)

Confira no Teams o link da tarefa equivalente. Lá você postará o link dos repositórios que você criou, um para cada exercício.

**Repositório de exemplo:**
[Exercício `EtecAB` (Saída em console)](https://github.com/ermogenes/EtecAB)

Exemplo de link a ser postado: https://github.com/ermogenes/EtecAB
