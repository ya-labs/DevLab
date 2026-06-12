# Cliente, servidor e API

## 1. O que e cliente

Cliente e quem faz uma requisicao para outro sistema.

Em desenvolvimento web, o cliente geralmente e:

- um navegador;
- uma aplicacao frontend;
- um aplicativo mobile;
- outro backend;
- uma ferramenta como Postman, Insomnia ou Swagger.

Exemplo:

```txt
O usuario abre uma tela de produtos.
O frontend precisa buscar a lista de produtos.
Nesse momento, o frontend atua como cliente.
```

O cliente nao precisa saber como o backend resolve tudo por dentro. Ele precisa saber para qual endereco enviar o pedido e qual formato de resposta esperar.

## 2. O que e servidor

Servidor e o sistema que recebe requisicoes, processa algo e devolve respostas.

No contexto de backend, o servidor e a aplicacao que fica rodando e esperando pedidos chegarem.

Exemplo:

```txt
Frontend pede: "me envie os produtos"
Servidor recebe o pedido
Servidor busca os produtos
Servidor responde com os dados
```

O servidor pode estar rodando localmente durante o desenvolvimento ou em um ambiente online em producao.

Exemplo local:

```txt
http://localhost:5000
```

Exemplo em producao:

```txt
https://api.minhaempresa.com
```

## 3. Como cliente e servidor se comunicam

Cliente e servidor se comunicam por meio de requisicoes e respostas.

Fluxo basico:

```txt
Cliente envia uma request
Servidor recebe a request
Servidor processa a request
Servidor envia uma response
Cliente usa a response
```

Esse modelo e importante porque backend normalmente nao "empurra" informacoes para o frontend o tempo todo. Na maioria dos casos, o frontend pede algo e o backend responde.

## 4. O que e API

API significa Application Programming Interface.

De forma simples, API e uma forma organizada de comunicacao entre sistemas.

Em uma aplicacao web, a API define quais pedidos o frontend pode fazer para o backend.

Exemplo:

```http
GET /produtos
```

Essa rota pode significar:

```txt
Buscar todos os produtos.
```

Outro exemplo:

```http
POST /produtos
```

Essa rota pode significar:

```txt
Criar um novo produto.
```

## 5. Por que o frontend nao acessa o banco diretamente

O frontend nao deve acessar o banco de dados diretamente porque isso seria inseguro e dificil de controlar.

Se o frontend acessasse o banco diretamente:

- credenciais poderiam ficar expostas;
- regras de negocio poderiam ser burladas;
- qualquer pessoa poderia tentar alterar dados;
- seria mais dificil controlar permissoes;
- a aplicacao ficaria mais fragil.

Por isso, o caminho correto geralmente e:

```txt
Frontend -> API -> Backend -> Banco de dados
```

E a resposta volta assim:

```txt
Banco de dados -> Backend -> API -> Frontend
```

O backend funciona como uma camada de protecao e organizacao.

## 6. API como contrato

Uma API tambem funciona como um contrato entre sistemas.

Esse contrato define:

- quais rotas existem;
- quais metodos HTTP podem ser usados;
- quais dados devem ser enviados;
- qual resposta sera devolvida;
- quais erros podem acontecer.

Exemplo de contrato simples:

```txt
Rota: POST /produtos
Objetivo: criar um produto
Body esperado: nome e preco
Resposta de sucesso: 201 Created
Resposta de erro: 400 Bad Request
```

Esse contrato ajuda frontend e backend a trabalharem juntos.

## 7. Exemplo pratico

Imagine um cadastro de produto.

Fluxo completo:

```txt
1. Usuario preenche nome e preco no frontend.
2. Frontend envia uma requisicao POST para /produtos.
3. API recebe a requisicao.
4. Backend valida se nome e preco foram enviados.
5. Backend salva o produto.
6. Backend devolve uma resposta.
7. Frontend mostra a mensagem para o usuario.
```

Request:

```http
POST /produtos
Content-Type: application/json
```

Body:

```json
{
    "nome": "Teclado",
    "preco": 199.90
}
```

Response:

```json
{
    "id": 1,
    "nome": "Teclado",
    "preco": 199.90
}
```

## 8. Erros comuns de entendimento

Um erro comum e pensar que API e sempre backend.

API e a interface de comunicacao. O backend e o sistema que executa a logica por tras dessa interface.

Outro erro comum e pensar que servidor significa apenas uma maquina fisica.

Na pratica, quando estudamos backend, "servidor" muitas vezes significa a aplicacao rodando e escutando requisicoes.

## 9. Relacao com outros conteudos

Este assunto se conecta diretamente com:

```txt
Frontend/estudos/javascript/documentos-de-estudo/secao-12-http-integracao/1 - Fetch API.md
Frontend/estudos/javascript/documentos-de-estudo/secao-12-http-integracao/2 - REST API.md
```

No frontend, voce aprende a fazer requisicoes.

No backend, voce aprende a receber essas requisicoes e responder corretamente.

## Conclusao

Cliente e quem faz o pedido. Servidor e quem recebe, processa e responde. API e a forma organizada dessa comunicacao acontecer.

Entender esse fluxo e essencial antes de entrar em C#, .NET e ASP.NET Core.
