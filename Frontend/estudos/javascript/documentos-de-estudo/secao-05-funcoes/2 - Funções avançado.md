# Funções avançadas em JavaScript

Depois de entender funções básicas, o próximo passo é estudar como funções se comportam como valores, como lidam com escopo, como mantêm contexto e como são usadas em código moderno.

Esses conceitos aparecem bastante em callbacks, eventos, React, APIs, closures, métodos de array e orientação a objetos.

---

# 1 - Function declaration, function expression e arrow function

Existem formas diferentes de declarar funções.

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

Arrow function:

```js
const somar = (a, b) => {
    return a + b;
};
```

Em código moderno, arrow functions são muito comuns em callbacks e funções curtas.

```js
const numeros = [1, 2, 3];
const dobrados = numeros.map((numero) => numero * 2);
```

Mas arrow function não substitui `function` em todos os casos, porque ela não possui `this` próprio.

---

# 2 - Diferença de this entre function e arrow

Funções declaradas com `function` têm `this` dinâmico.

O valor do `this` depende de como a função é chamada.

```js
const usuario = {
    nome: "Nícolas",
    falar: function() {
        console.log(this.nome);
    }
};

usuario.falar(); // "Nícolas"
```

Arrow functions não têm `this` próprio. Elas herdam o `this` do escopo onde foram criadas.

```js
const usuario = {
    nome: "Nícolas",
    falar: () => {
        console.log(this.nome);
    }
};

usuario.falar(); // undefined em muitos ambientes
```

Regra prática:

- use `function` para métodos que dependem do objeto;
- use arrow function para callbacks e funções curtas que não precisam de `this` próprio.

Esse assunto se conecta diretamente com `Frontend/estudos/javascript/documentos-de-estudo/secao-09-orientacao-objetos/3 - this, bind, call e apply.md`.

---

# 3 - Funções como valores

Em JavaScript, funções são valores.

Isso significa que uma função pode ser:

- armazenada em variável;
- passada como argumento;
- retornada por outra função;
- guardada em objeto;
- guardada em array.

Exemplo:

```js
function executar(acao) {
    acao();
}

executar(function() {
    console.log("Executando callback");
});
```

Esse comportamento é essencial para entender callbacks, eventos e programação funcional.

---

# 4 - Higher-order functions

Higher-order function é uma função que recebe outra função ou retorna outra função.

Exemplo recebendo função:

```js
function filtrar(lista, criterio) {
    const resultado = [];

    lista.forEach(function(item) {
        if (criterio(item)) {
            resultado.push(item);
        }
    });

    return resultado;
}

const numeros = [1, 2, 3, 4];

const pares = filtrar(numeros, function(numero) {
    return numero % 2 === 0;
});

console.log(pares); // [2, 4]
```

Métodos como `map`, `filter`, `reduce`, `find` e `forEach` são exemplos práticos disso.

---

# 5 - Escopo léxico

Escopo léxico significa que uma função lembra o local onde foi criada.

```js
const nome = "global";

function fora() {
    const nome = "fora";

    function dentro() {
        console.log(nome);
    }

    dentro();
}

fora(); // "fora"
```

A função `dentro` acessa a variável `nome` do escopo onde ela foi criada.

Isso é a base para entender closures.

---

# 6 - Closures

Closure acontece quando uma função continua acessando variáveis do escopo onde foi criada, mesmo depois que esse escopo já terminou sua execução.

```js
function criarContador() {
    let contador = 0;

    return function() {
        contador += 1;
        return contador;
    };
}

const incrementar = criarContador();

console.log(incrementar()); // 1
console.log(incrementar()); // 2
console.log(incrementar()); // 3
```

Mesmo depois de `criarContador` terminar, a função retornada ainda lembra da variável `contador`.

Na prática, closures são usadas para:

- encapsular estado;
- criar funções configuradas;
- preservar dados entre chamadas;
- implementar módulos;
- trabalhar com callbacks.

---

# 7 - Currying e funções configuradas

Uma função pode retornar outra função já configurada.

```js
function criarSaudacao(mensagem) {
    return function(nome) {
        return `${mensagem}, ${nome}`;
    };
}

const dizerOla = criarSaudacao("Olá");

console.log(dizerOla("Nícolas")); // "Olá, Nícolas"
```

Isso não precisa ser usado em todo código, mas ajuda a entender como funções podem carregar configuração.

---

# 8 - Parâmetros padrão

Parâmetros padrão definem valores quando nenhum argumento é enviado.

```js
function criarUsuario(nome, ativo = true) {
    return {
        nome,
        ativo
    };
}

console.log(criarUsuario("Nícolas"));
```

Isso evita validações manuais simples.

---

# 9 - Rest parameters

Rest parameters permitem receber vários argumentos como um array.

```js
function somarTodos(...numeros) {
    return numeros.reduce(function(total, numero) {
        return total + numero;
    }, 0);
}

console.log(somarTodos(1, 2, 3)); // 6
```

O `...numeros` junta os argumentos restantes em um array.

---

# 10 - Exemplo prático completo

```js
function criarFiltroPorStatus(status) {
    return function(item) {
        return item.status === status;
    };
}

const pedidos = [
    { id: 1, status: "aberto" },
    { id: 2, status: "finalizado" },
    { id: 3, status: "aberto" }
];

const filtrarAbertos = criarFiltroPorStatus("aberto");
const pedidosAbertos = pedidos.filter(filtrarAbertos);

console.log(pedidosAbertos);
```

Esse exemplo usa:

- função retornando função;
- closure;
- callback no `filter`;
- separação de responsabilidade.

---

# 11 - Erros comuns

### Usar arrow function em método que precisa de this

```js
const usuario = {
    nome: "Nícolas",
    falar: () => this.nome
};
```

Prefira:

```js
const usuario = {
    nome: "Nícolas",
    falar: function() {
        return this.nome;
    }
};
```

### Criar closure sem perceber e manter memória desnecessária

Closures são úteis, mas podem manter referências vivas por mais tempo.

Se uma função interna guarda acesso a objetos grandes, eles podem continuar na memória.

### Usar conceito avançado sem necessidade

Nem todo problema precisa de currying, factory complexa ou composição funcional.

Use quando deixar o código mais claro, não apenas porque é possível.

---

# 12 - Relação com outros estudos

Este conteúdo depende de `Frontend/estudos/javascript/documentos-de-estudo/secao-05-funcoes/1 - Funcoes básicas.md`.

Também se conecta com arrays, memória, assincronismo, `this`, classes e módulos.

---

# 13 - Conclusão

Funções avançadas mostram que funções em JavaScript não são apenas blocos de código.

Elas também são valores, carregam escopo, podem preservar estado e participam da estrutura de praticamente todo código moderno. Dominar esses conceitos ajuda a escrever código mais flexível, mas a regra continua sendo simples: use a solução avançada apenas quando ela melhorar clareza e manutenção.
