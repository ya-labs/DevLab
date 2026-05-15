# Variáveis e Tipos em JavaScript

Variáveis são espaços usados para armazenar valores durante a execução de um programa.

Esses valores podem representar textos, números, estados, listas, objetos, resultados de cálculos, respostas de APIs e muitas outras informações.

Em JavaScript, as variáveis são fundamentais para controlar dados e construir a lógica da aplicação.

---

# 1. O que é uma variável?

Uma variável é um nome associado a um valor.

Exemplo:

```js
const nome = "Ana";
const idade = 20;
const ativo = true;
````

Nesse exemplo:

```txt
nome armazena o texto "Ana"
idade armazena o número 20
ativo armazena o valor booleano true
```

A variável permite reutilizar esse valor em várias partes do código.

```js
console.log(nome);
console.log(idade);
console.log(ativo);
```

---

# 2. Declarando variáveis

Em JavaScript, existem três formas principais de declarar variáveis:

```js
var
let
const
```

Atualmente, recomenda-se usar principalmente `let` e `const`.

---

# 3. var

`var` é a forma antiga de declarar variáveis em JavaScript.

Exemplo:

```js
var nome = "Ana";

console.log(nome);
```

Embora ainda funcione, `var` deve ser evitado em códigos modernos, pois possui comportamentos que podem causar confusão, principalmente relacionados a escopo e hoisting.

Exemplo:

```js
if (true) {
    var nome = "Ana";
}

console.log(nome);
```

Nesse caso, a variável `nome` ainda pode ser acessada fora do bloco `if`.

Isso acontece porque `var` possui escopo de função, não escopo de bloco.

---

# 4. let

`let` é usado para declarar variáveis que podem ter seu valor alterado.

Exemplo:

```js
let idade = 20;

idade = 21;

console.log(idade);
```

Resultado:

```txt
21
```

Use `let` quando o valor da variável precisar mudar durante a execução do programa.

Exemplo:

```js
let contador = 0;

contador = contador + 1;
contador = contador + 1;

console.log(contador);
```

Resultado:

```txt
2
```

---

# 5. const

`const` é usado para declarar variáveis que não podem ser reatribuídas.

Exemplo:

```js
const nome = "Ana";

nome = "Carlos";
```

Esse código gera erro, pois uma variável declarada com `const` não pode receber outro valor.

Use `const` quando o valor não precisar ser reatribuído.

Exemplo:

```js
const taxaJuros = 0.05;
const nomeSistema = "Sistema de Vendas";
const limiteTentativas = 3;
```

---

# 6. const em objetos e arrays

Uma dúvida comum é pensar que `const` torna tudo imutável.

Na verdade, `const` impede a reatribuição da variável, mas não impede alteração interna de objetos e arrays.

Exemplo com objeto:

```js
const usuario = {
    nome: "Ana",
    idade: 20
};

usuario.idade = 21;

console.log(usuario);
```

Isso funciona, pois o objeto continua sendo o mesmo.

O que não pode é reatribuir a variável:

```js
usuario = {
    nome: "Carlos",
    idade: 25
};
```

Esse código gera erro.

Exemplo com array:

```js
const nomes = ["Ana", "Carlos"];

nomes.push("João");

console.log(nomes);
```

Resultado:

```txt
["Ana", "Carlos", "João"]
```

Isso também funciona.

Mas isto não funciona:

```js
nomes = ["Maria", "Pedro"];
```

---

# 7. Diferença entre let e const

Use `const` por padrão.

Use `let` apenas quando precisar alterar o valor da variável.

Exemplo com `const`:

```js
const nome = "Ana";
const idade = 20;
const usuarioAtivo = true;
```

Exemplo com `let`:

```js
let contador = 0;

contador++;
contador++;
```

Resumo:

```txt
const: valor não será reatribuído
let: valor poderá ser reatribuído
var: forma antiga, evite em código moderno
```

---

# 8. Escopo de variáveis

Escopo define onde uma variável pode ser acessada.

Em JavaScript, os principais escopos são:

```txt
Escopo global
Escopo de função
Escopo de bloco
```

---

# 9. Escopo global

Uma variável declarada fora de funções ou blocos pertence ao escopo global.

Exemplo:

```js
const nome = "Ana";

function exibirNome() {
    console.log(nome);
}

