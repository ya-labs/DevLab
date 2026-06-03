# this, bind, call e apply

`this` representa o contexto de execução de uma função.

Em JavaScript, o valor de `this` não depende apenas de onde a função foi escrita. Ele depende principalmente de como a função é chamada.

---

# 1 - O que é this

`this` é uma referência ao contexto atual da chamada.

Exemplo:

```js
const usuario = {
    nome: "Nícolas",
    saudacao: function() {
        return `Olá, ${this.nome}`;
    }
};

console.log(usuario.saudacao()); // "Olá, Nícolas"
```

Nesse caso, `this` aponta para `usuario`, porque a função foi chamada como método do objeto.

---

# 2 - Por que this causa confusão

O valor de `this` pode ser perdido quando o método é separado do objeto.

```js
const usuario = {
    nome: "Nícolas",
    saudacao: function() {
        return `Olá, ${this.nome}`;
    }
};

const fn = usuario.saudacao;

console.log(fn()); // undefined ou erro, dependendo do ambiente
```

Agora a função foi chamada sozinha, sem o objeto antes do ponto.

Por isso, `this` não aponta mais para `usuario`.

---

# 3 - Regras práticas do this

Em chamadas comuns:

```js
usuario.saudacao();
```

`this` aponta para `usuario`.

Em função solta:

```js
const fn = usuario.saudacao;
fn();
```

`this` pode ser `undefined` em strict mode.

Com `new`:

```js
function Pessoa(nome) {
    this.nome = nome;
}

const pessoa = new Pessoa("Nícolas");
```

`this` aponta para o novo objeto criado.

Em arrow functions:

```js
const usuario = {
    nome: "Nícolas",
    saudacao: () => this.nome
};
```

Arrow function não tem `this` próprio.

---

# 4 - bind

`bind` cria uma nova função com o `this` fixado.

```js
const usuario = {
    nome: "Nícolas",
    saudacao: function() {
        return `Olá, ${this.nome}`;
    }
};

const saudacaoUsuario = usuario.saudacao.bind(usuario);

console.log(saudacaoUsuario()); // "Olá, Nícolas"
```

Use `bind` quando precisa passar uma função sem perder o contexto.

Exemplo:

```js
setTimeout(usuario.saudacao.bind(usuario), 1000);
```

---

# 5 - call

`call` executa a função imediatamente, definindo o valor de `this`.

Os argumentos são passados um por um.

```js
function apresentar(cidade, estado) {
    return `${this.nome} mora em ${cidade} - ${estado}`;
}

const usuario = {
    nome: "Nícolas"
};

console.log(apresentar.call(usuario, "São Paulo", "SP"));
```

Use `call` quando quer executar a função agora com um contexto específico.

---

# 6 - apply

`apply` também executa a função imediatamente, mas recebe os argumentos em array.

```js
function apresentar(cidade, estado) {
    return `${this.nome} mora em ${cidade} - ${estado}`;
}

const usuario = {
    nome: "Nícolas"
};

const argumentos = ["São Paulo", "SP"];

console.log(apresentar.apply(usuario, argumentos));
```

Diferença prática:

- `call`: argumentos separados;
- `apply`: argumentos em array;
- `bind`: retorna uma nova função.

---

# 7 - Exemplo prático completo

```js
const validador = {
    idadeMinima: 18,
    validar: function(usuario) {
        return usuario.idade >= this.idadeMinima;
    }
};

const usuario = {
    nome: "Nícolas",
    idade: 20
};

const validarMaioridade = validador.validar.bind(validador);

console.log(validarMaioridade(usuario)); // true
```

Nesse exemplo:

- `validar` depende de `this.idadeMinima`;
- `bind` preserva o contexto de `validador`;
- a função pode ser passada para outro lugar sem perder o `this`.

---

# 8 - Erros comuns

### Usar arrow function como método com this

```js
const usuario = {
    nome: "Nícolas",
    saudacao: () => this.nome
};
```

Prefira `function` quando o método depende do objeto.

### Passar método como callback sem bind

```js
setTimeout(usuario.saudacao, 1000);
```

O método pode perder o contexto.

### Confundir bind com call

`bind` não executa imediatamente.

```js
const fn = apresentar.bind(usuario);
```

`call` executa na hora.

```js
apresentar.call(usuario);
```

---

# 9 - Relação com outros estudos

Este conteúdo depende de objetos e funções.

Ele se conecta com classes, prototype, callbacks, eventos do DOM e métodos de componentes.

Antes de estudar classes a fundo, entender `this` ajuda a evitar boa parte dos bugs de contexto.

---

# 10 - Conclusão

`this` é dinâmico e depende da forma como a função é chamada.

`bind`, `call` e `apply` existem para controlar esse contexto. Em código moderno, você não usa esses métodos o tempo todo, mas precisa entendê-los para ler código legado, eventos, classes e bibliotecas com segurança.
