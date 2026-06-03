# Objeto Map em JavaScript

`Map` é uma estrutura de dados usada para armazenar pares de chave e valor.

Ele parece um objeto comum, mas foi criado especificamente para trabalhar como coleção dinâmica de entradas.

---

# 1 - O que é Map

Um `Map` guarda valores associados a chaves.

```js
const mapa = new Map();

mapa.set("nome", "Nícolas");
mapa.set("idade", 20);

console.log(mapa.get("nome")); // "Nícolas"
```

Cada entrada possui:

- uma chave;
- um valor.

---

# 2 - Por que Map existe

Objetos comuns funcionam bem para representar entidades.

```js
const usuario = {
    nome: "Nícolas",
    idade: 20
};
```

Mas quando a intenção é trabalhar com uma coleção dinâmica de chave e valor, `Map` pode ser melhor.

Ele oferece:

- chaves de qualquer tipo;
- ordem de inserção preservada;
- propriedade `size`;
- métodos próprios para coleção;
- iteração mais direta.

---

# 3 - Map vs Object

Objeto comum:

```js
const usuario = {
    nome: "Nícolas",
    idade: 20
};
```

Melhor para representar dados com estrutura conhecida.

Map:

```js
const permissoes = new Map();

permissoes.set("admin", true);
permissoes.set("financeiro", false);
```

Melhor para coleções de pares chave-valor que podem crescer, mudar e ser iteradas.

Regra prática:

> Use objeto para modelar uma entidade. Use Map para coleção dinâmica de chave e valor.

---

# 4 - Criando um Map

Map vazio:

```js
const mapa = new Map();
```

Map com valores iniciais:

```js
const statusPedidos = new Map([
    ["aberto", "Pedido em aberto"],
    ["pago", "Pedido pago"],
    ["cancelado", "Pedido cancelado"]
]);
```

---

# 5 - Métodos principais

Adicionar ou atualizar:

```js
statusPedidos.set("enviado", "Pedido enviado");
```

Buscar:

```js
console.log(statusPedidos.get("pago"));
```

Verificar existência:

```js
console.log(statusPedidos.has("cancelado"));
```

Remover:

```js
statusPedidos.delete("aberto");
```

Limpar tudo:

```js
statusPedidos.clear();
```

Quantidade de entradas:

```js
console.log(statusPedidos.size);
```

---

# 6 - Chaves de qualquer tipo

Diferente de objetos comuns, `Map` permite usar objetos como chave.

```js
const usuario = {
    id: 1,
    nome: "Nícolas"
};

const sessoes = new Map();

sessoes.set(usuario, "sessao_abc");

console.log(sessoes.get(usuario)); // "sessao_abc"
```

Isso pode ser útil em caches, controle de estado e estruturas internas.

---

# 7 - Iterando um Map

Com `for...of`:

```js
const statusPedidos = new Map([
    ["aberto", "Pedido em aberto"],
    ["pago", "Pedido pago"]
]);

for (const [chave, valor] of statusPedidos) {
    console.log(chave, valor);
}
```

Com `forEach`:

```js
statusPedidos.forEach(function(valor, chave) {
    console.log(chave, valor);
});
```

Também existem:

```js
statusPedidos.keys();
statusPedidos.values();
statusPedidos.entries();
```

---

# 8 - Exemplo prático completo

```js
const mensagensStatus = new Map([
    ["pendente", "Aguardando pagamento"],
    ["pago", "Pagamento confirmado"],
    ["enviado", "Pedido enviado"],
    ["cancelado", "Pedido cancelado"]
]);

function obterMensagemStatus(status) {
    return mensagensStatus.get(status) ?? "Status desconhecido";
}

console.log(obterMensagemStatus("pago")); // "Pagamento confirmado"
console.log(obterMensagemStatus("x")); // "Status desconhecido"
```

Esse exemplo usa `Map` como tabela de consulta.

É uma alternativa mais organizada do que vários `if` quando a regra é apenas mapear uma chave para um valor.

---

# 9 - Erros comuns

### Usar propriedade como se fosse objeto

```js
const mapa = new Map();

mapa.nome = "Nícolas";
```

Isso não adiciona uma entrada no Map.

Use:

```js
mapa.set("nome", "Nícolas");
```

### Usar Map para entidade simples

```js
const usuario = new Map([
    ["nome", "Nícolas"],
    ["idade", 20]
]);
```

Para esse caso, objeto literal é mais claro.

### Esquecer que chaves de objeto dependem da mesma referência

```js
const mapa = new Map();

mapa.set({ id: 1 }, "valor");

console.log(mapa.get({ id: 1 })); // undefined
```

Os dois objetos têm o mesmo conteúdo, mas são referências diferentes.

---

# 10 - Relação com outros estudos

Map se conecta com objetos, arrays, memória e estruturas de dados.

Antes de usar `Map`, vale dominar objetos comuns, porque eles continuam sendo a estrutura mais usada para representar dados em JavaScript.

---

# 11 - Conclusão

`Map` é útil quando precisamos de uma coleção dinâmica de chave e valor.

Ele não substitui objetos comuns em todos os casos. A decisão prática é simples: objeto para dados estruturados de uma entidade, `Map` para coleção de pares chave-valor com operações frequentes de busca, inserção, remoção e iteração.