exibirNome();
```

A função consegue acessar `nome`, pois ele está no escopo global.

---

# 10. Escopo de função

Variáveis declaradas dentro de uma função só existem dentro dela.

Exemplo:

```js
function exibirMensagem() {
    const mensagem = "Olá";

    console.log(mensagem);
}

exibirMensagem();

console.log(mensagem);
```

A última linha gera erro, pois `mensagem` só existe dentro da função.

---

# 11. Escopo de bloco

Blocos são estruturas delimitadas por `{}`.

Exemplo:

```js
if (true) {
    const nome = "Ana";
    let idade = 20;

    console.log(nome);
    console.log(idade);
}
```

As variáveis `nome` e `idade` só existem dentro do bloco.

Fora dele, não podem ser acessadas:

```js
console.log(nome);
console.log(idade);
```

Isso gera erro.

---

# 12. Hoisting

Hoisting é um comportamento do JavaScript em que declarações são tratadas como se fossem movidas para o topo do escopo.

Com `var`, isso pode causar confusão.

Exemplo:

```js
console.log(nome);

var nome = "Ana";
```

Resultado:

```txt
undefined
```

Internamente, é como se acontecesse algo parecido com:

```js
var nome;

console.log(nome);

nome = "Ana";
```

Com `let` e `const`, o comportamento é mais seguro:

```js
console.log(nome);

const nome = "Ana";
```

Esse código gera erro.

Por isso, prefira `let` e `const`.

---

# 13. Tipos de dados

JavaScript possui diferentes tipos de dados.

Os principais são:

```txt
string
number
boolean
undefined
null
object
array
function
symbol
bigint
```

---

# 14. string

`string` representa texto.

Exemplo:

```js
const nome = "Ana";
const cidade = "Criciúma";
const mensagem = "Olá, mundo!";
```

Strings podem ser escritas com aspas duplas, aspas simples ou crase.

```js
const texto1 = "Texto";
const texto2 = 'Texto';
const texto3 = `Texto`;
```

A crase permite interpolação de valores.

```js
const nome = "Ana";
const idade = 20;

const mensagem = `Meu nome é ${nome} e tenho ${idade} anos.`;

console.log(mensagem);
```

Resultado:

```txt
Meu nome é Ana e tenho 20 anos.
```

---

# 15. number

`number` representa números.

Exemplo:

```js
const idade = 20;
const preco = 49.90;
const temperatura = -5;
```

JavaScript usa o tipo `number` tanto para inteiros quanto para números decimais.

Exemplo:

```js
const quantidade = 10;
const valor = 10.5;
```

Operações:

```js
const soma = 10 + 5;
const subtracao = 10 - 5;
const multiplicacao = 10 * 5;
const divisao = 10 / 5;
```

---

# 16. boolean

`boolean` representa verdadeiro ou falso.

Valores possíveis:

```js
true
false
```

Exemplo:

```js
const usuarioAtivo = true;
const possuiPermissao = false;
```

Booleans são muito usados em condições.

```js
if (usuarioAtivo) {
    console.log("Usuário ativo");
}
```

---

# 17. undefined

`undefined` indica que uma variável foi declarada, mas ainda não recebeu valor.

Exemplo:

```js
let nome;

console.log(nome);
```

Resultado:

```txt
undefined
```

Também pode aparecer ao acessar uma propriedade inexistente.

```js
const usuario = {
    nome: "Ana"
};

console.log(usuario.idade);
```

Resultado:

```txt
undefined
```

---

# 18. null

`null` representa ausência intencional de valor.

Exemplo:

```js
const usuarioSelecionado = null;
```

Use `null` quando quiser indicar que uma variável está vazia de propósito.

Exemplo:

```js
let produtoSelecionado = null;

produtoSelecionado = {
    nome: "Mouse",
    preco: 50
};
```

Diferença comum:

```txt
undefined: valor ainda não foi definido
null: valor vazio definido intencionalmente
```

---

# 19. object

`object` representa uma estrutura com propriedades.

Exemplo:

```js
const usuario = {
    nome: "Ana",
    idade: 20,
    ativo: true
};
```

Acessando propriedades:

```js
console.log(usuario.nome);
console.log(usuario.idade);
console.log(usuario.ativo);
```

Também é possível acessar usando colchetes:

```js
console.log(usuario["nome"]);
```

Alterando propriedades:

```js
usuario.idade = 21;
```

Adicionando propriedades:

```js
usuario.email = "ana@email.com";
```

---

# 20. array

Arrays são listas de valores.

Exemplo:

```js
const nomes = ["Ana", "Carlos", "João"];
const numeros = [10, 20, 30];
```

Acessando itens:

```js
console.log(nomes[0]);
console.log(nomes[1]);
console.log(nomes[2]);
```

Resultado:

```txt
Ana
Carlos
João
```

Arrays começam no índice `0`.

Adicionando item:

```js
nomes.push("Maria");
```

Removendo último item:

```js
nomes.pop();
```

---

# 21. function

Funções também são valores em JavaScript.

Exemplo:

```js
function somar(a, b) {
    return a + b;
}
```

Também é possível armazenar uma função em uma variável:

```js
const somar = function (a, b) {
    return a + b;
};

