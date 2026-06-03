# Promises, async e programação assíncrona

Programação assíncrona é a forma de lidar com operações que não terminam imediatamente.

Ela é essencial em JavaScript porque muitas tarefas do dia a dia dependem de tempo externo: requisições HTTP, timers, leitura de arquivos, acesso a banco de dados e interação com APIs.

---

# 1 - O que é programação assíncrona

Código síncrono executa uma linha depois da outra, esperando cada uma terminar.

```js
console.log("Início");
console.log("Fim");
```

Código assíncrono permite iniciar uma operação e continuar executando outras coisas enquanto ela termina.

```js
console.log("Início");

setTimeout(function() {
    console.log("Meio");
}, 1000);

console.log("Fim");
```

Saída:

```txt
Início
Fim
Meio
```

O JavaScript não ficou parado esperando o `setTimeout`.

---

# 2 - Por que assincronismo existe

Assincronismo evita que a aplicação trave enquanto espera uma operação demorada.

Exemplos comuns:

- buscar dados em uma API;
- enviar formulário;
- carregar imagem;
- esperar timer;
- consultar banco no backend;
- ler arquivo no Node.js.

Sem assincronismo, uma tela poderia congelar toda vez que precisasse esperar uma resposta do servidor.

---

# 3 - Callbacks

Callback é uma função passada como argumento para ser executada depois.

```js
function buscarDados(callback) {
    setTimeout(function() {
        callback("Dados carregados");
    }, 1000);
}

buscarDados(function(resultado) {
    console.log(resultado);
});
```

Callbacks funcionam, mas podem ficar difíceis de manter quando várias operações dependem uma da outra.

```js
buscarUsuario(function(usuario) {
    buscarPedidos(usuario.id, function(pedidos) {
        buscarPagamento(pedidos[0].id, function(pagamento) {
            console.log(pagamento);
        });
    });
});
```

Esse problema é conhecido como callback hell.

---

# 4 - O que é uma Promise

Uma Promise é um objeto que representa um valor que pode estar disponível no futuro.

Ela pode estar em três estados:

- `pending`: ainda não terminou;
- `fulfilled`: terminou com sucesso;
- `rejected`: terminou com erro.

Exemplo:

```js
const promessa = new Promise(function(resolve, reject) {
    const sucesso = true;

    if (sucesso) {
        resolve("Deu certo");
    } else {
        reject("Deu erro");
    }
});
```

Para consumir:

```js
promessa
    .then(function(resultado) {
        console.log(resultado);
    })
    .catch(function(erro) {
        console.log(erro);
    });
```

---

# 5 - then, catch e finally

`then` executa quando a Promise resolve.

`catch` executa quando a Promise rejeita.

`finally` executa no final, independentemente de sucesso ou erro.

```js
buscarUsuario()
    .then(function(usuario) {
        console.log(usuario);
    })
    .catch(function(error) {
        console.error(error);
    })
    .finally(function() {
        console.log("Finalizou");
    });
```

Na prática, `finally` é útil para desligar loading, liberar recurso ou executar limpeza.

---

# 6 - async e await

`async/await` é uma forma mais legível de trabalhar com Promises.

```js
async function carregarUsuario() {
    const usuario = await buscarUsuario();

    console.log(usuario);
}
```

`await` pausa a execução da função `async` até a Promise terminar.

Importante:

> O `await` pausa a função atual, não trava o navegador inteiro.

---

# 7 - Tratando erros com async/await

Com `async/await`, o tratamento de erro geralmente usa `try/catch`.

```js
async function carregarUsuario() {
    try {
        const usuario = await buscarUsuario();

        console.log(usuario);
    } catch (error) {
        console.error("Erro ao carregar usuário", error);
    }
}
```

Esse formato é muito usado em código real porque deixa o fluxo mais linear.

---

# 8 - Exemplo com Fetch API

```js
async function buscarProdutos() {
    const response = await fetch("/api/produtos");

    if (!response.ok) {
        throw new Error("Erro ao buscar produtos");
    }

    const produtos = await response.json();

    return produtos;
}
```

O que acontece:

- `fetch` retorna uma Promise;
- `await` espera a resposta HTTP;
- `response.ok` valida o status;
- `response.json()` também retorna uma Promise;
- a função retorna os dados convertidos.

Esse assunto se conecta com `Frontend/estudos/javascript/documentos-de-estudo/secao-12-http-integracao/1 - Fetch API.md`.

---

# 9 - Promise.all

`Promise.all` executa várias Promises em paralelo e espera todas terminarem.

```js
async function carregarTela() {
    const [usuario, pedidos] = await Promise.all([
        buscarUsuario(),
        buscarPedidos()
    ]);

    return {
        usuario,
        pedidos
    };
}
```

Use quando as operações não dependem uma da outra.

Se uma Promise falhar, o `Promise.all` rejeita.

---

# 10 - Exemplo prático completo

```js
async function carregarResumoUsuario(idUsuario) {
    try {
        const usuarioResponse = await fetch(`/api/usuarios/${idUsuario}`);

        if (!usuarioResponse.ok) {
            throw new Error("Usuário não encontrado");
        }

        const usuario = await usuarioResponse.json();

        const pedidosResponse = await fetch(`/api/usuarios/${idUsuario}/pedidos`);

        if (!pedidosResponse.ok) {
            throw new Error("Erro ao buscar pedidos");
        }

        const pedidos = await pedidosResponse.json();

        return {
            usuario,
            totalPedidos: pedidos.length
        };
    } catch (error) {
        console.error(error);
        throw error;
    }
}
```

Esse fluxo é comum em aplicações reais: buscar dados, validar status, converter resposta e tratar erro.

---

# 11 - Erros comuns

### Esquecer o await

```js
const response = fetch("/api/produtos");

console.log(response); // Promise
```

### Achar que fetch cai no catch em status 404

```js
const response = await fetch("/api/produtos");
```

O `fetch` só rejeita em erro de rede. Status HTTP como `404` e `500` precisam ser tratados com `response.ok`.

### Usar await em sequência quando poderia usar paralelo

Se uma chamada não depende da outra, `Promise.all` pode ser melhor.

---

# 12 - Relação com outros estudos

Assincronismo se conecta com funções, callbacks, Fetch API, eventos, DOM e consumo de APIs REST.

Antes de estudar Fetch com profundidade, é importante entender que `fetch` retorna Promise.

---

# 13 - Conclusão

Promises e `async/await` são a base do JavaScript assíncrono moderno.

Dominar esse assunto permite consumir APIs, tratar erros corretamente e escrever fluxos assíncronos mais legíveis e próximos do código usado no mercado.
