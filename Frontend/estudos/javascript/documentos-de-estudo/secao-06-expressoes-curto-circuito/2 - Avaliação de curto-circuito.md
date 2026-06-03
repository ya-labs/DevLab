# Avaliação de curto-circuito em JavaScript

Avaliação de curto-circuito acontece quando o JavaScript interrompe a leitura de uma expressão lógica assim que já consegue determinar o resultado.

Esse comportamento aparece principalmente com `&&`, `||` e `??`.

---

# 1 - Por que curto-circuito existe

Curto-circuito existe para evitar avaliações desnecessárias e permitir expressões mais flexíveis.

Exemplo:

```js
const usuario = null;

if (usuario && usuario.nome) {
    console.log(usuario.nome);
}
```

Nesse caso, o JavaScript avalia `usuario`.

Como `usuario` é `null`, ele não tenta acessar `usuario.nome`.

Isso evita erro.

---

# 2 - Valores truthy e falsy

Em JavaScript, alguns valores se comportam como falso em contexto booleano.

Valores falsy:

- `false`;
- `0`;
- `-0`;
- `0n`;
- `""`;
- `null`;
- `undefined`;
- `NaN`.

Todo o restante tende a ser truthy.

Exemplos truthy:

- `"texto"`;
- `"0"`;
- `"false"`;
- `[]`;
- `{}`;
- `1`;
- `true`.

Ponto importante:

> Array vazio e objeto vazio são truthy.

```js
if ([]) {
    console.log("Array vazio é truthy");
}
```

---

# 3 - Operador AND (`&&`)

O `&&` retorna o primeiro valor falsy encontrado.

Se todos forem truthy, retorna o último valor.

```js
console.log("teste" && null && "opa"); // null
console.log(true && "valor" && 10); // 10
```

Uso comum:

```js
const usuario = {
    nome: "Nícolas"
};

usuario && console.log(usuario.nome);
```

Em código moderno, para acessar propriedades com segurança, normalmente é melhor usar optional chaining.

```js
console.log(usuario?.nome);
```

---

# 4 - Operador OR (`||`)

O `||` retorna o primeiro valor truthy encontrado.

Se todos forem falsy, retorna o último valor.

```js
console.log(0 || false || "teste"); // "teste"
console.log(null || undefined || 0); // 0
```

Uso comum:

```js
const nome = "";
const nomeExibicao = nome || "Usuário sem nome";

console.log(nomeExibicao); // "Usuário sem nome"
```

Mas cuidado: `||` trata `0`, `""` e `false` como ausência de valor.

Isso pode ser um problema quando esses valores são válidos.

---

# 5 - Operador de coalescência nula (`??`)

O `??` retorna o valor da direita apenas quando o valor da esquerda é `null` ou `undefined`.

```js
console.log(0 ?? 10); // 0
console.log("" ?? "padrão"); // ""
console.log(null ?? "padrão"); // "padrão"
console.log(undefined ?? 5); // 5
```

Na prática, `??` é melhor que `||` quando `0`, `false` ou string vazia são valores válidos.

Exemplo:

```js
const quantidade = 0;
const quantidadeFinal = quantidade ?? 1;

console.log(quantidadeFinal); // 0
```

Com `||`, o resultado seria `1`, o que poderia gerar bug.

---

# 6 - Optional chaining (`?.`)

Optional chaining permite acessar propriedades sem quebrar o código quando algo é `null` ou `undefined`.

```js
const usuario = null;

console.log(usuario?.nome); // undefined
```

Sem optional chaining:

```js
console.log(usuario.nome); // erro
```

Muito usado em respostas de API:

```js
const cidade = usuario?.endereco?.cidade ?? "Cidade não informada";
```

---

# 7 - Exemplo prático completo

```js
function criarResumoUsuario(usuario) {
    const nome = usuario?.nome?.trim() || "Usuário sem nome";
    const idade = usuario?.idade ?? "Idade não informada";
    const ativo = usuario?.ativo ?? false;

    return {
        nome,
        idade,
        ativo
    };
}

console.log(criarResumoUsuario(null));
console.log(criarResumoUsuario({ nome: "", idade: 0, ativo: false }));
```

Esse exemplo mostra uma diferença importante:

- `||` é usado para nome vazio, porque string vazia não deve ser exibida;
- `??` é usado para idade e ativo, porque `0` e `false` podem ser valores válidos.

---

# 8 - Erros comuns

### Usar `||` quando `0` é válido

```js
const pagina = 0;
const paginaAtual = pagina || 1;

console.log(paginaAtual); // 1
```

Se `0` for válido, prefira:

```js
const paginaAtual = pagina ?? 1;
```

### Achar que `&&` sempre retorna booleano

```js
console.log("ok" && 10); // 10
```

Operadores lógicos retornam valores, não apenas `true` ou `false`.

### Misturar muita lógica em uma linha

```js
const valor = usuario && usuario.config && usuario.config.tema || "claro";
```

Prefira uma versão mais clara:

```js
const valor = usuario?.config?.tema ?? "claro";
```

---

# 9 - Relação com outros estudos

Este conteúdo depende de `Frontend/estudos/javascript/documentos-de-estudo/secao-06-expressoes-curto-circuito/1 - Expressões.md`.

Também aparece em objetos, funções, validações, consumo de APIs e renderização condicional em React.

---

# 10 - Conclusão

Curto-circuito é um recurso muito útil, mas precisa ser usado com intenção.

Use `&&` para depender de valores truthy, `||` para fallback quando falsy deve cair no padrão e `??` quando apenas `null` ou `undefined` devem ser tratados como ausência de valor.