console.log(somar(10, 5));
```

Ou usando arrow function:

```js
const somar = (a, b) => {
    return a + b;
};
```

---

# 22. bigint

`bigint` representa números inteiros muito grandes.

Exemplo:

```js
const numeroGrande = 9007199254740991n;
```

O `n` no final indica que o valor é um `bigint`.

Esse tipo é usado quando o número ultrapassa o limite seguro do tipo `number`.

---

# 23. symbol

`symbol` cria valores únicos.

Exemplo:

```js
const id = Symbol("id");
const outroId = Symbol("id");

console.log(id === outroId);
```

Resultado:

```txt
false
```

Mesmo com a mesma descrição, cada `Symbol` é único.

É um tipo mais avançado e menos usado em códigos iniciais.

---

# 24. typeof

O operador `typeof` mostra o tipo de um valor.

Exemplo:

```js
console.log(typeof "Ana");
console.log(typeof 20);
console.log(typeof true);
console.log(typeof undefined);
```

Resultado:

```txt
string
number
boolean
undefined
```

Exemplo prático:

```js
const idade = "20";

console.log(typeof idade);
```

Resultado:

```txt
string
```

---

# 25. Cuidados com typeof

Alguns resultados podem parecer estranhos.

Exemplo:

```js
console.log(typeof null);
```

Resultado:

```txt
object
```

Esse é um comportamento antigo do JavaScript.

Na prática, para verificar `null`, use:

```js
const valor = null;

console.log(valor === null);
```

Arrays também retornam `object` com `typeof`.

```js
const nomes = ["Ana", "Carlos"];

console.log(typeof nomes);
```

Resultado:

```txt
object
```

Para verificar se algo é array, use:

```js
console.log(Array.isArray(nomes));
```

---

# 26. Tipagem dinâmica

JavaScript possui tipagem dinâmica.

Isso significa que uma variável pode receber valores de tipos diferentes durante a execução.

Exemplo:

```js
let valor = 10;

valor = "Texto";

valor = true;
```

Isso é permitido.

Porém, não significa que seja uma boa prática mudar o tipo de uma variável sem necessidade.

Código assim pode dificultar a manutenção.

---

# 27. Conversão de tipos

Às vezes é necessário converter um valor de um tipo para outro.

## Convertendo para number

```js
const idadeTexto = "20";
const idade = Number(idadeTexto);

console.log(idade);
console.log(typeof idade);
```

Resultado:

```txt
20
number
```

## Convertendo para string

```js
const idade = 20;
const idadeTexto = String(idade);

console.log(idadeTexto);
console.log(typeof idadeTexto);
```

## Convertendo para boolean

```js
const valor = 1;
const booleano = Boolean(valor);

console.log(booleano);
```

Resultado:

```txt
true
```

---

# 28. Conversão implícita

JavaScript às vezes converte valores automaticamente.

Exemplo:

```js
console.log("10" + 5);
```

Resultado:

```txt
105
```

Nesse caso, o número `5` foi convertido para string.

Outro exemplo:

```js
console.log("10" - 5);
```

Resultado:

```txt
5
```

Nesse caso, a string `"10"` foi convertida para number.

Esse comportamento pode causar confusão.

Por isso, prefira conversões explícitas:

```js
const valor = Number("10");

console.log(valor + 5);
```

---

# 29. Comparação de valores

JavaScript possui dois tipos comuns de comparação:

```js
==
===
```

## Igualdade solta

O operador `==` compara valores permitindo conversão automática de tipos.

Exemplo:

```js
console.log("10" == 10);
```

Resultado:

```txt
true
```

## Igualdade estrita

O operador `===` compara valor e tipo.

Exemplo:

```js
console.log("10" === 10);
```

Resultado:

```txt
false
```

Recomenda-se usar `===` na maior parte dos casos.

---

# 30. Truthy e falsy

Em condições, alguns valores são tratados como `false`.

Valores falsy:

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
} else {
    console.log("Nome vazio");
}
```

