# 1 - O que é Status HTTP

Um código numérico enviado pelo servidor para informar o resultado de uma requisição.

Quando o front-end faz uma chamada para API, o servidor responde com:

- um status HTTP;
- headers;
- body, quando houver dados para retornar.

Exemplo:

```http
GET /users/10
```

Resposta:

```http
200 OK
```

Isso significa que a requisição foi bem sucedida e o servidor retornará os dados do usuário com id 10.

Na prática, o status HTTP ajuda o front-end a entender se deve:

- exibir os dados em tela;
- exibir uma mensagem de erro;
- redirecionar o usuário;
- pedir login novamente;
- tentar a requisição depois;
- tratar uma falha do servidor.

---

# 2 - Por que Status HTTP existe

Sem ele, o front-end teria dificuldade para saber o que aconteceu com a requisição e como reagir a ela.

Imagine uma busca de usuário:

```http
GET /users/10
```

Possíveis respostas e reações do front-end:

- `200 OK`: usuário encontrado, exibir os dados;
- `404 Not Found`: usuário não encontrado, exibir mensagem de erro;
- `500 Internal Server Error`: erro no servidor, exibir mensagem de erro genérica;
- `401 Unauthorized`: usuário não autenticado, redirecionar para login.

O mesmo endpoint pode responder de formas diferentes dependendo do cenário. O status HTTP padroniza essa comunicação.

---

# 3 - Famílias de Status HTTP

Os status são agrupados por centenas.

## 1xx - Informacional

Indicam que a requisição foi recebida e ainda está em processamento.

São menos comuns no dia a dia do front-end.

Exemplo:

```http
100 Continue
```

## 2xx - Sucesso

Indicam que a requisição foi bem sucedida.

### 200 OK

É o status mais comum de sucesso.

Usado quando a requisição foi processada e o servidor retornou uma resposta.

Exemplo:

```http
GET /users/10
```

Resposta:

```http
200 OK
{
  "id": 10,
  "name": "João"
}
```

Uso comum:

- buscar usuários;
- buscar produtos;
- buscar detalhes de um registro;
- atualizar algo e retornar o objeto atualizado.

### 201 Created

Indica que um novo recurso foi criado com sucesso.

Muito usado em requisições POST.

- Exemplo:

```http
POST /users
```

Body:

```json
{
  "name": "Nícolas",
  "email": "nicolas@email.com"
}
```

Resposta:

```http
201 Created
```

Na prática, significa:

> O usuário foi criado com sucesso.

### 204 No content

Indica que a requisição deu certo, mas o servidor não retornou conteúdo no body.

Muito comum em `DELETE`.

Exemplo:

```http
DELETE /users/10
```

Resposta:

```http
204 No content
```

O recurso foi removido, mas não há dados para devolver.

## 3xx - Redirecionamento

Indicam que o cliente precisa ir para outro endereço.

### 301 Moved Permanently

Indica que o recurso mudou de URL permanentemente.

### 302 Found

Indica redirecionamento temporário.

> No front-end moderno consumindo APIs REST, é raro lidar diretamente com `3xx`, pois o cliente HTTP geralmente segue os redirecionamentos automaticamente. Mas eles aparecem em login, autenticação, rotas antigas e redirects de servidor.

## 4xx - Erro do cliente

Indicam que a requisição enviada pelo cliente tem algum problema.

Aqui, "cliente" pode ser:

- navegador;
- aplicação React;
- app mobile;
- Postman;
- outro sistema consumindo a API.

### 400 Bad Request

A requisição está inválida.

Exemplo:

```http
POST /users
```

Body inválido:

```json
{
  "name": "Nícolas" // falta a vírgula aqui
  "email": "nicolas@email.com"
}
```

Resposta:

```http
400 Bad Request
```

Uso comum:
- campo obrigatório ausente;
- formato inválido;
- body mal montado;
- regra de validação quebrada.

### 401 Unauthorized

Indica que o usuário não está autenticado.

Exemplo:

```http
GET /profile
```

Sem token:

```http
401 Unauthorized
```

Na prática:
> Você precisa fazer login para acessar esse recurso.

### 403 Forbidden

Indica que o usuário está autenticado, mas não tem permissão para acessar o recurso.

Exemplo:
```http
DELETE /admin/users/10
```

Usuário comum tentando acessar rota de admin:

```http
403 Forbidden
```

Diferença importante:
- `401 Unauthorized`: usuário não autenticado;
- `403 Forbidden`: usuário autenticado, mas sem permissão.

### 404 Not Found

Indica que o recurso solicitado não foi encontrado.

Exemplo:

```http
GET /users/999
```

Resposta:

```http
404 Not Found
```

Uso comum:
- usuário inexistente;
- produto removido;
- rota incorreta;
- ID inválido que não existe no banco.

### 409 Conflict

Indica conflito com o estado atual do sistema.

Exemplo:

```http
POST /users
```

Tentando cadastrar um email que já existe:

```http
409 Conflict
```

Na prática:

> A requisição faz sentido, mas entra em conflito com algo que já existe.

### 422 Unprocessable Entity

Indica que o servidor entende a requisição, mas os dados não passaram na validação.

Exemplo:

```json
{
  "name": "Nícolas",
  "email": "email-invalido"
}
```

Resposta:

```http
422 Unprocessable Entity
```

