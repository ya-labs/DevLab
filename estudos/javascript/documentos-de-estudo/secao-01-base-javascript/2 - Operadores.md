# Operadores em JavaScript

Operadores são símbolos ou palavras usados para realizar operações com valores e variáveis.

Eles permitem fazer cálculos, comparações, atribuições, validações lógicas e manipulações de dados.

Exemplos:

```js
const soma = 10 + 5;
const maiorDeIdade = idade >= 18;
const usuarioAtivo = ativo && possuiPermissao;
````

---

# 1. Operadores aritméticos

Operadores aritméticos são usados para realizar cálculos matemáticos.

| Operador | Nome             | Exemplo  | Resultado |
| -------- | ---------------- | -------- | --------- |
| `+`      | Adição           | `10 + 5` | `15`      |
| `-`      | Subtração        | `10 - 5` | `5`       |
| `*`      | Multiplicação    | `10 * 5` | `50`      |
| `/`      | Divisão          | `10 / 5` | `2`       |
| `%`      | Resto da divisão | `10 % 3` | `1`       |
| `**`     | Exponenciação    | `2 ** 3` | `8`       |

Exemplo:

```js
const preco = 100;
const desconto = 20;

const total = preco - desconto;

console.log(total);
```

Resultado:

```txt
80
```

---

# 2. Operador de adição com textos

O operador `+` também pode ser usado para concatenar strings.

Exemplo:

```js
const nome = "Ana";
const sobrenome = "Silva";

const nomeCompleto = nome + " " + sobrenome;

console.log(nomeCompleto);
```

Resultado:

```txt
Ana Silva
```

Quando um dos valores é string, o JavaScript pode converter o outro valor para string automaticamente.

Exemplo:

```js
console.log("10" + 5);
```

Resultado:

```txt
105
```

Nesse caso, o número `5` foi convertido para texto.

---

# 3. Ordem de precedência

JavaScript segue uma ordem de prioridade nas operações matemáticas.

Exemplo:

```js
const resultado = 10 + 5 * 2;

console.log(resultado);
```

Resultado:

```txt
20
```

A multiplicação é executada antes da adição.

Para mudar a ordem, use parênteses:

```js
const resultado = (10 + 5) * 2;

console.log(resultado);
```

Resultado:

```txt
30
```

---

# 4. Operadores de atribuição

Operadores de atribuição são usados para atribuir valores a variáveis.

| Operador | Exemplo  | Equivalente |
| -------- | -------- | ----------- |
| `=`      | `x = 10` | `x = 10`    |
| `+=`     | `x += 5` | `x = x + 5` |
| `-=`     | `x -= 5` | `x = x - 5` |
| `*=`     | `x *= 5` | `x = x * 5` |
| `/=`     | `x /= 5` | `x = x / 5` |
| `%=`     | `x %= 5` | `x = x % 5` |

Exemplo:

```js
let contador = 0;

contador += 1;
contador += 1;

console.log(contador);
```

Resultado:

```txt
2
```

---

# 5. Operadores de incremento e decremento

São usados para aumentar ou diminuir um valor em `1`.

## Incremento

```js
let contador = 0;

contador++;

console.log(contador);
```

Resultado:

```txt
1
```

## Decremento

```js
let contador = 5;

contador--;

console.log(contador);
```

Resultado:

```txt
4
```

Também é possível usar:

```js
contador = contador + 1;
contador += 1;
```

---

# 6. Pré-incremento e pós-incremento

Existe diferença entre `++contador` e `contador++`.

## Pós-incremento

Primeiro usa o valor, depois incrementa.

```js
let contador = 1;

console.log(contador++);
console.log(contador);
```

Resultado:

```txt
1
2
```

## Pré-incremento

Primeiro incrementa, depois usa o valor.

```js
let contador = 1;

