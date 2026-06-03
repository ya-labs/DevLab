# Headers HTTP

Headers HTTP são informações extras enviadas junto com uma requisição ou resposta HTTP.

Eles não representam o conteúdo principal. Eles funcionam como metadados da comunicação entre cliente e servidor.

---

# 1 - O que são Headers HTTP

Quando o front-end faz uma requisição para uma API, a comunicação normalmente possui:

- método HTTP;
- URL;
- headers;
- body, quando necessário;
- status HTTP na resposta;
- body da resposta, quando houver.

Exemplo simples:

```http
GET /usuarios
Accept: application/json
```

Nesse exemplo, o header `Accept` informa que o cliente espera receber uma resposta em JSON.

---

# 2 - Por que Headers HTTP existem

Headers permitem que cliente e servidor troquem informações além dos dados principais.

Na prática, eles ajudam a responder perguntas como:

- qual formato de dados está sendo enviado?
- qual formato de resposta o cliente espera?
- o usuário está autenticado?
- a resposta pode ser armazenada em cache?
- a requisição veio de qual origem?
- cookies devem ser enviados?
- qual idioma o cliente prefere?

Sem headers, a API teria dificuldade para interpretar detalhes importantes da requisição.

Exemplo:

```http
POST /usuarios
Content-Type: application/json
```

O header `Content-Type` informa ao servidor:

> O body desta requisição está no formato JSON.

---

# 3 - Headers de requisição e headers de resposta

Headers de requisição são enviados pelo cliente para o servidor.

```http
Authorization: Bearer token_aqui
Content-Type: application/json
Accept: application/json
```

Headers de resposta são enviados pelo servidor para o cliente.

```http
Content-Type: application/json
Cache-Control: no-cache
Set-Cookie: sessionId=abc123
```

No front-end, geralmente os headers são enviados usando `fetch` e são lidos através do objeto `Response`.

---

# 4 - Headers mais comuns no front-end

## Content-Type

Informa o tipo de conteúdo que está sendo enviado.

```http
Content-Type: application/json
```

Uso comum no `fetch`:

```js
async function criarUsuario() {
    const response = await fetch("/api/usuarios", {
        method: "POST",
        headers: {
            "Content-Type": "application/json"
        },
        body: JSON.stringify({
            nome: "Nícolas",
            email: "nicolas@email.com"
        })
    });

    if (!response.ok) {
        throw new Error("Erro ao criar usuário");
    }

    return response.json();
}
```

Sem `Content-Type`, algumas APIs podem não interpretar corretamente o body enviado.

## Accept

Informa qual tipo de resposta o cliente espera receber.

```http
Accept: application/json
```

No front-end:

```js
const response = await fetch("/api/produtos", {
    headers: {
        Accept: "application/json"
    }
});
```

Esse header deixa a comunicação mais explícita.

## Authorization

Usado para enviar credenciais de autenticação.

Muito comum em APIs que usam JWT.

```http
Authorization: Bearer token_aqui
```

No `fetch`:

```js
async function buscarPerfil(token) {
    const response = await fetch("/api/perfil", {
        headers: {
            Authorization: `Bearer ${token}`
        }
    });

    if (!response.ok) {
        throw new Error("Erro ao buscar perfil");
    }

    return response.json();
}
```

O token ajuda o servidor a identificar e autorizar o usuário.

## Cache-Control

Controla como a resposta pode ser armazenada em cache.

```http
Cache-Control: no-store
```

Em APIs, esse header pode ser usado para evitar que dados sensíveis ou muito dinâmicos sejam reaproveitados incorretamente.

## Set-Cookie

É enviado pelo servidor para criar ou atualizar um cookie no navegador.

```http
Set-Cookie: sessionId=abc123
```

Quando a API usa cookies, o front-end muitas vezes precisa enviar credenciais.

```js
fetch("/api/perfil", {
    credentials: "include"
});
```

Esse assunto se conecta com `Frontend/estudos/javascript/documentos-de-estudo/secao-12-http-integracao/9 - Cookies Sessao e Credentials.md`.

---

# 5 - Lendo headers na resposta com Fetch

O `fetch` permite acessar headers da resposta através de `response.headers`.

```js
async function buscarDados() {
    const response = await fetch("/api/produtos");

    const contentType = response.headers.get("Content-Type");

    console.log(contentType);
}
```

Explicação:

- `response` representa a resposta HTTP inteira;
- `response.headers` contém os headers da resposta;
- `.get("Content-Type")` busca o valor de um header específico.

Isso é útil quando você precisa verificar o tipo de conteúdo retornado pela API.

---

# 6 - Exemplo prático completo

```js
async function buscarPerfil(token) {
    const response = await fetch("/api/perfil", {
        method: "GET",
        headers: {
            Accept: "application/json",
            Authorization: `Bearer ${token}`
        }
    });

    if (!response.ok) {
        throw new Error("Erro ao buscar perfil");
    }

    const contentType = response.headers.get("Content-Type");

    if (!contentType || !contentType.includes("application/json")) {
        throw new Error("Resposta não está no formato JSON");
    }

    return response.json();
}
```

O que acontece nesse código:

- `Accept` informa que o front-end espera JSON;
- `Authorization` envia o token do usuário;
- `response.ok` valida se o status está entre 200 e 299;
- `response.headers.get("Content-Type")` lê um header da resposta;
- a validação evita tentar tratar como JSON uma resposta que não é JSON.

---

# 7 - Erros comuns

### Enviar body JSON sem Content-Type

```js
await fetch("/api/usuarios", {
    method: "POST",
    body: JSON.stringify({ nome: "Ana" })
});
```

A API pode não entender corretamente o formato do corpo.

### Confundir Content-Type com Accept

`Content-Type` indica o formato do conteúdo enviado.

`Accept` indica o formato que o cliente aceita receber.

### Esquecer Authorization

Sem o token, a API pode retornar erro de autenticação ou autorização.

### Tentar ler header que o navegador não expõe

Em requisições cross-origin, alguns headers só ficam disponíveis para o JavaScript se a API permitir via CORS.

Esse assunto se conecta com `Frontend/estudos/javascript/documentos-de-estudo/secao-12-http-integracao/6 - CORS.md`.

---

# 8 - Relação com outros estudos

Antes deste assunto, vale revisar `Frontend/estudos/javascript/documentos-de-estudo/secao-12-http-integracao/1 - Fetch API.md`, porque é onde headers aparecem no uso prático.

Este conteúdo também se conecta com:

- `Frontend/estudos/javascript/documentos-de-estudo/secao-12-http-integracao/2 - REST API.md`;
- `Frontend/estudos/javascript/documentos-de-estudo/secao-12-http-integracao/3 - Status HTTP.md`;
- `Frontend/estudos/javascript/documentos-de-estudo/secao-12-http-integracao/5 - Autenticacao e JWT.md`;
- `Frontend/estudos/javascript/documentos-de-estudo/secao-12-http-integracao/6 - CORS.md`;
- `Frontend/estudos/javascript/documentos-de-estudo/secao-12-http-integracao/9 - Cookies Sessao e Credentials.md`.

Esse conteúdo não precisa repetir autenticação, CORS ou cookies em profundidade. Aqui o foco é entender o papel dos headers na comunicação.

---

# 9 - Conclusão

Headers HTTP são metadados que dão contexto para requisições e respostas.

No front-end, os mais importantes no começo são `Content-Type`, `Accept` e `Authorization`. Entender bem esses headers ajuda a consumir APIs com mais segurança, interpretar respostas corretamente e preparar o estudo de autenticação, CORS e cookies.