Resultado:

```txt
Nome vazio
```

Valores que não são falsy geralmente são truthy.

Exemplo:

```js
const nome = "Ana";

if (nome) {
    console.log("Nome informado");
}
```

---

# 31. NaN

`NaN` significa `Not a Number`.

Ele aparece quando uma operação numérica inválida é realizada.

Exemplo:

```js
const resultado = Number("abc");

console.log(resultado);
```

Resultado:

```txt
NaN
```

Para verificar se um valor é `NaN`, use:

```js
console.log(Number.isNaN(resultado));
```

---

# 32. Boas práticas com variáveis

## Use nomes claros

Evite:

```js
const x = 10;
const y = 5;
```

Prefira:

```js
const preco = 10;
const quantidade = 5;
```

---

## Use const por padrão

Prefira:

```js
const nome = "Ana";
```

Use `let` apenas quando o valor precisar mudar.

---

## Evite var

Em código moderno, prefira `let` e `const`.

---

## Não reutilize variáveis para tipos diferentes

Evite:

```js
let usuario = "Ana";

usuario = {
    nome: "Ana"
};
```

Prefira criar variáveis com responsabilidades claras.

---

## Declare variáveis perto de onde serão usadas

Isso facilita a leitura e reduz confusão.

---

# 33. Exemplo completo

```js
const nome = "Ana";
const idade = 20;
const possuiCadastro = true;
const endereco = null;

const usuario = {
    nome: nome,
    idade: idade,
    possuiCadastro: possuiCadastro,
    endereco: endereco
};

console.log(usuario);
console.log(typeof usuario.nome);
console.log(typeof usuario.idade);
console.log(typeof usuario.possuiCadastro);
console.log(usuario.endereco === null);
```

Versão mais curta:

```js
const nome = "Ana";
const idade = 20;
const possuiCadastro = true;
const endereco = null;

const usuario = {
    nome,
    idade,
    possuiCadastro,
    endereco
};

console.log(usuario);
```

---

# 34. Exercícios práticos

## Exercício 1

Crie três variáveis:

```txt
nome
idade
cidade
```

Depois, exiba os valores no console.

---

## Exercício 2

Crie uma variável `preco` e uma variável `quantidade`.

Calcule o total da compra.

---

## Exercício 3

Crie uma variável com o valor `"25"` em formato de texto.

Converta esse valor para number e some com `10`.

---

## Exercício 4

Crie um objeto `usuario` com as propriedades:

```txt
nome
idade
email
ativo
```

Depois, exiba cada propriedade no console.

---

## Exercício 5

Crie um array com três nomes.

Depois:

```txt
Exiba o primeiro nome.
Adicione um novo nome.
Remova o último nome.
Exiba o array final.
```

---

## Exercício 6

Analise o resultado:

```js
console.log("10" + 5);
console.log("10" - 5);
console.log("10" === 10);
console.log("10" == 10);
```

Explique o motivo de cada resultado.

---

## Exercício 7

Crie uma função que receba `nome` e `idade`.

A função deve retornar uma frase usando template string.

Exemplo:

```txt
Ana tem 20 anos.
```

---

## Exercício 8

Crie uma variável com valor `null`.

Depois, verifique se ela é realmente `null` usando comparação estrita.

---

# 35. Desafio final

Crie um pequeno cadastro de produto.

O produto deve ter:

```txt
nome
preco
quantidade
disponivel
categorias
```

Depois:

```txt
Exiba o tipo de cada propriedade.
Calcule o valor total em estoque.
Verifique se o produto está disponível.
Adicione uma nova categoria.
Exiba o objeto final.
```

Exemplo esperado de estrutura:

```js
const produto = {
    nome: "Mouse",
    preco: 50,
    quantidade: 10,
    disponivel: true,
    categorias: ["informática", "periféricos"]
};
```

---

# 36. Conclusão

Variáveis são a base para armazenar e manipular dados em JavaScript.

Os tipos definem a natureza desses dados e influenciam diretamente o comportamento do código.

Entender variáveis, escopo, tipos, conversões e comparações é essencial para escrever códigos mais claros, seguros e previsíveis.

Dominar esses conceitos facilita o aprendizado de estruturas mais avançadas, como funções, objetos, arrays, classes, módulos e programação assíncrona.