console.log(++contador);
console.log(contador);
```

Resultado:

```txt
2
2
```

Na maioria dos casos simples, prefira usar o incremento em uma linha separada para melhorar a leitura.

```js
contador++;
console.log(contador);
```

---

# 7. Operadores de comparação

Operadores de comparação são usados para comparar valores.

O resultado sempre será um booleano:

```js
true
false
```

| Operador | Nome              | Exemplo       | Resultado |
| -------- | ----------------- | ------------- | --------- |
| `>`      | Maior que         | `10 > 5`      | `true`    |
| `<`      | Menor que         | `10 < 5`      | `false`   |
| `>=`     | Maior ou igual    | `10 >= 10`    | `true`    |
| `<=`     | Menor ou igual    | `5 <= 10`     | `true`    |
| `==`     | Igualdade solta   | `"10" == 10`  | `true`    |
| `===`    | Igualdade estrita | `"10" === 10` | `false`   |
| `!=`     | Diferente solto   | `"10" != 10`  | `false`   |
| `!==`    | Diferente estrito | `"10" !== 10` | `true`    |

---

# 8. Igualdade solta e igualdade estrita

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

O JavaScript converte a string `"10"` para number antes de comparar.

---

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

Nesse caso, os valores são diferentes porque os tipos são diferentes:

```txt
"10" é string
10 é number
```

Recomendação: use `===` e `!==` na maior parte dos casos.

---

# 9. Operadores lógicos

Operadores lógicos são usados para combinar condições.

| Operador | Nome | Significado                                 |    |                                                |
| -------- | ---- | ------------------------------------------- | -- | ---------------------------------------------- |
| `&&`     | AND  | Todas as condições precisam ser verdadeiras |    |                                                |
| `        |      | `                                           | OR | Pelo menos uma condição precisa ser verdadeira |
| `!`      | NOT  | Inverte o valor lógico                      |    |                                                |

---

# 10. Operador AND `&&`

O operador `&&` retorna verdadeiro apenas quando todas as condições são verdadeiras.

Exemplo:

```js
const idade = 20;
const possuiDocumento = true;

if (idade >= 18 && possuiDocumento) {
    console.log("Entrada permitida");
}
```

Nesse exemplo, a entrada só será permitida se:

```txt
idade for maior ou igual a 18
E possuir documento
```

---

# 11. Operador OR `||`

O operador `||` retorna verdadeiro quando pelo menos uma condição é verdadeira.

Exemplo:

```js
const possuiEmail = false;
const possuiTelefone = true;

if (possuiEmail || possuiTelefone) {
    console.log("Cadastro válido");
}
```

Nesse exemplo, o cadastro será considerado válido se tiver e-mail ou telefone.

---

# 12. Operador NOT `!`

O operador `!` inverte um valor booleano.

Exemplo:

```js
const ativo = false;

console.log(!ativo);
```

Resultado:

```txt
true
```

Uso comum:

```js
const usuarioLogado = false;

if (!usuarioLogado) {
    console.log("Usuário precisa fazer login");
}
```

---

# 13. Truthy e falsy com operadores lógicos

Em JavaScript, valores não booleanos também podem ser avaliados em condições.

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

if (!nome) {
    console.log("Nome não informado");
}
```

Como `nome` é uma string vazia, ele é considerado falsy.

---

# 14. Short-circuit

Operadores lógicos podem parar a avaliação antes de verificar tudo.

Isso é chamado de short-circuit.

## Short-circuit com AND

```js
const usuario = null;

usuario && console.log(usuario.nome);
```

Nesse caso, o `console.log` não será executado, pois `usuario` é `null`.

---

## Short-circuit com OR

```js
const nome = "";

const nomeExibicao = nome || "Usuário sem nome";

console.log(nomeExibicao);
```

Resultado:

```txt
Usuário sem nome
```

Como `nome` é falsy, o valor padrão é usado.

---

# 15. Operador ternário

O operador ternário é uma forma curta de escrever uma condição simples.

