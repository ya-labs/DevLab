# Loops em JavaScript

Loops (estruturas de repetição) são usados para executar um bloco de código várias vezes.

Eles evitam repetição manual de código e permitem percorrer coleções de dados, repetir operações e automatizar processos.

Exemplo:

```js
console.log("Olá");
console.log("Olá");
console.log("Olá");
console.log("Olá");
console.log("Olá");
````

Com loop:

```js
for (let i = 0; i < 5; i++) {
    console.log("Olá");
}
```

O resultado é o mesmo, mas com código mais organizado e escalável.

---

# 1. Por que loops existem?

Imagine uma lista com 100 usuários.

Sem loop:

```js
console.log(usuarios[0]);
console.log(usuarios[1]);
console.log(usuarios[2]);
```

Isso rapidamente se torna inviável.

Loops existem para repetir uma ação de forma controlada.

---

# 2. for

O `for` é a estrutura de repetição mais comum.

Sintaxe:

```js
for (inicializacao; condicao; incremento) {
    // código
}
```

Exemplo:

```js
for (let i = 0; i < 5; i++) {
    console.log(i);
}
```

Resultado:

```txt
0
1
2
3
4
```

Partes:

```js
let i = 0;
```

Valor inicial.

```js
i < 5;
```

Condição para continuar.

```js
i++;
```

Atualização a cada repetição.

Fluxo:

```txt
cria variável
verifica condição
executa bloco
incrementa
repete
```

---

# 3. Controle do índice

O contador pode começar de qualquer valor.

Exemplo:

```js
for (let i = 1; i <= 5; i++) {
    console.log(i);
}
```

Resultado:

```txt
1
2
3
4
5
```

Também pode decrementar:

```js
for (let i = 5; i > 0; i--) {
    console.log(i);
}
```

Resultado:

```txt
5
4
3
2
1
```

---

# 4. Loop infinito

Se a condição nunca se tornar falsa, o loop nunca termina.

Exemplo:

```js
for (let i = 0; i >= 0; i++) {
    console.log(i);
}
```

Esse loop continuará indefinidamente.

Loops infinitos podem travar navegador ou aplicação.

---

# 5. while

Executa enquanto a condição for verdadeira.

Sintaxe:

```js
while (condicao) {
    // código
}
```

Exemplo:

```js
let contador = 0;

while (contador < 5) {
    console.log(contador);
    contador++;
}
```

Resultado:

```txt
0
1
2
3
4
```

Diferença principal:

* `for`: quando já se conhece a estrutura da repetição
* `while`: quando a repetição depende de condição dinâmica

---

# 6. Cuidado com while

Se esquecer de atualizar a condição:

```js
let contador = 0;

while (contador < 5) {
    console.log(contador);
}
```

Resultado:

```txt
loop infinito
```

Porque `contador` nunca muda.

---

# 7. do...while

Executa pelo menos uma vez, mesmo que a condição seja falsa.

Sintaxe:

```js
do {
    // código
} while (condicao);
```

Exemplo:

```js
let contador = 10;

do {
    console.log(contador);
} while (contador < 5);
```

Resultado:

```txt
10
```

Mesmo com condição falsa, executa uma vez.

---

# 8. for...of

Usado para percorrer valores iteráveis.

Muito comum com arrays.

Exemplo:

```js
const nomes = ["Ana", "Carlos", "João"];

for (const nome of nomes) {
    console.log(nome);
}
```

Resultado:

```txt
Ana
Carlos
João
```

Mais limpo que:

```js
for (let i = 0; i < nomes.length; i++) {
    console.log(nomes[i]);
}
```

Use quando só precisa do valor.

---

# 9. for...in

Usado para percorrer propriedades de objetos.

Exemplo:

```js
const usuario = {
    nome: "Ana",
    idade: 20,
    cidade: "Criciúma"
};

for (const chave in usuario) {
    console.log(chave);
}
```

Resultado:

```txt
nome
idade
cidade
```

Acessando valores:

```js
for (const chave in usuario) {
    console.log(usuario[chave]);
}
```

Resultado:

```txt
Ana
20
Criciúma
```

---

# 10. for...of vs for...in

## for...of

Percorre valores.

```js
for (const item of array) {
}
```

---

## for...in

Percorre chaves/propriedades.

```js
for (const chave in objeto) {
}
```

Exemplo:

Array com `for...in`:

```js
const nomes = ["Ana", "Carlos"];

for (const indice in nomes) {
    console.log(indice);
}
```

Resultado:

```txt
0
1
```

Com `for...of`:

```js
for (const nome of nomes) {
    console.log(nome);
}
```

Resultado:

```txt
Ana
Carlos
```

---

# 11. break

Interrompe completamente o loop.

Exemplo:

```js
for (let i = 0; i < 10; i++) {
    if (i === 5) {
        break;
    }

    console.log(i);
}
```

Resultado:

```txt
0
1
2
3
4
```

Quando chega em `5`, o loop termina.

---

# 12. continue

Pula apenas a iteração atual.

Exemplo:

```js
for (let i = 0; i < 5; i++) {
    if (i === 2) {
        continue;
    }

    console.log(i);
}
```

Resultado:

```txt
0
1
3
4
```

O `2` foi ignorado.

---

# 13. Loops com arrays

Forma clássica:

```js
const numeros = [10, 20, 30];

for (let i = 0; i < numeros.length; i++) {
    console.log(numeros[i]);
}
```

Forma moderna:

```js
for (const numero of numeros) {
    console.log(numero);
}
```

Se precisar do índice, use `for`.

Se precisar apenas do valor, `for...of` geralmente é melhor.

---

# 14. Loops aninhados

Um loop dentro de outro.

Exemplo:

```js
for (let i = 1; i <= 3; i++) {
    for (let j = 1; j <= 2; j++) {
        console.log(i, j);
    }
}
```

Resultado:

```txt
1 1
1 2
2 1
2 2
3 1
3 2
```

Cada repetição externa executa o loop interno inteiro.

Cuidado com performance em estruturas grandes.

---

# 15. Escopo no loop

Variáveis com `let` existem apenas dentro do bloco.

```js
for (let i = 0; i < 5; i++) {
    console.log(i);
}

console.log(i);
```

Isso gera erro.

Porque `i` só existe dentro do loop.

Com `var`, isso seria diferente.

Por isso, prefira `let`.

---

# 16. Erros comuns

## Condição errada

```js
for (let i = 0; i <= array.length; i++) {
}
```

Problema:

```txt
último índice será inválido
```

Correto:

```js
i < array.length
```

---

## Esquecer incremento

```js
while (contador < 10) {
}
```

Problema:

```txt
loop infinito
```

---

## Usar for...in em array sem necessidade

```js
for (const i in array) {
}
```

Se precisa dos valores:

```js
for (const item of array) {
}
```

---

# 17. Quando usar cada um?

Use `for`:

* quando precisar de índice
* controle manual da repetição
* incremento personalizado

Use `while`:

* repetição baseada em condição dinâmica

Use `do...while`:

* quando precisa executar ao menos uma vez

Use `for...of`:

* percorrer valores de arrays

Use `for...in`:

* percorrer propriedades de objetos

---

# Conclusão

Loops permitem repetir operações de forma controlada e eficiente.

São fundamentais para percorrer arrays, processar dados, automatizar tarefas e controlar fluxos repetitivos.

Saber escolher entre `for`, `while`, `do...while`, `for...of` e `for...in` melhora legibilidade, segurança e clareza do código.