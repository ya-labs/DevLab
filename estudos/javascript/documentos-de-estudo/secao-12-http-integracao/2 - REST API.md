## 1 - O que é uma API?
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

É uma API construída seguindo os princípios REST.
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

Significa `JavaScript Object Notation`

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

---

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
200 OK
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

---

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

^^^

---

# 14 - Autenticação em REST API

Serve para identificar quem está usando a API.

Um fluxo comum é:

1 - Usuário faz login
2 - API valida e-mail e senha
3 - API retorna um token
4 - Front-end salva o token
5 - Front-end envia o token nas próximas requisições

Exemplo:

```http
POST /auth/login
```

Body:

```json
{
    "email": "user@email.com",
    "password": "123456"
}
```

Resposta:

```json
{
    "token": "token_aqui"
}
```

Depois:

```http
GET /profile
Authorization: Bearer token_aqui
```

---

# 15 - Autorização

Autenticação != autorização.

Autenticação:

- Quem é você?

Autorização:

- Você pode fazer isso?

Exemplo:

Um usuário logado pode acessar o próprio perfil.

Mas apenas administradores possam excluir usuários.

```http
DELETE /users/10
Authorization: Bearer token_aqui
```

Se o usuário não tiver permissão:

```http 
403 Forbidden
```

---

# 16 - CORS

Significa Cross-Origin Resource Sharing.

Ele define quais origens podem acessar a API pelo navegador.

Exemplo:

Front-end:

`http://localhost:3000`

Back-end:

`http://localhost:5000`

Mesmo estando na mesma máquina, são `origens diferentes` por causa da porta.

Se a API não permitir essa origem, o navegador bloqueia a requisição.

> <span style="color: white; font-weight: bold;">Importante:</span>

CORS é uma política de segurança do navegador.

Ferramentas como Postman ou Insomnia não sofrem bloqueio de CORS.

---

# 17 - Paginação

Serve para dividir uma lista grande de recursos em partes menores, evitando retornar dados demais de uma vez.

> <span style="color: #bd5353; font-weight: bold;">Exemplo negativo:</span>

```http
GET /products
```

Se existirem 100 mil produtos, retornar tudo em uma única requisição pode travar ou deixar a API lenta.

> <span style="color: #64ac6e; font-weight: bold;">Exemplo positivo:</span>

```http
GET /products?page=1&limit=20
```

Isso retorna apenas os 20 primeiros produtos.

Resposta:

```json
{
    "data": [
        { "id": 1, "name": "Produto 1" },
        { "id": 2, "name": "Produto 2" },
        ...
    ],
    "meta": {
        "total": 100000,
        "page": 1,
        "limit": 20,
        "totalPages": 5000
    }
}
```

Nesse caso, a resposta inclui um objeto `meta` com informações sobre a paginação, como o total de itens, a página atual, o limite por página e o total de páginas.

O objeto `data` contém a lista de produtos retornados.

---

# 18 - Filtros e ordenação

APIs geralmente permitem filtros.

Exemplo:

```http
GET /products?category=keyboard
```

Também pode permitir ordenação:

```http
GET /products?sort=price_desc
```

Ou ordem decrescente:

```http
GET /products?sort=price_asc
```

Ou

```http
GET /products?sort=-price
```

Ou 

```http
GET /products?sortBy=price&order=desc
```

O importante é manter um padrão claro.

> *Esses exemplos de nomenclaturas não são universais, mas sim padrões comuns utilizados em APIs REST.*

# 19 - Boas práticas em REST API

- usar nome de recursos no plural;
- usar métodos HTTP corretamente;
- retornar status codes adequados;
- não colocar ações desnecessárias nas URLs;
- validar dados recebidos;
- padronizar respostas de erro;
- usar paginação em listas grandes;
- proteger rotas privadas;
- não expor detalhes internos em erros;
- documentar a API;
- manter nomes consistentes;

# 20 - Exemplo completo de CRUD

CRUD = `Create, Read, Update, Delete`

Em português: `Criar, Ler, Atualizar, Deletar`

Recurso: produtos.

> <span style="color: white; font-weight: bold;">Criar produto:</span>

```http
POST /products
```

Body:

```json
{
    "name": "Mouser Gamer",
    "price": 149.90
}
```

Resposta:

```http
201 Created
```
```json
{
    "id": 1,
    "name": "Mouser Gamer",
    "price": 149.90
}
```

> <span style="color: white; font-weight: bold;">Buscar produto por ID</span>

```http
GET /products/1
```

Resposta:

```http
200 OK
```
```json
{
    "id": 1,
    "name": "Mouser Gamer",
    "price": 149.90
}
```

> <span style="color: white; font-weight: bold;">Atualizar produto:</span>

```http
PUT /products/1
```

Body:

```json
{
    "name": "Mouser Gamer RGB",
    "price": 179.90
}
``` 

Resposta:

```http
200 OK
```
```json
{
    "id": 1,
    "name": "Mouser Gamer RGB",
    "price": 179.90
}
```

> <span style="color: white; font-weight: bold;">Remover produto:</span>

```http
DELETE /products/1
```

Resposta:

```http
204 No Content
```

# 21 - REST API no front-end

Consumimos uma REST API fazendo requisições HTTP.

Exemplo com [fetch](./1%20-%20Fetch%20API.md):

```javascript
fetch("https://api.exemplo.com/users")
    .then(response => response.json())
    .then(data => {
        console.log(data);
    })
    .catch(error => {
        console.log("Erro ao buscar usuários:", error);
    });
```

Com [async/await](../secao-08-assincronismo/1%20-%20Promises%20e%20async.md):

```javascript
async function carregarUsuarios() {
    try {
        const response = await fetch("https://api.exemplo.com/users");

        if (!response.ok) { // valida se a resposta foi bem-sucedida
            throw new Error("Erro ao buscar usuários.");
        }

        const data = await response.json();

        console.log(data);
    } catch (error) {
        console.error(error);
    }
}

carregarUsuarios();
```

---

# (EXTRA) - Back-end
### 22 - REST API no back-end

Em um back-end, podemos criar uma REST API usando frameworks como Express (Node.js), Django (Python), Spring Boot (Java), Laravel (PHP) e muitos outros.

Mapeamos rotas que recebem requisições e retornam respostas.

Exemplo conceitual:

```
GET /users → buscar usuários
POST /users → criar usuário
GET /users/:id → buscar usuário por ID
PUT /users/:id → atualizar usuário
DELETE /users/:id → remover usuário
```

Cada rota normalmente chama alguma camada do sistema.

Exemplo de fluxo:

```
Controller -> Service -> Repository -> Banco de dados
```

Controller recebe a requisição.

Service aplica regras de negócio.

Repository faz a comunicação com o banco de dados.

### 23 - Controllers

É a camada que lida diretamente com a requisição HTTP.

Ele recebe:

- parâmetros de rota;
- query parameters;
- body;
- headers;
- usuário autenticado

E retorna:

- status code;
- dados;
- mensagem de erro;

Exemplo de controller em Express:

```javascript
app.get("/users/:id", (req, res) => {
    const userId = req.params.id;
    // lógica para buscar usuário no banco de dados
    const user = findUserById(userId);
    if (user) {
        res.status(200).json(user);
    } else {
        res.status(404).json({ message: "Usuário não encontrado." });
    }
});
```