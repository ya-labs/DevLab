## 1 - O que é uma API?

API significa Application Programming Interface.
De forma simples, é uma forma de comunicação entre sistemas.

Exemplo:

Um front-end feito em React precisa buscar os dados de um usuário.
Ele não acessa diretamente o banco de dados.
Ele faz uma requisição para o back-end. 

O back-end busca as informações, processa as regras necessárias para tratamento dos dados e devolve uma resposta.

Fluxo básico:
``Front-end -> API -> Back-end -> Banco de dados``
``Banco de dados -> Back-end -> API -> Front-end``
A API funciona como ponte entre quem pede os dados e quem fornece os dados.

---

## 2 - O que é REST?

REST significa Representational State Transfer.

É um estilo de arquitetura para construção de APIs.

Uma REST API segue algumas ideias principais:

- usar HTTP como base da comunicação;
- representar recursos por URLs;
- usar métodos HTTP para indicar ações;
- trafegar dados geralmente em JSON;
- manter a comunicação sem estado (stateless);
- retornar respostas padronizadas.

Exemplo de recurso:
- /users
- /products
- /orders
- /posts

Cada recurso representa algo importante do sistema.

---

## 3 - O que é uma REST API?

Uma REST API é uma API construída seguindo os princípios REST.
Ela permite que sistemas conversem usando requisições HTTP.

Exemplo:
- GET /users

Essa requisição pode significar:
`buscar todos os usuários`

Outro exemplo:
- GET /users/10

Essa requisição pode significar:
`buscar o usuário com id 10`

---

## 4 - O que são recursos?

Em REST, é qualquer informação importante do sistema que queremos acessar ou manipular.

Exemplos:
- Usuários
- Produtos
- Pedidos
- Categorias
- Comentários
- Pagamentos

No código, esses recursos normalmente viram entidades, tabelas, models ou collections.

Exemplo de recurso usuário:
```json
{
  "id": 10,
  "name": "Nícolas",
  "email": "nicolas@email.com"
}
```
A URL deve representar esse recurso:
- /users

Ou um item específico:
- /users/10

---

## 5 - Métodos HTTP?
<!-- será incluído aprofundamento depois -->
Indicam a ação que será realizada sobre o recurso.

### GET
Usado para buscar dados.
```http
GET /users
```
-> Busca todos os usuários.

```http
GET /users/10
```
-> Busca o usuário com id 10.
GET não deve alterar o estado do recurso, apenas ler os dados.

### POST
Usado para criar um novo recurso.
```http
POST /users
```
-> Cria um novo usuário.

Recebe um body com os dados do usuário que será criado:
```json
{
  "name": "Nícolas",
  "email": "
}
```

### PUT
Usado para atualizar um recurso <strong>INTEIRO</strong>.
```http
PUT /users/10
```

Recebe um body com os dados do usuário que será atualizado:
```json
{
  "name": "Nícolas",
  "email": "nicolas@email.com"
}
```
Normalmente o PUT substitui o recurso completo.

### PATCH
Usado para atualizar um recurso <strong>PARCIALMENTE</strong>.
```http
PATCH /users/10
```

Recebe um body com os dados do usuário que será atualizado:
```json
{
  "email": "nicolas@email.com"
}
```

### DELETE
Usado para deletar um recurso.

```http
DELETE /users/10
```

-> Deleta o usuário com id 10.

---

# 6 - URLs em REST
Em uma REST API, as URLs devem representar recursos, não ações.

Exemplos positivos:
```html
GET /users
POST /users
GET /users/10
PUT /users/10
PATCH /users/10
DELETE /users/10
```

Exemplos negativos:
```html
GET /get-users
POST /create-user
GET /get-user?id=10
PUT /update-user?id=10
PATCH /update-user?id=10
DELETE /delete-user?id=10
```

O método HTTP já indica a ação.

---

# 7 - Padrão de nomes das rotas

Geralmente, usamos nomes no plural para os recursos:
- /users
- /products
- /orders
- /categories.

---

# 8 - Parâmetros de rota

São usados para identifacr recursos específicos.

Exemplo:
```http
GET /users/10
```
Nesse caso, 10 é o id do usuário que queremos acessar.

Outro exemplo:
```http
GET /orders/25/items
```
Busca todos os itens do pedido 25.

---

# 9 - Query parameters

São usados para filtros, paginação, busca e ordenação.

Eles vêm após o símbolo ? na URL.

Exemplo:

```http
GET /users?name=Nícolas
```
-> Busca usuários com o nome Nícolas.

```http
GET /products?category=electronics&sort=price_desc
GET /products?search=teclado
GET /orders?active=true
```
Diferença simples entre parâmetros de rota e query parameters:
- Parâmetros de rota: identificam um recurso específico (ex: /users/10).
- Query parameters: filtra uma lista de recursos (ex: /users?name=Nícolas).

Na prática, ambos podem ser usados para buscar um recurso específico, mas o mais comum é usar parâmetros de rota para isso.

---

# 10 - Body da requisição

É o corpo da requisição.
Usado principalmente em POST, PUT e PATCH.

Exemplo:
```http
POST /users
```

Body:
```json
{
  "name": "Nícolas",
  "email": "nicolasmacardoso@gmail.com"
}
```

Carrega os dados que serão enviados para a API.
GET normalmente não tem body.

---

# 11 - JSON

JSON significa `JavaScript Object Notation`

É um formato de dados muito usado em APIs.`

Exemplo:
```json
{
    "id": 1,
    "name": "Produto X",
    "price": 99.90,
    "active": true
}
```

JSON é leve, fácil de ler e funciona bem entre linguagens.

Mesmo tendo "JavaScript" no nome, não é exclusivo do JavaScript.

APIs feitas em C#, Java, PHP, Python, Node.js e várias outras linguagens podem usar JSON normalmente.

# 12 - Exemplos de resposta

> <span style="color: #64ac6e;">Sucesso:</span>

```http
GET /users/1
```

Resposta:

```json
{
    "id": 1,
    "name": "Ana",
    "email": "ana@email.com"
}
```

Status:

```http
200 ok
```

> <span style="color: #bd5353;">Erro:</span>

```http
POST /users
```

Body inválido:

```json
{
    "name": "",
    "email": "email-invalido"
}
```

Resposta:

```json
{
    "message": "Dados inválidos.",
    "errors": {
        "name": ["O nome é obrigatório"],
        "email": ["O email informado é inválido"]
    }
}
```

*Nesse caso, as variáveis dentro do objeto error estão em arrays para exemplificar que pode haver mais de um erro para cada campo.*

Status:

```http
400 Bad Request
```

# 13 - Stateless

Uma REST API deve ser stateless.

Isso significa que cada requisição deve conter todas as informações necessárias para ser processada.

A API não deve depender de uma requisição anterior para entender a atual.

Exemplo:

```http
GET /profile
Authorization: Bearer token_aqui
```

O servidor usa o token para identificar o usuário.

Ele não deve depender de uma "memória" da requisição anterior.

Isso ajuda a API a ser mais escalável e previsível.