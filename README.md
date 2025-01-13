# Task Manager - API REST

API REST que permite aos usuários gerenciar listas de tarefas. A aplicação oferece:
- Registro e login de usuários
- Operações CRUD para tarefas
- Ordenação e filtragem para personalizar as visualizações
- Segurança garantida por autenticação baseada em JWT
- Controle de autorização para garantir que apenas os criadores possam excluir ou alterar recursos

## Tecnologias

- Java 17
- Spring Boot
- Spring Security 6 com JWT
- Spring Data JPA
- Spring Web
- Lombok
- JJWT API
- MapStruct

## Requisitos

- JDK 17

- Maven instalado para construir e executar a aplicação

- PostgreSQL instalado e configurado. Certifique-se de criar o banco de dados necessário e ajustar as credenciais
no arquivo de config

- Um cliente HTTP capaz de manipular as requisições, como o Postman, Insomnia ou similares, para testar e enviar
o Token de autenticação nas requisições protegidas

  
## Instalação e execução

Siga os passos para obter e executar o projeto na sua máquina

1. Clone ou faça o [download](https://github.com/gabriellrocha/task-manager-api-jwt/archive/refs/heads/main.zip) do repositório
```
git clone https://github.com/gabriellrocha/task-manager-api-jwt.git
```
2. Navegue até a pasta raiz
```
cd task-manager-api
```
3. Execute `mvn clean install` para construir o projeto e baixar as dependências

4. Inicie a aplicação com `mvn spring-boot:run`

5. Use o cliente HTTP para testar os endpoints da API. Certifique-se de fazer o registro e enviar o Token de
autenticação nos endpoints protegidos

## Endpoints

| Método | Endpoint               | Descrição                                  | Autenticação |                        Filtros e Ordenação                        |                                           Body (JSON)                                           |
|--------|------------------------|--------------------------------------------|:------------:|:-----------------------------------------------------------------:|:-----------------------------------------------------------------------------------------------:|
| POST   | /api/auth/register     | Registrar o usuário e retorna um token     |      ❌       |                                 ❌                                 | { "firstName": "gabriel", "lastName": "silva", "email": "gabriel@mail.com", "password": "123" } |
| POST   | /api/auth/login        | Autenticar o usuário e retorna um token    |      ❌       |                                 ❌                                 |                        {"email": "gabriel@mail.com", "password": "123"}                         |
| POST   | api/v1/tasks           | Criar uma nova tarefa                      |      ✅       |                                 ❌                                 |        {"title": "test", "description": "desc", "priority": "LOW", "status": "PENDING" }        |
| PUT    | api/v1/tasks/{task_id} | Atualizar um tarefa específica             |      ✅       |                                 ❌                                 |    {"title": "updated", "description": "updated", "priority": "LOW", "status": "COMPLETED" }    |
| GET    | api/v1/tasks/{task_id} | Retornar detalhes de uma tarefa específica |      ✅       |                                 ❌                                 |                                                ❌                                                |
| GET    | api/v1/tasks/          | Listar todas as tarefas do usuário         |      ✅       | ?status={status}&priority={priority}&sort={field},asc&size={size} |                                                ❌                                                |
| DELETE | api/v1/tasks/{task_id} | Excluir uma tarefa específica              |      ✅       |                                 ❌                                 |                                                ❌                                                |


### Legenda para Filtros e Ordenação

|  Campo   |                    Descrição                    |    Default    |             Alternativas             |
|:--------:|:-----------------------------------------------:|:-------------:|:------------------------------------:|
|  status  |           filtra as tasks por status            |    PENDING    |              COMPLETED               |
| priority |         filtra as tasks por prioridade          |     HIGH      |             LOW, MEDIUM              |
|   sort   | ordena por campo + `asc` ou `desc` para direção | createdAt,asc | description, priority, status, title |
|   size   |         quantidade de tasks por página          |      10       |             ? número > 0             |
