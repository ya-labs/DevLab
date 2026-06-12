### Seção 00 - Primeiros Passos Em Programação Backend

  1. O que é backend
  2. Como cliente e servidor se comunicam
  3. O que é uma API
  4. O que é HTTP
  5. Request e response
  6. Como uma aplicação backend roda
  7. Como resolver problemas backend
  8. Debug no backend

  Essa seção é importante porque conecta com o que já existe em Frontend/estudos/javascript/documentos-de-estudo/secao-12-http-integracao/2 - REST API.md.

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

  ### Seção 02 - Fundamentos Do .NET

  1. O que é .NET
  2. Diferença entre C#, .NET, ASP.NET Core e Entity Framework
  3. Estrutura de um projeto .NET
  4. Program.cs
  5. Injeção de dependência
  6. Configurações com appsettings.json
  7. Ambientes: Development, Staging e Production

  ### Seção 03 - ASP.NET Core Web API

  1. Criando primeira API
  2. Controllers
  3. Rotas
  4. Métodos HTTP: GET, POST, PUT, PATCH e DELETE
  5. Parâmetros de rota
  6. Query params
  7. Body da requisição
  8. Retornando status HTTP
  9. Padronização de respostas
  10. Swagger/OpenAPI

  Essa seção conversa diretamente com os documentos de HTTP do frontend.

  ### Seção 04 - Arquitetura Básica De API

  1. Controller
  2. Service
  3. Repository
  4. DTO
  5. Entity
  6. Separação de responsabilidades
  7. Validação de entrada
  8. Mapeamento entre DTO e Entity

  Essa parte já aparece conceitualmente no final de REST API.md, mas no backend você pode aprofundar com C# e .NET.

  ### Seção 05 - Banco De Dados

  1. O que é banco de dados
  2. SQL básico
  3. Tabelas, colunas e registros
  4. Chave primária
  5. Chave estrangeira
  6. Relacionamentos
  7. SELECT, INSERT, UPDATE e DELETE
  8. Migrations
  9. Entity Framework Core
  10. DbContext
  11. DbSet
  12. Consultas com LINQ

  ### Seção 06 - CRUD Completo

  1. Criar recurso
  2. Buscar lista
  3. Buscar por ID
  4. Atualizar
  5. Remover
  6. Paginação
  7. Filtros
  8. Ordenação
  9. Tratamento de recurso não encontrado
  10. Validação de dados

  Eu faria um CRUD de Produtos, Usuários ou Tarefas.

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

  ### Seção 08 - Boas Práticas De Backend

  1. Tratamento global de erros
  2. Logs
  3. Validações com FluentValidation
  4. Respostas padronizadas
  5. Versionamento de API
  6. Organização de pastas
  7. Clean Code básico
  8. Testes automatizados
  9. Testes de endpoint
  10. Documentação da API

  ### Seção 09 - Projeto Prático

  1. API de tarefas
  2. API de produtos
  3. API de usuários com login
  4. API com relacionamento entre tabelas
  5. API consumida por frontend
  6. Deploy básico

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
