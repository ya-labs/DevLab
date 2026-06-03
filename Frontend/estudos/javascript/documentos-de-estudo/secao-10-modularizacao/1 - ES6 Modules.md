# ES6 Modules

ES6 Modules, também chamados de ESM, são o sistema nativo de módulos do JavaScript.

Eles permitem dividir o código em arquivos separados e compartilhar funções, objetos, constantes e classes entre esses arquivos usando `export` e `import`.

---

# 1 - Por que módulos existem

Sem módulos, projetos grandes ficariam concentrados em poucos arquivos ou dependeriam de variáveis globais.

Isso causa problemas como:

- código difícil de manter;
- nomes em conflito;
- baixa reutilização;
- responsabilidades misturadas;
- dificuldade para testar;
- dificuldade para entender dependências.

Módulos resolvem isso permitindo separar o código por responsabilidade.

---

# 2 - Exportando e importando

Arquivo `math.js`:

```js
export function somar(a, b) {
    return a + b;
}
```

Arquivo `main.js`:

```js
import { somar } from "./math.js";

console.log(somar(2, 3)); // 5
```

O `export` torna a função disponível para outros arquivos.

O `import` traz a função para o arquivo atual.

---

# 3 - Named export

Named export permite exportar várias coisas no mesmo arquivo.

```js
export const PI = 3.14;

export function multiplicar(a, b) {
    return a * b;
}
```

Importando:

```js
import { PI, multiplicar } from "./math.js";
```

Esse é um padrão muito comum porque deixa explícito o que está sendo importado.

---

# 4 - Default export

Default export permite exportar um valor principal do arquivo.

```js
export default function formatarNome(nome) {
    return nome.trim();
}
```

Importando:

```js
import formatarNome from "./formatarNome.js";
```

O nome na importação pode ser escolhido livremente.

```js
import qualquerNome from "./formatarNome.js";
```

Por isso, em muitos times, named export é preferido para evitar confusão em refactors.

---

# 5 - Misturando default e named export

É possível misturar, mas use com cuidado.

```js
export const LIMITE = 10;

export default function listarUsuarios() {
    return [];
}
```

Importando:

```js
import listarUsuarios, { LIMITE } from "./usuarios.js";
```

Funciona, mas pode deixar o arquivo menos previsível se usado sem padrão.

---

# 6 - Módulos no navegador

No navegador, use `type="module"`.

```html
<script type="module" src="./main.js"></script>
```

Com isso:

- o arquivo roda em modo módulo;
- imports e exports funcionam;
- o escopo não polui o global automaticamente;
- o carregamento segue regras modernas do navegador.

Exemplo:

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>ES Modules</title>
</head>
<body>
    <script type="module" src="./main.js"></script>
</body>
</html>
```

---

# 7 - Módulos em projetos modernos

Frameworks e bundlers usam módulos o tempo todo.

Exemplo em React:

```js
import { useState } from "react";
import { buscarProdutos } from "./services/produtosService.js";
import ProdutoCard from "./components/ProdutoCard.jsx";
```

Na prática, ESM é base para:

- React;
- Vite;
- Angular moderno;
- Vue;
- bibliotecas npm;
- tree-shaking;
- organização por arquivos.

---

# 8 - Exemplo prático completo

`produtosService.js`:

```js
export async function buscarProdutos() {
    const response = await fetch("/api/produtos");

    if (!response.ok) {
        throw new Error("Erro ao buscar produtos");
    }

    return response.json();
}
```

`main.js`:

```js
import { buscarProdutos } from "./produtosService.js";

async function iniciar() {
    const produtos = await buscarProdutos();

    console.log(produtos);
}

iniciar();
```

Esse exemplo separa a responsabilidade de buscar dados da responsabilidade de iniciar a aplicação.

---

# 9 - Erros comuns

### Esquecer a extensão no navegador

```js
import { somar } from "./math";
```

No navegador puro, normalmente use:

```js
import { somar } from "./math.js";
```

### Criar dependência circular

Arquivo A importa B, e B importa A.

Isso pode gerar bugs difíceis de entender.

### Misturar muitos exports sem responsabilidade clara

Um arquivo chamado `utils.js` com dezenas de funções sem relação vira um ponto de bagunça.

Prefira arquivos com responsabilidade mais clara.

---

# 10 - Relação com outros estudos

ES6 Modules se conectam com funções, objetos, Fetch API e modularização moderna.

Depois deste conteúdo, faz sentido estudar `Frontend/estudos/javascript/documentos-de-estudo/secao-10-modularizacao/2 - Modularização moderna.md`.

---

# 11 - Conclusão

ES6 Modules são a base da organização de código JavaScript moderno.

Eles permitem dividir responsabilidades, reutilizar código e deixar dependências explícitas. Dominar `import` e `export` é obrigatório para trabalhar com aplicações frontend atuais.
