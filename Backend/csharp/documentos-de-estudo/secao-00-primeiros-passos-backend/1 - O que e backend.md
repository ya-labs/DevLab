# O que e backend

## 1. O que e

Backend e a parte de uma aplicacao responsavel por processar dados, aplicar regras, acessar banco de dados e devolver respostas para outros sistemas.

Em uma aplicacao web, o usuario normalmente interage com o frontend: tela, botoes, formularios, menus e mensagens visuais.

O backend fica por tras dessa interface. Ele recebe pedidos, decide o que deve acontecer e responde com o resultado.

Exemplo simples:

```txt
Usuario preenche um formulario
Frontend envia os dados
Backend recebe os dados
Backend valida as informacoes
Backend salva no banco
Backend devolve uma resposta
Frontend mostra o resultado na tela
```

## 2. Por que backend existe

O backend existe porque nem tudo deve ou pode acontecer no navegador do usuario.

Algumas responsabilidades precisam ficar em um ambiente controlado, como:

- validar dados importantes;
- salvar informacoes em banco de dados;
- autenticar usuarios;
- proteger regras do sistema;
- integrar com outros servicos;
- processar pagamentos;
- enviar emails;
- controlar permissoes;
- registrar logs;
- devolver dados para o frontend.

Se tudo ficasse no frontend, qualquer pessoa poderia abrir o navegador, inspecionar o codigo e alterar regras importantes.

Por exemplo, em uma loja online, o frontend pode mostrar o preco de um produto, mas a decisao final sobre o valor correto da compra precisa passar pelo backend.

## 3. Backend no uso real

Em sistemas reais, o backend aparece em tarefas como:

- login de usuario;
- cadastro de produto;
- listagem de pedidos;
- alteracao de senha;
- envio de notificacao;
- consulta de estoque;
- geracao de relatorio;
- pagamento de compra;
- permissao de acesso a uma area restrita.

Exemplo:

```txt
Um usuario tenta fazer login.

O frontend envia email e senha.
O backend verifica se o usuario existe.
O backend compara a senha enviada com a senha salva de forma segura.
O backend gera uma resposta dizendo se o login foi aceito ou recusado.
```

O ponto importante e que o backend nao existe apenas para "guardar dados". Ele tambem decide se uma acao faz sentido dentro das regras do sistema.

## 4. Diferenca entre frontend e backend

Frontend e a parte da aplicacao que o usuario ve e usa diretamente.

Backend e a parte da aplicacao que processa dados e regras no servidor.

Exemplo em um sistema de produtos:

```txt
Frontend:
- mostra a lista de produtos;
- exibe formulario de cadastro;
- mostra mensagem de sucesso ou erro;
- envia requisicoes para a API.

Backend:
- recebe a requisicao;
- valida nome e preco;
- verifica se o produto ja existe;
- salva no banco;
- devolve status e dados.
```

O frontend se preocupa com experiencia visual e interacao.

O backend se preocupa com processamento, seguranca, regras e persistencia dos dados.

## 5. Responsabilidades comuns do backend

As responsabilidades mais comuns sao:

- receber requisicoes;
- interpretar rotas;
- validar entrada de dados;
- executar regras de negocio;
- acessar banco de dados;
- retornar respostas padronizadas;
- tratar erros;
- autenticar e autorizar usuarios;
- integrar sistemas externos;
- registrar informacoes importantes em logs.

Exemplo de regra de negocio:

```txt
Um produto nao pode ser cadastrado com preco menor ou igual a zero.
```

Mesmo que o frontend tente bloquear esse erro na tela, o backend tambem precisa validar. O frontend pode ser burlado. O backend precisa ser a camada confiavel.

## 6. O que backend nao e

Backend nao e apenas "banco de dados".

Backend tambem nao e apenas "API".

Uma API pode fazer parte do backend, mas backend e um conjunto maior de responsabilidades.

De forma simples:

```txt
API = forma de comunicacao
Backend = sistema que processa a comunicacao e executa regras
Banco de dados = lugar onde as informacoes ficam armazenadas
```

Essas partes trabalham juntas, mas nao sao a mesma coisa.

## 7. Exemplo completo

Imagine um sistema de tarefas.

O usuario quer criar uma nova tarefa chamada "Estudar C#".

Fluxo:

```txt
1. Usuario digita o nome da tarefa no frontend.
2. Frontend envia uma requisicao para o backend.
3. Backend verifica se o nome da tarefa foi enviado.
4. Backend cria a tarefa.
5. Backend salva a tarefa no banco.
6. Backend devolve a tarefa criada.
7. Frontend atualiza a tela.
```

Resposta que o backend poderia devolver:

```json
{
    "id": 1,
    "titulo": "Estudar C#",
    "concluida": false
}
```

## 8. Relacao com outros conteudos

Este assunto se conecta com REST API, que ja aparece em:

```txt
Frontend/estudos/javascript/documentos-de-estudo/secao-12-http-integracao/2 - REST API.md
```

Aqui o foco e entender o papel do backend.

Na parte de frontend, o foco e entender como consumir uma API.

Na parte de backend, o foco sera entender como criar essa API.

## Conclusao

Backend e a parte da aplicacao que recebe pedidos, processa regras, acessa dados e devolve respostas.

Nesta primeira etapa, o mais importante e entender o papel do backend dentro do sistema. Os detalhes tecnicos, como C#, .NET, controllers, services e banco de dados, entram melhor nas proximas secoes.
