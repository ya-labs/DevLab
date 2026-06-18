# 1 - O que é autenticação?

Processo usado para descobrir quem é o usuário.

Na prática, ela responde esta pergunta?

> Quem está usando o sistema

Exemplo comum:

1 - O usuário informa e-mail e senha.
2 - O front-end envia esses dados para a API.
3 - A API valida se os dados estão corretos
4 - Caso estejam corretos, a API devolve uma forma de identificar esse usuário nas próximas requisições.

Autenticação não é a mesma coisa que autorização.

Autenticação:

> <span style="color: white;">Quem é você?</span>

Autorização:

> <span style="color: white;">Você tem permissão para isso?</span>

Exemplo:

Um usuário pode estar autenticado, mas não ter permissão para acessar uma área administrativa. Nesse caso, ele está logado, mas não autorizado.

---

# 2 - Por que autenticação existe?

Sem ela, qualquer pessoa poderia acessar qualquer dado da aplicação.

Por exemplo, uma tela de perfil:

```http
GET /profile
```

Se essa rota não tiver autenticação, qualquer usuário poderia tentar acessar dados privados.

Com autenticação, a API exige alguma prova de identidade, normalmente um token:

```http
GET /profile
Authorization: Bearer token_aqui
```

Assim, o servidor consegue identificar quem está fazendo a requisição.

---

# 3 - O que é JWT?

Significa JSON Web Token.

É um tipo de token muito usado para autenticação em APIs.

De forma simples, um JWT é uma string gerada pelo servidor depois que o usuário faz login. Essa string carrega informações que ajudam o servidor a reconhecer o usuário nas próximas requisições.

Exemplo visual de um JWT:

```txt
xxxxx.yyyyy.zzzzz
```

Ele costuma ter três partes:

- header: informações sobre o tipo de token e algoritmo usado;
- payload: dados sobre o usuário ou sessão;
- signature: assinatura usada para verificar se o token foi alterado.

O ponto importante aqui é:

> <span style="color: white;">O front-end não cria o JWT. Quem cria e valida o JWT é o back-end.</span>

---

# 4 - Fluxo básico com JWT

Fluxo comum:

1 - Usuário faz login.
2 - Front-end envia e-mail e senha para a API.
3 - API valida os dados.
4 - API gera um JWT.
5 - Front-end guarda o token.
6 - Front-end envia o token nas próximas requisições.
7 - API valida o token antes de devolver dados protegidos.

Exemplo de login:

```http
POST /auth/login
Content-Type: application/json

Body:
```JSON
{
    "email": "usuario@email.com",
    "password": "123456"
}
```

Resposta:

```json
{
    "token": "token_jwt_aqui"
}
```

Depois disso, o token deve ser enviado no header ``Authorization``.

---

# 5 - Enviando JWT nas requisições

Depois do login, o front-end usa o token para acessar rotas protegidas.

```js
async function buscarPerfil() {
    const response = await fetch("/api/profile", {
        method: "GET",
        headers: {
            Accept: "application/json",
            Authorization: `Bearer ${token}`
        }
    });

    if (!response.ok) {
        throw new Error("Erro ao buscar perfil");
    }

    return await response.json();
}
```

O header:
```http
Authorization: Bearer token_jwt_aqui
``` 

Segue o padrão Bearer Token.

`Bearer` indica que quem possui aquele token pode usá-lo para acessar o recurso, desde que ele seja válido.

---

# 6 - O que acontece no back-end?

Quando a API recebe uma requisição protegida, ela normalmente faz estes passos:

1 - Lê o header `Authorization`.
2 - Verifica se existe um token.
3 - Valida a assinatura do JWT.
4 - Verifica se o token expirou.
5 - Extrai as informações do usuário.
6 - Decide se o usuário pode acessar o recurso.

Exemplo conceitual:

```txt
Request -> Middleware de autenticação -> Controller -> Service -> Response
```

Em APIs reais, essa validação geralmente fica em middlewares, filters ou mecanismos próprios do framework.

# 7 - Payload do JWT

O payload pode carregar informações como:

```json
{
    "sub": "123",
    "name': "Nícolas",
    "role": "admin",
    "exp": 1712345678
}
```

Campos comuns: 

- `sub`: identificador do usuário.
- `name`: nome do usuário.
- `role`: perfil ou permissão do usuário.
- `exp`: data em timestamp de expiração do token.

Cuidado importante:
> <span style="color: white;">O payload do JWT não deve conter dados sensíveis.</span>

Mesmo que o token pareça embaralhado, o payload pode ser decodificado. Portanto, não coloque senha, CPF, dados bancários ou informações sigilosas dentro dele.

---

# 8 - Token assinado não é token criptografado

Um erro comum é achar que JWT é sempre criptografado.
Na maioria dos casos, é apenas ASSINADO.

Significa:

> <span style="color: white;">O servidor consegue verificar se o token foi alterado.</span>

Criptografado significa:

> <span style="color: white;">O conteúdo fica escondido para quem não tem a chave</span>

Na prática, um JWT comum pode ser lido, mas não pode ser alterado sem invalidar a assinatura.

---

# 9 - Expiração do token

Tokens geralmente têm tempo de validade.

Isso evita que um token roubado funcione para sempre.

Exemplo:

```json
{
    "token": "token_jwt_aqui",
    "expiresIn": 3600
}
```

Nesse exemplo, o token expira em 3600 segundos (1 hora).

Quando o token expira, a API pode retornar:

```http
401 unauthorized
```

No front-end, uma reação comum é:
- remover o token salvo;
- redirecionar o usuário para a tela de login;
- exibir mensagem de sesão expirada.

---

# 10 - Onde guardar o token no front-end

Existem algumas opções, cada uma com prós e contras:

### Memória da aplicação:

O token fica em uma variável ou estado global.

Pró:
- não persiste depois de carregar a página.

Contra:
- O usuário perde a sessão ao atualizar a página.

### LocalStorage

O token fica salvo no navegador.

Prós:
- simples de usar;
- persiste depois de recarregar a página.

Contras:
- Pode ser acessado por JavaScript;
- Se houver XSS, o token pode ser roubado.

### Cookie HttpOnly

O token ou sessão fica em cookie configurado pelo servidor.

Prós:
- JavaScript não consegue ler cookie HttpOnly;
- Mais seguro contra XSS.
Contra:
- Exige cuidado com CORS, `credentials`, SameSite e CSRF.

Para estudo de front-end, é comum começar entendendo `Authorization: Bearer token`. Depois vale aprofundar cookies, sessão e credentials.

