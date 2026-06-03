# Memória em JavaScript

JavaScript é uma linguagem com gerenciamento automático de memória.

Isso significa que o desenvolvedor não aloca e libera memória manualmente como faria em linguagens de baixo nível. A engine do JavaScript, como V8, SpiderMonkey ou JavaScriptCore, gerencia boa parte desse processo.

---

# 1 - Por que estudar memória

Mesmo com gerenciamento automático, entender memória ajuda a explicar comportamentos importantes da linguagem.

Esse assunto ajuda a entender:

- diferença entre primitivos e objetos;
- comparação por valor e por referência;
- cópias rasas;
- mutações em objetos e arrays;
- closures;
- vazamentos de memória;
- garbage collector.

Na prática, muitos bugs de JavaScript acontecem porque o desenvolvedor acha que está copiando um objeto, mas está apenas copiando a referência.

---

# 2 - Stack e Heap

A memória costuma ser explicada usando duas áreas principais: stack e heap.

## Stack

A stack, ou pilha, guarda informações de execução.

Ela armazena:

- chamadas de funções;
- variáveis locais;
- valores primitivos;
- referências para objetos.

Características:

- é rápida;
- tem tamanho mais limitado;
- segue a lógica LIFO, ou seja, o último item que entra é o primeiro que sai.

## Heap

A heap guarda dados mais complexos e dinâmicos.

Ela armazena:

- objetos;
- arrays;
- funções;
- closures;
- estruturas que precisam viver além de uma chamada simples.

Resumo prático:

> Stack guarda execução e referências. Heap guarda objetos reais.

---

# 3 - Tipos primitivos e memória

Tipos primitivos são copiados por valor.

Exemplos:

- `number`;
- `string`;
- `boolean`;
- `null`;
- `undefined`;
- `symbol`;
- `bigint`.

```js
let a = 10;
let b = a;

b = 20;

console.log(a); // 10
console.log(b); // 20
```

Alterar `b` não altera `a`, porque cada variável possui seu próprio valor.

---

# 4 - Objetos e referências

Objetos, arrays e funções são trabalhados por referência.

```js
const usuario1 = {
    nome: "Nícolas"
};

const usuario2 = usuario1;

usuario2.nome = "Ana";

console.log(usuario1.nome); // "Ana"
```

Isso acontece porque `usuario1` e `usuario2` apontam para o mesmo objeto na heap.

Não existem dois objetos nesse exemplo. Existem duas variáveis apontando para o mesmo objeto.

---

# 5 - Cópia rasa

Para criar uma cópia simples de um objeto, use spread.

```js
const usuario1 = {
    nome: "Nícolas",
    idade: 20
};

const usuario2 = {
    ...usuario1
};

usuario2.nome = "Ana";

console.log(usuario1.nome); // "Nícolas"
```

Mas isso é uma cópia rasa.

Objetos internos continuam compartilhando referência.

```js
const usuario1 = {
    nome: "Nícolas",
    endereco: {
        cidade: "São Paulo"
    }
};

const usuario2 = {
    ...usuario1
};

usuario2.endereco.cidade = "Campinas";

console.log(usuario1.endereco.cidade); // "Campinas"
```

Para estruturas profundas, é preciso cuidado extra.

---

# 6 - Garbage collector

Garbage collector é o mecanismo que libera memória que não está mais sendo usada.

Exemplo:

```js
let usuario = {
    nome: "Nícolas"
};

usuario = null;
```

Depois que o objeto deixa de ter referências acessíveis, ele pode ser removido da memória pelo garbage collector.

O desenvolvedor não controla exatamente quando isso acontece.

---

# 7 - Vazamento de memória

Vazamento de memória acontece quando algo que não deveria mais ser usado continua referenciado.

Exemplos comuns:

- listeners de eventos não removidos;
- timers ativos sem necessidade;
- referências globais;
- closures mantendo objetos grandes;
- elementos DOM removidos da tela, mas ainda referenciados no JavaScript.

Exemplo:

```js
function iniciarRelogio() {
    setInterval(function() {
        console.log("Executando...");
    }, 1000);
}
```

Se esse intervalo não for limpo quando não for mais necessário, ele continua executando e mantendo referências.

---

# 8 - Exemplo prático completo

```js
function atualizarUsuario(usuario, novoNome) {
    return {
        ...usuario,
        nome: novoNome
    };
}

const usuarioOriginal = {
    nome: "Nícolas",
    ativo: true
};

const usuarioAtualizado = atualizarUsuario(usuarioOriginal, "Ana");

console.log(usuarioOriginal.nome); // "Nícolas"
console.log(usuarioAtualizado.nome); // "Ana"
```

Esse exemplo evita alterar o objeto original.

Esse padrão é importante em aplicações modernas, principalmente quando se trabalha com estado.

---

# 9 - Erros comuns

### Achar que objeto foi copiado

```js
const a = { nome: "Nícolas" };
const b = a;

b.nome = "Ana";

console.log(a.nome); // "Ana"
```

Isso não é cópia. É referência compartilhada.

### Ignorar objetos aninhados

```js
const copia = {
    ...usuario
};
```

Essa cópia só resolve o primeiro nível.

### Manter referências desnecessárias

Guardar dados grandes em variáveis globais, caches sem limpeza ou listeners antigos pode prejudicar performance.

---

# 10 - Relação com outros estudos

Memória se conecta com arrays, objetos, funções, closures, DOM e React.

Antes de estudar closures com profundidade, vale entender que funções podem manter referências vivas.

Antes de manipular DOM de forma intensa, vale lembrar que elementos também podem ficar presos na memória por referências JavaScript.

---

# 11 - Conclusão

JavaScript gerencia memória automaticamente, mas isso não elimina a responsabilidade do desenvolvedor.

Entender stack, heap, referência, cópia rasa e garbage collector ajuda a evitar bugs difíceis e melhora a forma de pensar sobre objetos, arrays, funções e estado.