Muitas APIs usam `400` para validação. Outras usam `422`. O importante é manter consistência no projeto.
A diferença entre os dois, de forma mais comum, é:
- `400 Bad Request`: erro genérico de requisição inválida, pode ser usado para erros de sintaxe, formatação ou regras de negócio;
- `422 Unprocessable Entity`: erro específico de validação, indicando que os dados estão no formato correto, mas não atendem aos critérios de validação definidos pelo servidor.

Exemplo prático:
- `400 Bad Request`: O cliente envia um JSON mal formado, como:

```json
{
  "name": "Nícolas",
  "email": "email-invalido"
}
```

Resposta:

```http
400 Bad Request
```

- `422 Unprocessable Entity`: O cliente envia um JSON bem formado, mas com um email que não atende aos critérios de validação, como:

```json
{
  "name": "Nícolas",
  "email": "email-invalido"
}
```

Resposta:

```http
422 Unprocessable Entity
```


### 429 Too Many Requests

Indica que o cliente fez requisições demais em pouco tempo.

Muito comum em APIs com rate limit.

## 5xx - Erro do servidor

Indicam que o problema aconteceu no servidor.

### 500 Internal Server Error

Erro interno genérico.

Pode acontecer por:

- exceção não tratada;
- erro no banco de dados;
- regra quebrada no back-end;
- falha inesperada na aplicação.

Para o front-end, normalmente vira uma mensagem genérica:
> Ocorreu um erro inesperado. Tente novamente mais tarde.

### 502 Bad Gateway

Indica problema entre servidores.

Comum quando uma API depende de outro serviço e esse serviço falha.

### 503 Service Unavailable

Indica que o serviço está indisponível temporariamente.

Pode acontecer em manutenção, sobrecarga ou instabilidade.

### 504 Gateway Timeout

Indica que o servidor demorou demais para responder.

---

# 4 - Status HTTP com [Fetch API](1%20-%20Fetch%20API.md)

Um ponto muito importante:

`fetch` não cai automaticamente no `catch` quando recebe status `400`, `404`, ou `500`.

Exemplo:

```js
async function buscarUsuario(id) {
    const response = await fetch(`/users/${id}`);

    console.log(response.status); 
}
```

Mesmo se a API responder `404`, o `fetch` ainda considera que houve uma resposta HTTP válida.

Por isso, você precisa validar `response.ok`.

```js
async function buscarUsuario(id) {
    const response = await fetch(`/users/${id}`);

    if (!response.ok) {
        throw new Error("Erro HTTP");
    }

    const data = await response.json();

    console.log(data);
}
```

e utilizar try/catch para tratar erros de rede ou outros erros inesperados:

```js
async function buscarUsuario(id) {
    try {
        const response = await fetch(`/users/${id}`);

        if (!response.ok) {
            throw new Error("Erro HTTP");
        }

        const data = await response.json();

        console.log(data);
    } catch (error) {
        console.error(error);
    }
}
```

`response.ok` retorna `true` quando o status está entre `200` e `299`.

---

# 5 - Tratamento por Status

Em aplicações reais, é comum tratar status de formas diferentes.

```js
async function buscarUsuario(id) {
    const response = await fetch(`/users/${id}`);

    if (response.status === 404) {
        return null; // usuário não encontrado
    }

    if (response.status === 401) {
        throw new Error("Usuário não autenticado");
    }

    if (!response.ok) {
        throw new Error("Erro ao buscar usuário");
    }

    return await response.json();
}
```

Por essa razão, é importante conhecer os status HTTP para construir uma comunicação clara entre front-end e back-end, e para que o front-end possa reagir de forma adequada a cada situação.

Na prática:
- `404` pode significar "não encontrado";
- `401` pode mandar o usuário para login;
- `500` pode mostrar erro genérico;
- `200` permite usar os dados normalmente.

---

# 6 - Boas práticas

Use status HTTP de forma consistente.

Evite retornar `200 OK` para tudo.

> <span style="color: #bd5353;">Exemplo negativo:</span>

```http
200 OK
```

Body:

```json
{
  "error": "Usuário não encontrado"
}
```

Isso confunde o front-end, porque o status diz sucesso, mas o body diz erro.

> <span style="color: #53bd5e;">Exemplo positivo:</span>

```http
404 Not Found
```

Body:

```json
{
  "error": "Usuário não encontrado"
}
```

Boas práticas:
- use `200` para buscas e respostas bem-sucedidas;
- use `201` para criação de recursos;
- use `204` para ações que não retornam dados;
- use `400` para requisição inválida;
- use `401` para falta de autenticação;
- use `403` para falta de permissão;
- use `404` para recursos não encontrados;
- use `409` para conflitos de estado;
- use `422` para erros de validação;
- use `500` para erros inesperados do servidor.
- mantenha consistência no uso dos status em toda a API;

--- 

# 7 - Conclusão

Status HTTP é a forma padrão de uma API dizer ao cliente o resultado de uma requisição.

No front-end, entender esses códigos é essencial para consumir APIs corretamente, tratar erros, exibir mensagens adequadas e criar integrações mais previsíveis.

O ponto mais importante é:

> O status HTTP não é detalhe técnico. Ele faz parte do contrato entre front-end e back-end.

Esse conteúdo complementa principalmente:

- 1 - [Fetch API.md](1%20-%20Fetch%20API.md);
- 2 - [REST API.md](2%20-%20REST%20API.md);


