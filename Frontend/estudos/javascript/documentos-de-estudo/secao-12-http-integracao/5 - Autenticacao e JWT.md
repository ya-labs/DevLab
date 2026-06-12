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

> <span style="color: white; font-weight: 500">Quem é você?</span>

Autorização:

> <span style="color: white; font-weight: 500">Você tem permissão para isso?</span>

Exemplo:

Um usuário pode estar autenticado, mas não ter permissão para acessar uma área administrativa. Nesse caso, ele está logado, mas não autorizado.

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

> <span style="color: white; font-weight: 500">O front-end não cria o JWT. Quem cria e valida o JWT é o back-end.</span>

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