Sintaxe:

```js
condicao ? valorSeVerdadeiro : valorSeFalso;
```

Exemplo:

```js
const idade = 20;

const mensagem = idade >= 18 ? "Maior de idade" : "Menor de idade";

console.log(mensagem);
```

Resultado:

```txt
Maior de idade
```

Equivalente com `if`:

```js
let mensagem;

if (idade >= 18) {
    mensagem = "Maior de idade";
} else {
    mensagem = "Menor de idade";
}
```

Use ternário apenas quando a condição for simples.

---

# 16. Operador nullish coalescing `??`

O operador `??` retorna o valor da direita apenas quando o valor da esquerda é `null` ou `undefined`.

Exemplo:

```js
const nome = null;

const nomeExibicao = nome ?? "Usuário sem nome";

console.log(nomeExibicao);
```

Resultado:

```txt
Usuário sem nome
```

Diferença importante entre `||` e `??`:

```js
const quantidade = 0;

console.log(quantidade || 10);
console.log(quantidade ?? 10);
```

Resultado:

```txt
10
0
```

Com `||`, o `0` é considerado falsy.

Com `??`, o `0` é considerado um valor válido.

---

# 17. Optional chaining `?.`

O optional chaining permite acessar propriedades de forma segura.

Exemplo:

```js
const usuario = null;

console.log(usuario?.nome);
```

Resultado:

```txt
undefined
```

Sem optional chaining, o código geraria erro:

```js
console.log(usuario.nome);
```

Uso com objetos aninhados:

```js
const usuario = {
    nome: "Ana",
    endereco: null
};

console.log(usuario.endereco?.rua);
```

---

# 18. Operador spread `...`

O spread permite espalhar valores de arrays ou objetos.

## Spread em arrays

```js
const numeros = [1, 2, 3];
const novosNumeros = [...numeros, 4, 5];

console.log(novosNumeros);
```

Resultado:

```txt
[1, 2, 3, 4, 5]
```

## Spread em objetos

```js
const usuario = {
    nome: "Ana",
    idade: 20
};

const usuarioAtualizado = {
    ...usuario,
    idade: 21
};

console.log(usuarioAtualizado);
```

Resultado:

```txt
{ nome: "Ana", idade: 21 }
```

Esse recurso é muito usado para copiar e atualizar dados sem alterar diretamente o objeto original.

---

# 19. Operador rest `...`

O operador rest também usa `...`, mas tem outra função.

Ele agrupa valores restantes.

## Rest em funções

```js
function somar(...numeros) {
    let total = 0;

    for (const numero of numeros) {
        total += numero;
    }

    return total;
}

console.log(somar(1, 2, 3, 4));
```

Resultado:

```txt
10
```

## Rest em arrays

```js
const numeros = [1, 2, 3, 4];

const [primeiro, ...restante] = numeros;

console.log(primeiro);
console.log(restante);
```

Resultado:

```txt
1
[2, 3, 4]
```

---

# 20. Operador typeof

O operador `typeof` retorna o tipo de um valor.

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

Cuidados:

```js
console.log(typeof null);
```

Resultado:

```txt
object
```

Esse é um comportamento antigo do JavaScript.

Para verificar `null`, use:

```js
const valor = null;

console.log(valor === null);
```

Arrays também retornam `object`:

```js
const nomes = ["Ana", "Carlos"];

console.log(typeof nomes);
console.log(Array.isArray(nomes));
```

---

# 21. Operador instanceof

O operador `instanceof` verifica se um objeto foi criado a partir de uma função construtora ou classe.

Exemplo:

```js
const data = new Date();

console.log(data instanceof Date);
```

Resultado:

```txt
true
```

Exemplo com array:

```js
const nomes = ["Ana", "Carlos"];

console.log(nomes instanceof Array);
```

Resultado:

```txt
true
```

Apesar disso, para verificar arrays, normalmente prefira:

