# Vitrine de Medicamentos 2

## Descrição do Projeto

Este projeto consiste em uma API completa desenvolvida com Node.js, TypeORM e PostgreSQL.
Seu objetivo principal é gerenciar informações de usuários e medicamentos, garantindo segurança, validação e uma estrutura profissional.

A aplicação permite que:

- Usuários se cadastrem.

- Façam login e autenticação segura.

- Registrem medicamentos que possuem em estoque.

- Gerenciem permissões e roles (RBAC) para controle de acesso.

## Funcionalidades

- Gerenciamento de Usuários
- Cadastro de usuários com hashing seguro de senhas (utilizando bcrypt ou similar).
- Autenticação de usuários com geração de tokens JWT.
- Atribuição de roles (papéis) e permissões aos usuários.

## Gerenciamento de Medicamentos
- CRUD completo:
- Criar medicamentos associados a usuários autenticados.
- Listar medicamentos de forma geral ou por usuário.

- Atualizar medicamentos (restrito ao criador).

- Excluir medicamentos (restrito ao criador).

- Relacionamento entre medicamentos e usuários:

- Cada medicamento pertence a um único usuário.

## Paginação e filtros:

- Paginação configurada via page e limit nos endpoints de listagem.

- Filtro por nome de medicamento nos endpoints de listagem.

- Gerenciamento de RBAC (Role-Based Access Control)
## CRUD de Permissões:

- Listar permissões.

- Criar novas permissões.

- CRUD de Roles:

- Listar roles.

- Criar novas roles.

- Associar permissões a roles.

- Associar roles a usuários.

## Middleware de Autenticação:

- Validação de tokens JWT.

- Verificação de roles e permissões para acesso a rotas privadas.

## Tecnologias Utilizadas
- Node.js (back-end)

- Express (servidor web)

- TypeORM (ORM para manipulação de banco de dados)

- PostgreSQL (banco de dados relacional)

- bcrypt (hashing de senhas)

- JWT (autenticação baseada em tokens)

- RBAC (controle de acesso baseado em roles)

## Estrutura das Rotas
- Rotas de Usuários
 POST /users
Cadastra um novo usuário com os campos:
nome, email, e senha (armazenada como hash).

 POST /login
Autentica um usuário com base no email e senha.
Retorna um token JWT para acesso aos endpoints protegidos.

- Rotas de Medicamentos
POST /medicamentos
Cria um novo medicamento associado ao usuário autenticado.
Campos: nome, descricao (opcional), quantidade.

GET /medicamentos/all
Lista todos os medicamentos cadastrados no sistema, com paginação e filtro por nome.

GET /medicamentos
Lista os medicamentos cadastrados pelo usuário autenticado, com paginação e filtro por nome.

GET /medicamentos/:id
Retorna os detalhes de um medicamento específico.

PUT /medicamentos/:id
Atualiza um medicamento específico.
Somente o usuário criador pode realizar a atualização.

DELETE /medicamentos/:id
Remove um medicamento específico.
Somente o usuário criador pode realizar a remoção.

- Rotas de RBAC (Role-Based Access Control)
GET /permissions
Lista todas as permissões cadastradas no sistema.

POST /permissions
Cria uma nova permissão.

GET /roles
Lista todas as roles cadastradas no sistema.

POST /roles
Cria uma nova role.

GET /roles/:id /permissions
Lista as permissões associadas a uma role específica.

POST /roles/:id /permissions
Adiciona uma permissão a uma role específica.

POST /users/:id /roles
Adiciona uma role a um usuário específico.


- Middleware de Autenticação e RBAC
- Autenticação: O middleware de autenticação valida o token JWT enviado nas requisições.

- RBAC: O middleware de RBAC verifica se o usuário possui a role e as permissões necessárias para acessar determinadas rotas.

## Exemplo de Uso do RBAC
Criar uma permissão:

Use a rota POST /permissions para criar uma nova permissão.

Criar uma role:

Use a rota POST /roles para criar uma nova role.

Associar permissão à role:

Use a rota POST /roles/:id/permissions para adicionar uma permissão a uma role.

Associar role ao usuário:

Use a rota POST /users/:id/roles para adicionar uma role a um usuário.

## Rotas Privadas e Controle de Acesso
As rotas de medicamentos e RBAC são protegidas por autenticação JWT.

O acesso a determinadas rotas pode ser restrito com base nas roles e permissões do usuário.
