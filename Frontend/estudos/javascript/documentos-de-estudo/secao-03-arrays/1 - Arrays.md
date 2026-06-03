# Arrays em JavaScript

Arrays são estruturas usadas para guardar vários valores em uma única variável.

Eles são muito usados quando precisamos trabalhar com listas: lista de usuários, produtos, mensagens, tarefas, pedidos, filtros, itens de carrinho e muitos outros dados do dia a dia de uma aplicação.

---

# 1 - O que é um array

Um array é uma coleção ordenada de valores.

Cada valor dentro do array ocupa uma posição chamada índice.

Exemplo:

```js
const nomes = ["Nícolas", "João", "Maria"];
```

Nesse exemplo:

- `"Nícolas"` está no índice `0`;
- `"João"` está no índice `1`;
- `"Maria"` está no índice `2`.

O ponto importante é:

> Em JavaScript, arrays começam no índice `0`.

Para acessar um valor:

```js
const nomes = ["Nícolas", "João", "Maria"];

console.log(nomes[0]); // "Nícolas"
console.log(nomes[2]); // "Maria"
```

---

# 2 - Por que arrays existem

Arrays existem para evitar a criação de várias variáveis separadas para representar dados parecidos.

Sem array:

```js
const produto1 = "Arroz";
const produto2 = "Feijão";
const produto3 = "Macarrão";
```

Com array:

```js
const produtos = ["Arroz", "Feijão", "Macarrão"];
```

Com o array, fica mais fácil:

- percorrer todos os itens;
- adicionar novos valores;
- remover valores;
- filtrar dados;
- transformar uma lista em outra;
- renderizar listas na tela;
- enviar coleções para uma API.

Na prática, qualquer tela que mostra vários registros provavelmente usa arrays em algum ponto.

---

# 3 - Criando arrays

A forma mais comum é usar colchetes.

```js
const listaVazia = [];
const numeros = [1, 2, 3];
const nomes = ["Ana", "Carlos", "Marina"];
```

Um array também pode guardar valores de tipos diferentes, mas em código real isso costuma ser evitado quando a lista representa uma mesma coisa.

```js
const dadosMisturados = ["Nícolas", 20, true];
```

Melhor, quando os dados pertencem à mesma entidade:

```js
const usuario = {
    nome: "Nícolas",
    idade: 20,
    ativo: true
};
```

Arrays funcionam melhor quando guardam vários itens do mesmo tipo ou da mesma natureza.

---

# 4 - Tamanho do array

A propriedade `length` retorna a quantidade de itens.

```js
const produtos = ["Arroz", "Feijão", "Macarrão"];

console.log(produtos.length); // 3
```

Ela é muito usada em validações:

```js
const produtos = [];

if (produtos.length === 0) {
    console.log("Nenhum produto encontrado.");
}
```

---

# 5 - Adicionando e removendo itens

Para adicionar no final, use `push`.

```js
const numeros = [1, 2];

numeros.push(3);

console.log(numeros); // [1, 2, 3]
```

Para adicionar no começo, use `unshift`.

```js
const numeros = [2, 3];

numeros.unshift(1);

console.log(numeros); // [1, 2, 3]
```

Para remover do final, use `pop`.

```js
const numeros = [1, 2, 3];

const removido = numeros.pop();

console.log(removido); // 3
console.log(numeros); // [1, 2]
```

Para remover do começo, use `shift`.

```js
const numeros = [1, 2, 3];

const removido = numeros.shift();

console.log(removido); // 1
console.log(numeros); // [2, 3]
```

Esses métodos alteram o array original.

---

# 6 - Buscando itens

Para verificar se um valor existe, use `includes`.

```js
const permissoes = ["criar", "editar", "excluir"];

console.log(permissoes.includes("editar")); // true
```

Para encontrar o índice de um valor, use `indexOf`.

```js
const nomes = ["Ana", "Carlos", "Marina"];

console.log(nomes.indexOf("Carlos")); // 1
console.log(nomes.indexOf("João")); // -1
```

Quando o array possui objetos, `includes` e `indexOf` geralmente não resolvem bem, porque objetos são comparados por referência.

Nesse caso, use `find` ou `some`.

```js
const usuarios = [
    { id: 1, nome: "Ana" },
    { id: 2, nome: "Carlos" }
];

const usuario = usuarios.find(function(item) {
    return item.id === 2;
});

console.log(usuario); // { id: 2, nome: "Carlos" }
```

