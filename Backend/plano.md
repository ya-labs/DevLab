### Seção 00 - Primeiros Passos Em Programação Backend

1. O que é backend
2. Como cliente e servidor se comunicam
3. O que é uma API
4. O que é HTTP
5. Request e response
6. Como uma aplicação backend roda
7. Como resolver problemas backend
8. Debug no backend

Essa seção conecta backend com os conteúdos de HTTP já estudados no frontend.

---

### Seção 01 - Base De C#

1. Variáveis e tipos em C#
2. Operadores
3. Condicionais
4. Loops
5. Arrays e listas
6. Métodos
7. Classes e objetos
8. Encapsulamento
9. Interfaces
10. Tratamento de erros com try/catch

Aqui é o equivalente backend da base JavaScript.

---

### Seção 02 - Fundamentos Do .NET

1. O que é .NET
2. Diferença entre C#, .NET, ASP.NET Core e Entity Framework
3. Estrutura de um projeto .NET
4. Program.cs
5. Comandos básicos do dotnet
6. Build, run, restore e packages
7. Injeção de dependência
8. Configurações com appsettings.json
9. Ambientes: Development, Staging e Production

---

### Seção 03 - ASP.NET Core Web API

1. Criando primeira API
2. Swagger/OpenAPI
3. Controllers
4. Rotas
5. Métodos HTTP: GET, POST, PUT, PATCH e DELETE
6. Parâmetros de rota
7. Query params
8. Body da requisição
9. Retornando status HTTP
10. Padronização de respostas

Essa seção conversa diretamente com os documentos de HTTP do frontend.

---

### Seção 04 - Arquitetura Básica De API

1. Separação de responsabilidades
2. Controller
3. DTO
4. Service
5. Repository
6. Entity
7. Validação de entrada
8. Mapeamento entre DTO e Entity

Essa parte aprofunda como organizar uma API em C# e .NET.

---

### Seção 05 - Banco De Dados E LINQ

1. O que é banco de dados
2. SQL básico
3. Tabelas, colunas e registros
4. Chave primária
5. Chave estrangeira
6. Relacionamentos
7. SELECT, INSERT, UPDATE e DELETE
8. Consultas com LINQ
9. Entity Framework Core
10. DbContext
11. DbSet
12. Migrations

---

### Seção 06 - CRUD Completo

1. CRUD em memória
2. Criar recurso
3. Buscar lista
4. Buscar por ID
5. Atualizar
6. Remover
7. Paginação
8. Filtros
9. Ordenação
10. Tratamento de recurso não encontrado
11. Validação de dados

Eu faria primeiro um CRUD de tarefas em memória e depois evoluiria para banco de dados.

---

### Seção 07 - Autenticação E Segurança

1. Autenticação vs autorização
2. Login
3. Hash de senha
4. JWT
5. Claims
6. Roles
7. Proteção de rotas
8. CORS
9. Dados sensíveis
10. Erros seguros
11. Rate limit

---

### Seção 08 - Boas Práticas De Backend

1. Tratamento global de erros
2. Logs
3. Validações com FluentValidation
4. Respostas padronizadas
5. Versionamento de API
6. Organização de pastas
7. Clean Code básico
8. Documentação da API
9. Variáveis de ambiente
10. Configurações sensíveis

---

### Seção 09 - Testes No Backend

1. O que são testes automatizados
2. Testes unitários
3. Testes de service
4. Testes de repository
5. Testes de endpoint
6. Mocks
7. Dados de teste
8. Testes de integração
9. Diferença entre teste unitário, integração e E2E
10. Quando testar cada camada

---

### Seção 10 - Projeto Prático

1. API de tarefas
2. API de produtos
3. API de usuários com login
4. API com relacionamento entre tabelas
5. API consumida por frontend
6. CRUD com banco de dados
7. Autenticação com JWT
8. Validação e tratamento global de erros
9. Logs e documentação com Swagger
10. Deploy básico

  ## Ordem Que Eu Recomendo Para Você

  1. Comece por “O que é backend”.
  2. Depois estude HTTP, request, response e API.
  3. Aprenda C# básico.
  4. Aprenda o básico de .NET.
  5. Crie uma Web API simples.
  6. Faça CRUD sem banco, usando lista em memória.
  7. Depois coloque banco com Entity Framework.
  8. Depois autenticação.
  9. Depois organização profissional: DTO, Service, Repository, validação e logs.

  ## Primeiros Documentos Que Eu Criaria

  Backend/estudos/dotnet/documentos-de-estudo/secao-00-primeiros-passos-backend/
  1 - O que é backend.md
  2 - Cliente servidor e API.md
  3 - HTTP para backend.md
  4 - Request e Response.md
  5 - Como uma API funciona.md

  Depois:

  Backend/estudos/dotnet/documentos-de-estudo/secao-01-base-csharp/
  1 - Variáveis e tipos em CSharp.md
  2 - Condicionais.md
  3 - Loops.md
  4 - Métodos.md
  5 - Classes e objetos.md

  Minha recomendação: não comece direto criando API com banco. Comece entendendo o fluxo:

  Front-end faz requisição
  ↓
  API recebe
  ↓
  Controller interpreta
  ↓
  Service aplica regra
  ↓
  Repository acessa banco
  ↓
  API devolve resposta
  ↓
  Front-end usa os dados
