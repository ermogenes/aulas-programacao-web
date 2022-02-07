# REST com bancos de dados

Para cada exercício abaixo crie um repositório com o nome indicado contendo um projeto do tipo `web` em C#.

Adicione suporte a OpenAPI (Swagger) em todos eles.

---
## Exercício `TarefasAPI`

Crie um repositório baseado [nesse template](https://github.com/ermogenes/tarefas-cs-web-template).

Crie um banco de dados com a estrutura descrita [nesse repositório](https://github.com/ermogenes/tarefas-mysql):

```sql
CREATE SCHEMA `tarefas` DEFAULT CHARACTER SET utf8 ;

CREATE TABLE IF NOT EXISTS `tarefas`.`tarefa` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `descricao` VARCHAR(200) NOT NULL,
  `concluida` TINYINT(1) NOT NULL DEFAULT 0,
  PRIMARY KEY (`id`))
ENGINE = InnoDB;
```

Implemente um CRUD REST na tabela `tarefa`, com _endpoints_ que atendas as seguintes requisições:

_requisição | Resposta
--- | ---
`GET /api/tarefas` | Lista todas as tarefas
`GET /api/tarefas?somente_pendentes={?}` | Filtra por conclusão
`GET /api/tarefas?descricao={?}` | Filtra por descrição
`GET /api/tarefas/{id}` | Retorna uma tarefa, pelo ID
`POST /api/tarefas` | Nova tarefa
`PUT /api/tarefas/{id}` | Altera uma tarefa
`PATCH /api/tarefas/{id}/concluir` | Conclui uma tarefa pendente
`DELETE /api/tarefas/{id}` | Exclui tarefa

---

## 🏁 Orientações para entrega (alunos do curso presencial)

Confira no Teams o link da tarefa equivalente. Lá você postará o link dos repositórios que você criou, um para cada exercício.

**Repositório de exemplo:**
[Exercício `EtecAB` (Saída em console)](https://github.com/ermogenes/EtecAB)

Exemplo de link a ser postado: https://github.com/ermogenes/EtecAB
