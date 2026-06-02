# 1 - O que são Headers HTTP

Informações extras enviadas junto com uma requisição ou resposta HTTP.

Eles não representam o conteúdo principal da resposta. Eles funcionam como `Metadados`, ou seja, informações sobre a comunicação.

Quando o front-end faz uma requisição para uma API, a comunicação normalmente possui:
- método HTTP;
- URL;
- headers;
- body, quando necessário;
- status HTTP na resposta;
- body da resposta, quando houver.

Exemplo simples de requisição:

```
GET /usuarios
Accept: application/json
```

Nesse exemplo, o header `Accept` informa que o cliente espera receber uma resposta em JSON.

---

# 2 - Por que Headers HTTP existem

Headers existem para permitir que cliente e servidor troquem informações além dos dados principais.

Na prática, eles ajudam a responder perguntas como:
- Qual formato de dados está sendo enviado?
- Qual formato de resposta o cliente espera?
- O usuário está autenticado?
- A resposta pode ser armazenada em cache?
- A requisição veio de qual origem?
- Cookies devem ser enviados?
- Qual idioma o cliente prefere?

Sem headers, a API teria dificuldade para entender detalhes importantes da requisição.

Exemplo:

```
POST /usuarios
Content-Type: application/json
```

O header Content-Type informa ao servidor:

> O body desta requisição está no formato JSON.

---

# 3 - Headers de requisição e headers de resposta

Existem dois momentos principais em que headers aparecem.

Headers de requisição são enviados pelo cliente para o servidor.

Exemplo:

```
Authorization: Bearer token_aqui
Content-Type: application/json
Accept: application/json
```

Headers de resposta são enviados pelo servidor para o cliente.

Exemplo:

```
Content-Type: application/json
Cache-Control: no-cache
Set-Cookie: sessionId=abc123
```

No front-end, geralmente os headers são enviados usando `fetch` e são lidos através do objeto `Response`.

---

# 4 - Headers mais comuns no front-end

Content-Type

Informa o tipo de conteúdo que está sendo enviado.

Exemplo com JSON:

```
Content-Type: application/json
```

Uso comum no fetch:

```js
async function criarUsuario () {
    const response = await fetch("/api/usuarios", {
        method: "POST",
        headers: {
            "Content-Type": "application/json"
        },
        body: JSON.stringify({
            nome: "Nicolas",
            email: "nicolas@email.com"
        })
    });

    const data = await response.json();

    console.log(data);
}
```

Explicação:

- `method: "POST"` informa que a requisição vai criar um recurso;
- `headers` configura os metadados da requisição;
- `"Content-Type": "application/json"` informa que o body está em JSON;
- `JSON.stringify(...)` transforma o objeto JavaScript em uma string JSON.

Sem `Content-Type`, algumas APIs podem não conseguir interpretar corretamente o body enviado.

### Accept

Informa qual tipo de resposta o cliente espera receber.

Exemplo:

```
Accept: application/json
```

No front-end:

```js
const response = await fetch("/api/produtos", {
    headers: {
        accept: "application/json"
    }
});
```

Na prática, esse header diz:

> Servidor, eu prefiro receber a resposta em JSON.

Nem toda API exige esse header, mas ele deixa a comunicação mais explícita.

### Authorization

Usado para enviar credenciais de autenticação.

Muito comum em APIs que usam JWT.

Exemplo:

```
Authorization: Bearer token_aqui
```

No `fetch`:

```js
async function buscarPerfil (token) {
    const response = await fetch("/api/perfil", {
        headers: {
            Authorization: `Bearer ${token}`
        }
    })
}
```

