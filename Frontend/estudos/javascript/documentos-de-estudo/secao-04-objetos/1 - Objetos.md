# Objetos em JavaScript

Objetos são estruturas usadas para representar dados organizados em pares de chave e valor.

Eles são uma das bases do JavaScript moderno, porque aparecem em praticamente tudo: dados de API, configurações, estados de tela, entidades de negócio, parâmetros de funções e estruturas internas da linguagem.

---

# 1 - O que é um objeto

Um objeto guarda informações usando propriedades.

Cada propriedade possui:

- uma chave;
- um valor.

Exemplo:

```js
const pessoa = {
    nome: "Nícolas",
    idade: 20,
    ativo: true
};
```

Nesse exemplo:

- `nome` é uma chave;
- `"Nícolas"` é o valor dessa chave;
- `idade` guarda um número;
- `ativo` guarda um booleano.

Na prática, objetos ajudam a representar uma coisa com várias características.

---

# 2 - Por que objetos existem

Sem objetos, seria necessário criar várias variáveis soltas.

```js
const nomeUsuario = "Nícolas";
const idadeUsuario = 20;
const emailUsuario = "nicolas@email.com";
```

Com objeto:

```js
const usuario = {
    nome: "Nícolas",
    idade: 20,
    email: "nicolas@email.com"
};
```

O objeto mantém dados relacionados dentro da mesma estrutura.

Isso facilita:

- organizar informações;
- passar dados para funções;
- enviar dados para APIs;
- receber respostas do backend;
- modelar entidades reais;
- evitar muitas variáveis soltas.

---

# 3 - Criando objetos

A forma mais comum é usar objeto literal.

```js
const produto = {
    nome: "Arroz",
    preco: 20,
    ativo: true
};
```

Também existe `new Object()`, mas quase nunca é usado em código moderno.

```js
const produto = new Object();

produto.nome = "Arroz";
produto.preco = 20;
```

O resultado prático é parecido, mas a versão literal é mais simples e mais legível.

---

# 4 - Acessando propriedades

Existem duas formas principais.

Com ponto:

```js
const usuario = {
    nome: "Nícolas"
};

console.log(usuario.nome); // "Nícolas"
```

Com colchetes:

```js
const usuario = {
    nome: "Nícolas"
};

console.log(usuario["nome"]); // "Nícolas"
```

Use ponto quando o nome da propriedade é fixo.

Use colchetes quando a propriedade vem de uma variável.

```js
const campo = "nome";

const usuario = {
    nome: "Nícolas"
};

console.log(usuario[campo]); // "Nícolas"
```

---

# 5 - Alterando e adicionando propriedades

Objetos podem ser alterados depois de criados, quando declarados com `const`.

```js
const usuario = {
    nome: "Nícolas"
};

usuario.idade = 20;
usuario.nome = "Nicolas";

console.log(usuario);
```

`const` impede reatribuir a variável, mas não impede alterar o conteúdo do objeto.

```js
const usuario = {
    nome: "Nícolas"
};

usuario.nome = "Ana"; // permitido

usuario = {}; // erro
```

---

# 6 - Métodos em objetos

Quando uma propriedade guarda uma função, ela é chamada de método.

```js
const usuario = {
    nome: "Nícolas",
    saudacao: function() {
        return `Olá, meu nome é ${this.nome}`;
    }
};

console.log(usuario.saudacao());
```

Dentro de métodos, `this` geralmente representa o objeto que chamou a função.

Esse assunto é aprofundado em `Frontend/estudos/javascript/documentos-de-estudo/secao-09-orientacao-objetos/3 - this, bind, call e apply.md`.

---

# 7 - Desestruturação de objetos

Desestruturação permite extrair propriedades para variáveis.

```js
const usuario = {
    nome: "Nícolas",
    idade: 20
};

const { nome, idade } = usuario;

console.log(nome); // "Nícolas"
console.log(idade); // 20
```

Isso é muito comum em React, funções e consumo de APIs.

Também é possível renomear:

```js
const produto = {
    nome: "Arroz"
};

const { nome: nomeProduto } = produto;

console.log(nomeProduto); // "Arroz"
```

---

# 8 - Spread operator em objetos

O spread (`...`) permite copiar propriedades de um objeto para outro.

```js
const usuario = {
    nome: "Nícolas",
    idade: 20
};

const usuarioAtualizado = {
    ...usuario,
    idade: 21
};

console.log(usuarioAtualizado);
```

Isso é útil para criar uma nova versão do objeto sem alterar diretamente o original.

Em React e em código moderno, esse padrão aparece bastante.

---

# 9 - Objetos e referências

Objetos são tipos por referência.

```js
const usuario1 = {
    nome: "Nícolas"
};

const usuario2 = usuario1;

usuario2.nome = "Ana";

console.log(usuario1.nome); // "Ana"
```

Isso acontece porque `usuario1` e `usuario2` apontam para o mesmo objeto na memória.

Para criar uma cópia simples:

```js
const usuario1 = {
    nome: "Nícolas"
};

const usuario2 = {
    ...usuario1
};

usuario2.nome = "Ana";

console.log(usuario1.nome); // "Nícolas"
```

Esse assunto se conecta com `Frontend/estudos/javascript/documentos-de-estudo/secao-07-memoria/1 - Memória.md`.

---

# 10 - Exemplo prático completo

```js
const pedido = {
    id: 10,
    cliente: {
        nome: "Nícolas",
        cidade: "São Paulo"
    },
    itens: [
        { produto: "Arroz", preco: 20 },
        { produto: "Feijão", preco: 12 }
    ]
};

const total = pedido.itens.reduce(function(acumulador, item) {
    return acumulador + item.preco;
}, 0);

console.log(pedido.cliente.nome);
console.log(total);
```

Esse exemplo mostra um formato muito comum em APIs: objetos contendo outros objetos e arrays.

---

# 11 - Erros comuns

### Comparar objetos pelo conteúdo

```js
console.log({ id: 1 } === { id: 1 }); // false
```

Mesmo parecidos, são objetos diferentes na memória.

### Alterar objeto original sem perceber

```js
const usuario = {
    nome: "Nícolas"
};

function alterarNome(dados) {
    dados.nome = "Ana";
}

alterarNome(usuario);

console.log(usuario.nome); // "Ana"
```

Quando isso for um problema, crie uma cópia antes.

### Criar objetos grandes demais sem responsabilidade clara

Objetos muito grandes e genéricos dificultam manutenção.

Prefira estruturas com nomes claros e dados relacionados.

---

# 12 - Relação com outros estudos

Objetos se conectam com arrays, memória, funções, `this`, classes e prototypes.

Antes de estudar classes e prototypes, é importante dominar objetos, porque esses assuntos partem da ideia de propriedades, métodos e referência.

---

# 13 - Conclusão

Objetos são a principal forma de representar dados estruturados em JavaScript.

Dominar objetos é essencial para entender respostas de API, estado de aplicações, componentes React, configurações, entidades de negócio e praticamente qualquer código JavaScript real.
