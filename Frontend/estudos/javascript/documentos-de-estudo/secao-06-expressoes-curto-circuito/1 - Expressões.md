# Expressões em JavaScript

Expressão é qualquer pedaço de código que produz um valor.

Entender expressões ajuda a ler melhor condicionais, atribuições, retornos de funções, arrow functions, operadores lógicos e avaliações de curto-circuito.

---

# 1 - O que é uma expressão

Uma expressão sempre resulta em algum valor.

Exemplos:

```js
2 + 2;
"Olá " + "Nícolas";
idade >= 18;
usuario.nome;
somar(2, 3);
```

Cada linha acima produz um valor:

- `2 + 2` produz `4`;
- `"Olá " + "Nícolas"` produz uma string;
- `idade >= 18` produz `true` ou `false`;
- `usuario.nome` produz o valor da propriedade;
- `somar(2, 3)` produz o retorno da função.

---

# 2 - Expressão vs instrução

Uma expressão produz valor.

Uma instrução executa uma ação.

Expressão:

```js
const resultado = 10 + 5;
```

`10 + 5` é uma expressão, porque produz `15`.

Instrução:

```js
if (resultado > 10) {
    console.log("Maior que 10");
}
```

O `if` é uma instrução de controle de fluxo. Ele decide qual bloco executar.

Você não pode usar um `if` tradicional como valor direto:

```js
// Inválido
const mensagem = if (idade >= 18) {
    "Maior";
};
```

Para isso, use operador ternário.

```js
const mensagem = idade >= 18 ? "Maior" : "Menor";
```

---

# 3 - Por que isso importa

Saber diferenciar expressão de instrução ajuda a entender por que alguns códigos funcionam em certos lugares e outros não.

Exemplo:

```js
const dobro = (numero) => numero * 2;
```

`numero * 2` é uma expressão. Por isso, a arrow function consegue retornar esse valor implicitamente.

Agora:

```js
const validar = (idade) => {
    if (idade >= 18) {
        return "Maior";
    }

    return "Menor";
};
```

Aqui usamos bloco `{}` porque existe uma instrução `if` dentro da função.

---

# 4 - Expressões de atribuição

A atribuição também produz um valor.

```js
let x;
const y = (x = 10);

console.log(x); // 10
console.log(y); // 10
```

Mesmo sendo possível, esse tipo de código pode reduzir legibilidade.

Em código profissional, prefira separar quando a leitura ficar confusa.

```js
let x = 10;
const y = x;
```

---

# 5 - Expressões de função

Uma função pode ser criada como expressão e armazenada em variável.

```js
const somar = function(a, b) {
    return a + b;
};

console.log(somar(2, 3)); // 5
```

Arrow functions também são expressões.

```js
const somar = (a, b) => a + b;
```

Isso é muito comum em callbacks:

```js
const numeros = [1, 2, 3];

const dobrados = numeros.map((numero) => numero * 2);
```

---

# 6 - Expressões lógicas

Operadores lógicos também retornam valores.

```js
console.log(true && "ativo"); // "ativo"
console.log(false || "padrão"); // "padrão"
console.log(null ?? "sem valor"); // "sem valor"
```

Esse comportamento é a base da avaliação de curto-circuito.

O conteúdo é aprofundado em `Frontend/estudos/javascript/documentos-de-estudo/secao-06-expressoes-curto-circuito/2 - Avaliação de curto-circuito.md`.

---

# 7 - Expressões em retornos

Funções geralmente retornam expressões.

```js
function calcularDesconto(preco, percentual) {
    return preco * percentual;
}
```

`preco * percentual` é a expressão retornada.

Também pode retornar uma expressão mais completa:

```js
function usuarioPodeComprar(usuario) {
    return usuario.ativo && usuario.idade >= 18;
}
```

Esse tipo de retorno é comum, mas deve continuar legível.

---

# 8 - Exemplo prático completo

```js
function criarResumoUsuario(usuario) {
    const status = usuario.ativo ? "Ativo" : "Inativo";
    const nomeFormatado = usuario.nome.trim();
    const podeAcessar = usuario.ativo && usuario.idade >= 18;

    return {
        nome: nomeFormatado,
        status,
        podeAcessar
    };
}

const resumo = criarResumoUsuario({
    nome: " Nícolas ",
    idade: 20,
    ativo: true
});

console.log(resumo);
```

Nesse exemplo:

- o ternário produz o valor de `status`;
- `trim()` produz uma nova string;
- `&&` produz um booleano;
- o objeto retornado também é uma expressão.

---

# 9 - Erros comuns

### Confundir expressão com instrução

```js
const resultado = if (ativo) {
    "Ativo";
};
```

Use ternário quando precisa produzir valor.

```js
const resultado = ativo ? "Ativo" : "Inativo";
```

### Criar expressão grande demais

```js
const permitido = usuario && usuario.ativo && usuario.perfil === "admin" && usuario.configuracoes && usuario.configuracoes.acesso;
```

Esse código funciona, mas é difícil de ler.

Prefira quebrar:

```js
const usuarioAtivo = usuario && usuario.ativo;
const usuarioAdmin = usuario && usuario.perfil === "admin";
const possuiAcesso = usuario && usuario.configuracoes && usuario.configuracoes.acesso;

const permitido = usuarioAtivo && usuarioAdmin && possuiAcesso;
```

---

# 10 - Relação com outros estudos

Expressões se conectam com funções, operadores lógicos, curto-circuito, condicionais, arrays e retornos.

Antes de estudar curto-circuito, é importante entender que operadores lógicos não retornam apenas `true` ou `false`; eles retornam valores.

---

# 11 - Conclusão

Expressões são pequenas partes do código que produzem valores.

Esse conceito parece simples, mas ajuda a entender muita coisa em JavaScript moderno: ternários, arrow functions, retornos, operadores lógicos, callbacks e composição de dados.
