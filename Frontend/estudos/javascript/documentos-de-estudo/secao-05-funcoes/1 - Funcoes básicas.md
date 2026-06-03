# Funções básicas em JavaScript

Funções são blocos de código reutilizáveis que executam uma tarefa.

Elas ajudam a organizar o código, evitar repetição e separar responsabilidades. Em projetos reais, funções aparecem em validações, cálculos, eventos, requisições, componentes, serviços e regras de negócio.

---

# 1 - O que é uma função

Uma função é um bloco de código que pode ser criado uma vez e executado várias vezes.

Exemplo:

```js
function saudacao() {
    console.log("Olá");
}

saudacao();
```

Nesse exemplo:

- `function` declara a função;
- `saudacao` é o nome da função;
- o bloco `{}` contém o código executado;
- `saudacao()` chama a função.

Criar uma função não executa ela automaticamente. Ela só roda quando é chamada.

---

# 2 - Por que funções existem

Sem funções, o código fica repetitivo.

```js
console.log("Bem-vindo");
console.log("Bem-vindo");
console.log("Bem-vindo");
```

Com função:

```js
function mostrarMensagem() {
    console.log("Bem-vindo");
}

mostrarMensagem();
mostrarMensagem();
mostrarMensagem();
```

Se a mensagem precisar mudar, basta alterar em um único lugar.

Funções existem para:

- evitar repetição;
- dar nome a uma regra;
- organizar responsabilidades;
- facilitar manutenção;
- facilitar testes;
- dividir problemas grandes em partes menores.

---

# 3 - Parâmetros e argumentos

Parâmetros são variáveis declaradas na função.

Argumentos são os valores enviados na chamada.

```js
function saudar(nome) {
    console.log(`Olá, ${nome}`);
}

saudar("Nícolas");
saudar("Ana");
```

Nesse exemplo:

- `nome` é o parâmetro;
- `"Nícolas"` e `"Ana"` são argumentos.

Funções podem receber mais de um parâmetro.

```js
function somar(a, b) {
    return a + b;
}

console.log(somar(2, 3)); // 5
```

---

# 4 - Retorno de função

O `return` define o valor que a função devolve.

```js
function calcularTotal(preco, quantidade) {
    return preco * quantidade;
}

const total = calcularTotal(20, 3);

console.log(total); // 60
```

Sem `return`, a função retorna `undefined`.

```js
function mostrarNome(nome) {
    console.log(nome);
}

const resultado = mostrarNome("Nícolas");

console.log(resultado); // undefined
```

Use `return` quando a função precisa entregar um resultado para outro ponto do código.

---

# 5 - Funções com responsabilidade clara

Uma função deve ter uma intenção fácil de entender.

Exemplo ruim:

```js
function processar(usuario) {
    console.log(usuario.nome);
    usuario.ativo = true;
    return usuario.idade >= 18;
}
```

Essa função faz coisas demais: imprime, altera objeto e valida idade.

Versão melhor:

```js
function ativarUsuario(usuario) {
    return {
        ...usuario,
        ativo: true
    };
}

function usuarioMaiorDeIdade(usuario) {
    return usuario.idade >= 18;
}
```

Funções pequenas e claras são mais fáceis de ler, testar e manter.

---

# 6 - Function declaration e function expression

Function declaration:

```js
function somar(a, b) {
    return a + b;
}
```

Function expression:

```js
const somar = function(a, b) {
    return a + b;
};
```

As duas criam funções, mas possuem diferenças de hoisting.

Na prática, para funções comuns nomeadas, `function nome()` é simples e legível. Para funções usadas como valor, callback ou configuração, function expression também aparece bastante.

---

# 7 - Arrow functions

Arrow function é uma sintaxe mais curta para escrever funções.

```js
const somar = (a, b) => {
    return a + b;
};
```

Quando há apenas uma expressão, o retorno pode ser implícito.

```js
const somar = (a, b) => a + b;
```

Muito comum em métodos de array:

```js
const numeros = [1, 2, 3];

const dobrados = numeros.map((numero) => numero * 2);

console.log(dobrados); // [2, 4, 6]
```

Arrow functions têm diferença importante em relação ao `this`. Esse ponto é aprofundado em `Frontend/estudos/javascript/documentos-de-estudo/secao-05-funcoes/2 - Funções avançado.md`.

---

# 8 - Callbacks

Callback é uma função passada como argumento para outra função.

```js
function executar(callback) {
    callback();
}

executar(function() {
    console.log("Executou depois");
});
```

Callbacks aparecem muito em:

- eventos;
- timers;
- métodos de array;
- código assíncrono;
- bibliotecas.

Exemplo com array:

```js
const nomes = ["Ana", "Carlos", "Marina"];

nomes.forEach(function(nome) {
    console.log(nome);
});
```

---

# 9 - Exemplo prático completo

```js
function calcularTotalItens(itens) {
    return itens.reduce(function(total, item) {
        return total + item.preco * item.quantidade;
    }, 0);
}

function criarResumoPedido(cliente, itens) {
    const total = calcularTotalItens(itens);

    return {
        cliente,
        quantidadeItens: itens.length,
        total
    };
}

const itens = [
    { nome: "Arroz", preco: 20, quantidade: 2 },
    { nome: "Feijão", preco: 12, quantidade: 1 }
];

const resumo = criarResumoPedido("Nícolas", itens);

console.log(resumo);
```

Esse exemplo separa responsabilidades:

- uma função calcula o total;
- outra monta o resumo do pedido.

---

# 10 - Erros comuns

### Criar função com nome genérico

```js
function executar(dados) {
    return dados.valor * 2;
}
```

Prefira nomes que expliquem a intenção.

```js
function calcularValorDobrado(valor) {
    return valor * 2;
}
```

### Esquecer o return

```js
function somar(a, b) {
    a + b;
}

console.log(somar(2, 3)); // undefined
```

### Fazer função grande demais

Se a função valida, altera, salva, renderiza e envia dados, provavelmente ela precisa ser dividida.

---

# 11 - Relação com outros estudos

Funções se conectam com arrays, porque métodos como `map`, `filter`, `find` e `reduce` recebem funções.

Também se conectam com assincronismo, porque callbacks, Promises e `async/await` dependem da ideia de passar e retornar funções.

Antes de avançar para funções avançadas, vale dominar parâmetros, retorno, callbacks e responsabilidade clara.

---

# 12 - Conclusão

Funções são uma das ferramentas mais importantes para escrever código organizado.

Elas permitem transformar regras soltas em blocos nomeados, reutilizáveis e fáceis de manter. Em código profissional, uma boa função não é apenas uma função que funciona, mas uma função com responsabilidade clara.
