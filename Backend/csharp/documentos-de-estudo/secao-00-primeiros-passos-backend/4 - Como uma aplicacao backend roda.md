# Como uma aplicacao backend roda

## 1. O que significa uma aplicacao backend rodar

Uma aplicacao backend precisa estar em execucao para receber requisicoes.

Diferente de um arquivo HTML simples, que pode ser aberto diretamente no navegador, uma API precisa iniciar um processo.

Esse processo fica aguardando requisicoes chegarem.

Exemplo:

```txt
A API inicia.
A API escuta uma porta.
O cliente envia uma requisicao.
A API processa a requisicao.
A API devolve uma resposta.
```

## 2. O que e localhost

`localhost` representa a propria maquina onde a aplicacao esta rodando.

Durante os estudos, e comum rodar o backend localmente.

Exemplo:

```txt
http://localhost:5000
```

Isso significa:

```txt
A aplicacao esta rodando no computador atual.
Ela esta ouvindo requisicoes na porta 5000.
```

Quando o frontend chama essa URL, ele esta tentando se comunicar com uma aplicacao local.

## 3. O que e porta

Porta e um numero usado para identificar onde uma aplicacao esta escutando requisicoes.

Exemplo:

```txt
http://localhost:5000
http://localhost:3000
http://localhost:5173
```

Cada aplicacao pode usar uma porta diferente.

Exemplo comum:

```txt
Frontend rodando em: http://localhost:5173
Backend rodando em:  http://localhost:5000
```

Assim, frontend e backend podem rodar ao mesmo tempo na mesma maquina, desde que usem portas diferentes.

## 4. O que acontece quando a API inicia

Quando uma API backend inicia, ela prepara algumas coisas:

- configuracoes da aplicacao;
- rotas disponiveis;
- servicos internos;
- conexoes necessarias;
- porta onde vai escutar requisicoes.

Em uma API .NET, esses detalhes aparecem mais para frente em arquivos como `Program.cs`.

Nesta secao, o foco e entender o conceito.

## 5. O que e rota

Rota e o caminho usado para acessar uma funcionalidade da API.

Exemplo:

```txt
/produtos
```

Se a API esta rodando em:

```txt
http://localhost:5000
```

E a rota e:

```txt
/produtos
```

A URL completa fica:

```txt
http://localhost:5000/produtos
```

## 6. Fluxo de uma requisicao dentro do backend

Fluxo simplificado:

```txt
1. Cliente envia uma requisicao.
2. Backend recebe a requisicao.
3. Backend identifica a rota.
4. Backend executa o codigo responsavel.
5. Backend aplica validacoes e regras.
6. Backend monta uma resposta.
7. Backend devolve a resposta ao cliente.
```

Exemplo:

```http
GET /produtos
```

O backend precisa identificar que essa rota representa uma busca de produtos.

Depois, ele executa a logica relacionada a essa busca.

## 7. Aplicacao local e aplicacao em producao

Aplicacao local e a que roda na maquina do desenvolvedor.

Exemplo:

```txt
http://localhost:5000
```

Aplicacao em producao e a que roda em um servidor real, acessivel por usuarios ou outros sistemas.

Exemplo:

```txt
https://api.sistema.com
```

A ideia principal e a mesma:

```txt
Aplicacao roda
Escuta requisicoes
Processa pedidos
Devolve respostas
```

A diferenca e o ambiente onde ela esta hospedada.

## 8. Por que isso importa

Entender como uma aplicacao backend roda evita confusoes comuns.

Exemplos:

- se a API nao estiver iniciada, o frontend nao consegue se comunicar com ela;
- se a porta estiver errada, a requisicao nao chega;
- se a rota estiver errada, pode retornar `404 Not Found`;
- se a API travar, ela para de responder;
- se frontend e backend estiverem em enderecos diferentes, podem surgir problemas de CORS.

Esse entendimento ajuda a investigar erros de forma mais organizada.

## 9. Exemplo pratico

Imagine uma API rodando em:

```txt
http://localhost:5000
```

Ela possui a rota:

```http
GET /tarefas
```

A URL completa para buscar tarefas seria:

```txt
http://localhost:5000/tarefas
```

Se a API estiver desligada, essa chamada falha.

Se a API estiver ligada, mas a rota nao existir, a resposta pode ser `404 Not Found`.

Se a rota existir e funcionar, a resposta pode ser `200 OK`.

## 10. Relacao com .NET

Quando voce estudar ASP.NET Core, esse conceito vai aparecer na pratica.

Voce vai ver:

- como iniciar uma API;
- como configurar rotas;
- como criar endpoints;
- como retornar respostas;
- como testar a API no navegador, Swagger, Postman ou Insomnia.

Por enquanto, o objetivo e entender o fluxo geral antes de entrar no codigo.

## Conclusao

Uma aplicacao backend precisa estar rodando para receber requisicoes.

Ela escuta uma porta, recebe pedidos por rotas, executa codigo e devolve respostas.

Esse conceito prepara o terreno para entender APIs em ASP.NET Core.
