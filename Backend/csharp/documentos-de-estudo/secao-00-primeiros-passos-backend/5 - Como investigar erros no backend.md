# Como investigar erros no backend

## 1. O que significa investigar um erro

Investigar um erro no backend e descobrir onde o comportamento real ficou diferente do comportamento esperado.

Exemplo:

```txt
Esperado:
Cadastrar um produto e receber sucesso.

Real:
A API retorna erro 400.
```

O trabalho do desenvolvedor e entender por que isso aconteceu.

## 2. Por que erros acontecem no backend

Erros podem acontecer por varios motivos:

- rota errada;
- metodo HTTP incorreto;
- dados invalidos;
- regra de negocio descumprida;
- usuario sem permissao;
- falha no banco de dados;
- erro no codigo;
- configuracao incorreta;
- servico externo fora do ar.

O ponto importante e nao tentar corrigir no chute.

Primeiro, entenda onde o erro esta acontecendo.

## 3. Roteiro simples de investigacao

Um caminho pratico:

```txt
1. A API esta rodando?
2. A requisicao chegou no backend?
3. A rota esta correta?
4. O metodo HTTP esta correto?
5. Os dados enviados estao corretos?
6. Qual status HTTP foi retornado?
7. Existe mensagem de erro?
8. O erro apareceu nos logs?
9. O problema esta na entrada, na regra, no banco ou na resposta?
```

Esse roteiro evita perder tempo olhando a parte errada do sistema.

## 4. Verificar se a API esta rodando

Antes de investigar a regra de negocio, verifique se a aplicacao esta ligada.

Exemplo:

```txt
API esperada:
http://localhost:5000
```

Se a API nao estiver rodando, qualquer chamada para ela vai falhar.

Esse erro pode aparecer como:

```txt
Failed to fetch
Connection refused
Unable to connect
```

Nesse caso, o problema nao e a regra do endpoint. O backend simplesmente nao esta respondendo.

## 5. Verificar rota e metodo HTTP

Uma rota errada pode gerar `404 Not Found`.

Exemplo:

```http
GET /produtos
```

Se o backend so tiver esta rota:

```http
GET /products
```

A chamada para `/produtos` nao vai encontrar nada.

Tambem existe erro de metodo.

Exemplo:

```http
GET /produtos
POST /produtos
```

Essas duas chamadas usam a mesma rota, mas fazem coisas diferentes.

Se voce usa `GET` quando deveria usar `POST`, a API pode nao encontrar um endpoint compativel.

## 6. Entender o status HTTP

O status HTTP ajuda a identificar o tipo do problema.

Exemplos:

- `400 Bad Request`: os dados enviados estao invalidos;
- `401 Unauthorized`: o usuario nao esta autenticado;
- `403 Forbidden`: o usuario nao tem permissao;
- `404 Not Found`: rota ou recurso nao encontrado;
- `500 Internal Server Error`: erro interno no backend.

Exemplo:

```txt
Se uma API retorna 400 ao cadastrar produto,
o primeiro lugar para olhar sao os dados enviados.
```

Exemplo:

```txt
Se uma API retorna 500,
o primeiro lugar para olhar sao logs, excecoes e codigo interno.
```

## 7. Verificar dados enviados

Muitos erros acontecem porque o cliente envia dados incompletos ou no formato errado.

Exemplo esperado:

```json
{
    "nome": "Mouse",
    "preco": 99.90
}
```

Exemplo com erro:

```json
{
    "nome": "",
    "preco": -10
}
```

Possiveis problemas:

- nome vazio;
- preco negativo;
- campo obrigatorio ausente;
- tipo de dado errado;
- JSON mal formatado.

O backend deve validar esses dados e devolver uma resposta clara.

## 8. Logs

Logs sao registros que ajudam a entender o que aconteceu na aplicacao.

Eles podem mostrar:

- qual endpoint foi chamado;
- qual erro ocorreu;
- qual excecao foi disparada;
- qual etapa do fluxo foi executada;
- qual operacao falhou.

Exemplo conceitual de log:

```txt
Erro ao cadastrar produto: preco invalido.
```

Logs sao importantes porque nem todo erro aparece claramente para o usuario.

## 9. Debug

Debug e o processo de acompanhar o codigo em execucao para entender o comportamento da aplicacao.

No backend, debug pode envolver:

- colocar breakpoints;
- acompanhar a chegada da requisicao;
- verificar valores de variaveis;
- entender qual condicao foi executada;
- identificar onde uma excecao aconteceu.

Exemplo:

```txt
O produto chega no endpoint?
O nome esta preenchido?
O preco esta correto?
A validacao passou?
O metodo de salvar foi chamado?
A resposta foi montada corretamente?
```

Esse tipo de pergunta ajuda a rastrear o problema passo a passo.

## 10. Ferramentas para testar backend

Algumas ferramentas comuns:

- Swagger;
- Postman;
- Insomnia;
- navegador, para chamadas simples `GET`;
- terminal, usando ferramentas como `curl`.

Essas ferramentas ajudam a testar a API sem depender do frontend.

Isso e importante porque, se um erro acontece na tela, voce precisa descobrir se o problema esta no frontend ou no backend.

## 11. Exemplo de investigacao

Problema:

```txt
Ao cadastrar produto, a API retorna 400 Bad Request.
```

Investigacao:

```txt
1. A API esta rodando? Sim.
2. A rota esta correta? POST /produtos.
3. O metodo esta correto? Sim.
4. O body foi enviado? Sim.
5. O JSON esta correto? Sim.
6. Os dados sao validos? Nao, o preco esta negativo.
```

Conclusao:

```txt
O erro nao esta na rota.
O erro esta nos dados enviados.
```

## 12. Erros comuns ao investigar

Erros comuns:

- olhar o frontend antes de testar a API diretamente;
- ignorar o status HTTP;
- nao ler a mensagem de erro;
- nao verificar se a API esta rodando;
- testar a rota errada;
- alterar varias coisas ao mesmo tempo;
- corrigir sem entender a causa.

Uma investigacao boa muda uma coisa por vez e confirma o resultado.

## 13. Relacao com proximas secoes

Este assunto sera usado em toda a trilha backend.

Ele aparece quando voce estudar:

- C#;
- tratamento de erros;
- ASP.NET Core;
- controllers;
- services;
- banco de dados;
- autenticacao;
- testes de API.

Investigar erros e uma habilidade continua. Nao e apenas um topico isolado.

## Conclusao

Investigar erros no backend exige metodo.

Primeiro confirme se a API esta rodando. Depois verifique rota, metodo, dados enviados, status HTTP, logs e comportamento do codigo.

Quanto mais organizado for o processo de investigacao, mais facil fica encontrar a causa real do problema.
