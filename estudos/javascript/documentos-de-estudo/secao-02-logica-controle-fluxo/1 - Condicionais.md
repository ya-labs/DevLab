# Condicionais em JavaScript

Condicionais são estruturas usadas para executar diferentes blocos de código com base em condições.

Elas permitem que o programa tome decisões durante a execução.

Exemplo:

```js
const idade = 20;

if (idade >= 18) {
    console.log("Maior de idade");
}
````

Nesse caso, o código dentro do bloco será executado apenas se a condição for verdadeira.

---

# 1. O que é uma condição?

Uma condição é uma expressão que retorna um valor booleano:

```js
true
false
```

Exemplo:

```js
10 > 5
```

Resultado:

```js
true
```

Outro exemplo:

```js
idade >= 18
```

Se `idade` for `20`:

```js
true
```

Condicionais dependem dessas expressões para decidir o fluxo do programa.

---

# 2. if

A estrutura `if` executa um bloco apenas se a condição for verdadeira.

Sintaxe:

```js
if (condicao) {
    // código
}
```

Exemplo:

```js
const usuarioLogado = true;

if (usuarioLogado) {
    console.log("Bem-vindo");
}
```

Se a condição for falsa, nada acontece.

---

# 3. if/else

Quando é necessário executar um caminho alternativo, usa-se `else`.

Exemplo:

```js
const idade = 16;

if (idade >= 18) {
    console.log("Entrada permitida");
} else {
    console.log("Entrada negada");
}
```

Fluxo:

```txt
se condição for true → primeiro bloco
se condição for false → segundo bloco
```

---

# 4. else if

Usado quando existem múltiplas possibilidades.

Exemplo:

```js
const nota = 7;

if (nota >= 9) {
    console.log("Excelente");
} else if (nota >= 7) {
    console.log("Aprovado");
} else if (nota >= 5) {
    console.log("Recuperação");
} else {
    console.log("Reprovado");
}
```

O JavaScript verifica de cima para baixo.

Quando encontra a primeira condição verdadeira, para.

---

# 5. Comparações em condicionais

Condições normalmente usam operadores relacionais.

Exemplos:

```js
>
<
>=
<=
===
!==
```

Exemplo:

```js
const idade = 18;

if (idade === 18) {
    console.log("Tem exatamente 18 anos");
}
```

Prefira `===` ao invés de `==`.

Errado:

```js
"10" == 10
```

Resultado:

```js
true
```

Correto:

```js
"10" === 10
```

Resultado:

```js
false
```

---

# 6. Operadores lógicos em condicionais

## AND (&&)

Exige que todas as condições sejam verdadeiras.

```js
const idade = 20;
const possuiDocumento = true;

if (idade >= 18 && possuiDocumento) {
    console.log("Entrada permitida");
}
```

---

## OR (||)

Exige pelo menos uma condição verdadeira.

```js
const admin = false;
const moderador = true;

if (admin || moderador) {
    console.log("Acesso liberado");
}
```

---

## NOT (!)

Inverte o valor lógico.

```js
const usuarioLogado = false;

if (!usuarioLogado) {
    console.log("Faça login");
}
```

---

# 7. Truthy e falsy

Nem toda condição precisa ser uma comparação explícita.

JavaScript converte valores automaticamente para boolean.

Falsy:

```js
false
0
""
null
undefined
NaN
```

Exemplo:

```js
const nome = "";

if (nome) {
    console.log("Nome informado");
}
```

Nada será executado porque string vazia é falsy.

Outro exemplo:

```js
const nome = "Ana";

if (nome) {
    console.log("Nome válido");
}
```

Aqui executa, porque string preenchida é truthy.

---

# 8. Condições aninhadas

É possível colocar condicionais dentro de outras.

Exemplo:

```js
const usuarioLogado = true;
const assinaturaAtiva = false;

if (usuarioLogado) {
    if (assinaturaAtiva) {
        console.log("Acesso premium");
    } else {
        console.log("Assinatura inativa");
    }
}
```

Funciona, mas excesso de aninhamento dificulta leitura.

Evite quando possível.

---

# 9. Operador ternário

Forma reduzida para condições simples.

Sintaxe:

```js
condicao ? valorSeTrue : valorSeFalse;
```

Exemplo:

```js
const idade = 20;

const mensagem = idade >= 18
    ? "Maior de idade"
    : "Menor de idade";
```

Equivalente:

```js
if (idade >= 18) {
    mensagem = "Maior de idade";
} else {
    mensagem = "Menor de idade";
}
```

Use apenas quando a lógica for simples.

---

# 10. Short-circuit em condicionais

JavaScript pode interromper avaliação cedo.

Exemplo:

```js
const usuario = null;

if (usuario && usuario.nome) {
    console.log(usuario.nome);
}
```

Como `usuario` é `null`, a segunda condição nem será avaliada.

Isso evita erro.

---

# 11. Optional chaining

Forma moderna de verificar propriedades sem quebrar.

Antes:

```js
if (usuario && usuario.endereco && usuario.endereco.rua) {
    console.log(usuario.endereco.rua);
}
```

Agora:

```js
console.log(usuario?.endereco?.rua);
```

Muito mais limpo.

---

# 12. Switch

Usado quando há múltiplos casos fixos.

Exemplo:

```js
const dia = 2;

switch (dia) {
    case 1:
        console.log("Segunda");
        break;

    case 2:
        console.log("Terça");
        break;

    case 3:
        console.log("Quarta");
        break;

    default:
        console.log("Dia inválido");
}
```

Sem `break`, a execução continua nos próximos casos.

---

# 13. Quando usar if ou switch?

Use `if` quando:

* houver comparações complexas
* usar operadores lógicos
* intervalos de valores

Exemplo:

```js
if (idade >= 18 && ativo) {
}
```

Use `switch` quando:

* comparar um mesmo valor fixo contra vários casos

Exemplo:

```js
switch (status) {
}
```

---

# 14. Boas práticas

## Prefira clareza

Ruim:

```js
if (!!usuario === true)
```

Melhor:

```js
if (usuario)
```

---

## Evite aninhamento excessivo

Ruim:

```js
if (a) {
    if (b) {
        if (c) {
        }
    }
}
```

Melhor:

```js
if (a && b && c) {
}
```

---

## Use ternário com moderação

Ruim:

```js
const status = ativo
    ? admin
        ? "Admin"
        : "Usuário"
    : "Bloqueado";
```

Melhor usar `if`.

---

# Conclusão

Condicionais controlam o fluxo do programa e permitem tomada de decisão.

Com elas, é possível validar dados, controlar acessos, alterar comportamentos e responder a diferentes cenários da aplicação.

Dominar `if`, `else`, operadores lógicos, ternário e `switch` é essencial para qualquer desenvolvimento em JavaScript.