```js
Array.isArray(nomes);
```

---

# 22. Operador delete

O operador `delete` remove uma propriedade de um objeto.

Exemplo:

```js
const usuario = {
    nome: "Ana",
    idade: 20
};

delete usuario.idade;

console.log(usuario);
```

Resultado:

```txt
{ nome: "Ana" }
```

Use com cuidado, pois remover propriedades pode dificultar a previsibilidade do objeto.

---

# 23. Operador in

O operador `in` verifica se uma propriedade existe em um objeto.

Exemplo:

```js
const usuario = {
    nome: "Ana",
    idade: 20
};

console.log("nome" in usuario);
console.log("email" in usuario);
```

Resultado:

```txt
true
false
```

Importante: `in` verifica se a propriedade existe, mesmo que o valor seja `undefined`.

```js
const usuario = {
    nome: undefined
};

console.log("nome" in usuario);
```

Resultado:

```txt
true
```

---

# 24. Desestruturação

A desestruturação permite extrair valores de arrays e objetos.

## Desestruturação de objetos

```js
const usuario = {
    nome: "Ana",
    idade: 20
};

const { nome, idade } = usuario;

console.log(nome);
console.log(idade);
```

## Desestruturação de arrays

```js
const coordenadas = [10, 20];

const [x, y] = coordenadas;

console.log(x);
console.log(y);
```

Embora não seja exatamente um operador único, a desestruturação é uma sintaxe muito usada junto com operadores modernos.

---

# 25. Operadores bitwise

Operadores bitwise trabalham com bits.

Eles são menos comuns em códigos iniciais, mas existem na linguagem.

| Operador | Nome                                |              |
| -------- | ----------------------------------- | ------------ |
| `&`      | AND bit a bit                       |              |
| `        | `                                   | OR bit a bit |
| `^`      | XOR bit a bit                       |              |
| `~`      | NOT bit a bit                       |              |
| `<<`     | Deslocamento para esquerda          |              |
| `>>`     | Deslocamento para direita           |              |
| `>>>`    | Deslocamento para direita sem sinal |              |

Exemplo:

```js
console.log(5 & 1);
```

Resultado:

```txt
1
```

Esses operadores são mais usados em casos específicos, como manipulação binária, permissões e operações de baixo nível.

---

# 26. Cuidados comuns

## Evite usar `==`

Prefira:

```js
valor === outroValor;
```

Em vez de:

```js
valor == outroValor;
```

---

## Cuidado com `+` entre string e number

```js
console.log("10" + 5);
```

Resultado:

```txt
105
```

Para somar corretamente:

```js
console.log(Number("10") + 5);
```

Resultado:

```txt
15
```

---

## Cuidado com ternários complexos

Evite:

```js
const status = idade >= 18 ? ativo ? "Liberado" : "Pendente" : "Bloqueado";
```

Prefira `if/else` quando a lógica for maior ou mais difícil de ler.

---

## Cuidado com `||` para valores padrão

```js
const quantidade = 0;

const valor = quantidade || 10;

console.log(valor);
```

Resultado:

```txt
10
```

Se `0` for um valor válido, use `??`:

```js
const valor = quantidade ?? 10;
```

---

# 27. Exemplo completo

```js
const produto = {
    nome: "Mouse",
    preco: 50,
    quantidade: 3,
    desconto: null
};

const desconto = produto.desconto ?? 0;
const subtotal = produto.preco * produto.quantidade;
const total = subtotal - desconto;

const possuiEstoque = produto.quantidade > 0;
const mensagem = possuiEstoque ? "Produto disponível" : "Produto indisponível";

console.log("Produto:", produto.nome);
console.log("Subtotal:", subtotal);
console.log("Total:", total);
console.log("Status:", mensagem);
```

Resultado:

```txt
Produto: Mouse
Subtotal: 150
Total: 150
Status: Produto disponível
```

---