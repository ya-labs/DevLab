# HTTP, request e response

## 1. O que e HTTP

HTTP e o protocolo mais usado para comunicacao entre cliente e servidor na web.

Ele funciona com um modelo de pedido e resposta.

```txt
Cliente envia uma request
Servidor devolve uma response
```

Quando um frontend chama uma API, ele normalmente esta fazendo uma requisicao HTTP.

Exemplo:

```http
GET /produtos
```

Essa requisicao pede ao backend a lista de produtos.

## 2. Por que HTTP existe

HTTP existe para padronizar a comunicacao na web.

Sem um padrao, cada sistema poderia enviar dados de um jeito diferente, dificultando a integracao entre navegadores, servidores, APIs e aplicacoes.

Com HTTP, cliente e servidor conseguem se comunicar usando elementos conhecidos:

- URL;
- metodo HTTP;
- headers;
- body;
- status code;
- response body.

## 3. O que e request

Request e a requisicao enviada pelo cliente para o servidor.

Ela representa uma intencao.

Exemplos:

```txt
Buscar produtos
Criar usuario
Alterar pedido
Remover tarefa
Fazer login
```

Uma request normalmente contem:

- metodo HTTP;
- URL;
- headers;
- body, quando necessario.

## 4. Metodo HTTP

Metodo HTTP indica o tipo de acao que o cliente quer executar.

Principais metodos:

- `GET`: buscar dados;
- `POST`: criar dados;
- `PUT`: atualizar um recurso inteiro;
- `PATCH`: atualizar parte de um recurso;
- `DELETE`: remover um recurso.

Exemplos:

```http
GET /produtos
```

Busca produtos.

```http
POST /produtos
```

Cria produto.

```http
DELETE /produtos/10
```

Remove o produto com id `10`.

## 5. URL

URL e o endereco acessado pelo cliente.

Exemplo:

```txt
http://localhost:5000/produtos
```

Partes importantes:

```txt
http://localhost:5000 -> endereco base da API
/produtos             -> rota acessada
```

Em APIs, a URL geralmente representa um recurso.

Exemplos:

```txt
/produtos
/usuarios
/pedidos
/tarefas
```

## 6. Headers

Headers sao informacoes extras enviadas na request ou na response.

Eles nao sao o conteudo principal, mas ajudam o servidor e o cliente a entenderem detalhes da comunicacao.

Exemplo:

```http
Content-Type: application/json
```

Esse header informa que os dados enviados estao em JSON.

Outro exemplo:

```http
Authorization: Bearer token
```

Esse header pode ser usado para enviar um token de autenticacao.

Neste momento, o importante e entender que headers carregam metadados da comunicacao.

## 7. Body

Body e o corpo da requisicao ou da resposta.

Em uma request, o body costuma carregar dados enviados pelo cliente.

Exemplo:

```http
POST /produtos
Content-Type: application/json
```

```json
{
    "nome": "Mouse",
    "preco": 99.90
}
```

Nesse caso, o body contem os dados do produto que sera criado.

Requisicoes `GET` normalmente nao usam body.

## 8. O que e response

Response e a resposta que o servidor devolve depois de processar uma request.

Uma response normalmente contem:

- status code;
- headers;
- body.

Exemplo:

```http
201 Created
Content-Type: application/json
```

```json
{
    "id": 1,
    "nome": "Mouse",
    "preco": 99.90
}
```

Essa resposta informa que o produto foi criado com sucesso.

## 9. Status code

Status code e um numero que indica o resultado da requisicao.

Exemplos comuns:

- `200 OK`: deu certo;
- `201 Created`: algo foi criado;
- `400 Bad Request`: dados invalidos;
- `401 Unauthorized`: usuario nao autenticado;
- `403 Forbidden`: usuario sem permissao;
- `404 Not Found`: recurso nao encontrado;
- `500 Internal Server Error`: erro interno no servidor.

Nesta secao, o objetivo e entender a ideia geral.

O aprofundamento de status HTTP ja aparece em:

```txt
Frontend/estudos/javascript/documentos-de-estudo/secao-12-http-integracao/3 - Status HTTP.md
```

## 10. JSON

JSON e um formato muito usado para enviar e receber dados em APIs.

Exemplo:

```json
{
    "id": 1,
    "nome": "Nicolas",
    "email": "nicolas@email.com"
}
```

Ele parece um objeto JavaScript, mas e um formato de texto.

No backend, esse JSON pode ser convertido para objetos da linguagem usada, como C#.

No frontend, esse JSON pode ser lido e usado para atualizar a tela.

## 11. Exemplo completo

Request:

```http
POST /tarefas
Content-Type: application/json
```

Body da request:

```json
{
    "titulo": "Estudar backend"
}
```

Response:

```http
201 Created
Content-Type: application/json
```

Body da response:

```json
{
    "id": 1,
    "titulo": "Estudar backend",
    "concluida": false
}
```

Fluxo:

```txt
Cliente pediu para criar uma tarefa.
Servidor recebeu os dados.
Servidor criou a tarefa.
Servidor respondeu com status 201 e os dados criados.
```

## 12. Erros comuns

Um erro comum e achar que toda requisicao HTTP que chega no backend esta correta.

Na pratica, o backend precisa validar tudo.

Outro erro comum e ignorar o status code e olhar apenas o body.

Em uma API bem feita, o status code ajuda a entender rapidamente se a operacao deu certo ou falhou.

## Conclusao

HTTP e a base da comunicacao entre cliente e servidor na web.

Request e o pedido enviado pelo cliente. Response e a resposta enviada pelo servidor.

Entender URL, metodo, headers, body e status code e essencial antes de criar uma API com ASP.NET Core.