---

# 7 - Percorrendo arrays

Para executar uma ação para cada item, use `forEach`.

```js
const nomes = ["Ana", "Carlos", "Marina"];

nomes.forEach(function(nome) {
    console.log(nome);
});
```

Para transformar uma lista em outra, use `map`.

```js
const produtos = [
    { nome: "Arroz", preco: 20 },
    { nome: "Feijão", preco: 12 }
];

const nomes = produtos.map(function(produto) {
    return produto.nome;
});

console.log(nomes); // ["Arroz", "Feijão"]
```

Para filtrar itens, use `filter`.

```js
const produtos = [
    { nome: "Arroz", ativo: true },
    { nome: "Feijão", ativo: false },
    { nome: "Macarrão", ativo: true }
];

const produtosAtivos = produtos.filter(function(produto) {
    return produto.ativo;
});

console.log(produtosAtivos);
```

Para acumular um resultado, use `reduce`.

```js
const itens = [
    { nome: "Arroz", preco: 20 },
    { nome: "Feijão", preco: 12 }
];

const total = itens.reduce(function(acumulador, item) {
    return acumulador + item.preco;
}, 0);

console.log(total); // 32
```

---

# 8 - Métodos que alteram e métodos que retornam novo array

Alguns métodos modificam o array original.

Exemplos:

- `push`;
- `pop`;
- `shift`;
- `unshift`;
- `splice`;
- `sort`;
- `reverse`.

Outros retornam um novo array.

Exemplos:

- `map`;
- `filter`;
- `slice`;
- `concat`;
- spread operator (`...`).

Exemplo usando spread:

```js
const numeros = [1, 2, 3];
const novosNumeros = [...numeros, 4];

console.log(numeros); // [1, 2, 3]
console.log(novosNumeros); // [1, 2, 3, 4]
```

Em projetos modernos, principalmente com React, é comum preferir criar novos arrays em vez de modificar o original diretamente.

---

# 9 - Exemplo prático completo

```js
const produtos = [
    { id: 1, nome: "Arroz", preco: 20, ativo: true },
    { id: 2, nome: "Feijão", preco: 12, ativo: false },
    { id: 3, nome: "Macarrão", preco: 8, ativo: true }
];

const produtosAtivos = produtos.filter(function(produto) {
    return produto.ativo;
});

const nomesProdutosAtivos = produtosAtivos.map(function(produto) {
    return produto.nome;
});

const total = produtosAtivos.reduce(function(acumulador, produto) {
    return acumulador + produto.preco;
}, 0);

console.log(nomesProdutosAtivos); // ["Arroz", "Macarrão"]
console.log(total); // 28
```

Esse exemplo mostra um fluxo comum em aplicações reais:

- receber uma lista;
- filtrar registros válidos;
- transformar os dados para exibição;
- calcular um resultado.

---

# 10 - Erros comuns

### Achar que o primeiro índice é 1

```js
const nomes = ["Ana", "Carlos"];

console.log(nomes[1]); // "Carlos", não "Ana"
```

### Alterar array original sem perceber

```js
const numeros = [3, 1, 2];

numeros.sort();

console.log(numeros); // [1, 2, 3]
```

`sort` altera o array original. Se isso for um problema, crie uma cópia antes.

```js
const numeros = [3, 1, 2];
const ordenados = [...numeros].sort();
```

### Usar `map` quando não precisa retornar nada

```js
nomes.map(function(nome) {
    console.log(nome);
});
```

Nesse caso, `forEach` é mais adequado, porque a intenção é só executar uma ação.

---

# 11 - Relação com outros estudos

Arrays se conectam diretamente com objetos, porque em código real é muito comum trabalhar com arrays de objetos.

Antes de avançar para métodos mais complexos, vale revisar `Frontend/estudos/javascript/documentos-de-estudo/secao-04-objetos/1 - Objetos.md`.

Também se conecta com funções, porque métodos como `map`, `filter`, `find`, `some` e `reduce` recebem funções como argumento.

---

# 12 - Conclusão

Arrays são uma das estruturas mais importantes do JavaScript.

Eles permitem representar listas e trabalhar com coleções de dados de forma organizada. No uso real, dominar arrays significa conseguir manipular dados vindos de APIs, montar telas, filtrar registros, calcular totais e transformar informações para exibição.
