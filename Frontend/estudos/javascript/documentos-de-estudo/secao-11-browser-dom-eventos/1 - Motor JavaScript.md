# Motor JavaScript

O motor JavaScript é a parte responsável por transformar código JavaScript em execução real.

Sem o motor, um arquivo `.js` é apenas texto. O motor interpreta, compila, otimiza e executa esse código.

---

# 1 - Exemplos de motores JavaScript

Motores famosos:

- V8: usado no Google Chrome e no Node.js;
- SpiderMonkey: usado no Firefox;
- JavaScriptCore: usado no Safari;
- Chakra: usado em versões antigas do Microsoft Edge.

Cada navegador possui ou usa um motor para executar JavaScript.

---

# 2 - Por que estudar o motor

Entender o motor ajuda a compreender:

- por que JavaScript não executa texto diretamente;
- como funções entram e saem da call stack;
- onde objetos ficam na memória;
- por que algumas operações assíncronas não travam a tela;
- como otimizações podem melhorar ou piorar performance;
- como DOM, eventos e event loop se conectam.

Não é necessário decorar detalhes internos, mas entender o fluxo geral melhora a leitura de código.

---

# 3 - Pipeline simplificado

De forma simplificada:

```txt
Código JavaScript -> Parser -> AST -> Bytecode/compilação -> Execução -> Otimizações
```

O motor não executa o texto bruto diretamente.

Ele transforma o código em estruturas internas que consegue entender e executar.

---

# 4 - Parser e AST

O parser lê o código e cria uma AST.

AST significa Abstract Syntax Tree.

Ela representa o código em formato de árvore.

Exemplo:

```js
let idade = 20;
```

O motor entende que existe:

- uma declaração de variável;
- um identificador chamado `idade`;
- um valor literal `20`;
- uma atribuição.

Essa estrutura facilita análise, execução e otimização.

---

# 5 - Execução e call stack

A call stack controla a execução das funções.

```js
function a() {
    b();
}

function b() {
    console.log("b");
}

a();
```

Fluxo:

1. `a()` entra na stack;
2. `b()` entra na stack;
3. `console.log()` entra na stack;
4. `console.log()` termina e sai;
5. `b()` termina e sai;
6. `a()` termina e sai.

A stack segue a regra LIFO: o último que entra é o primeiro que sai.

---

# 6 - Heap e objetos

Objetos, arrays e funções ficam na heap.

```js
const usuario = {
    nome: "Nícolas"
};
```

De forma simplificada:

- o objeto fica na heap;
- a variável `usuario` guarda uma referência para esse objeto.

Esse assunto se conecta com `Frontend/estudos/javascript/documentos-de-estudo/secao-07-memoria/1 - Memória.md`.

---

# 7 - Garbage collector

O garbage collector libera memória que não está mais acessível.

```js
let usuario = {
    nome: "Nícolas"
};

usuario = null;
```

Quando o objeto deixa de ter referências, ele pode ser removido da memória.

O desenvolvedor não controla exatamente quando essa limpeza acontece.

---

# 8 - JIT e otimizações

Motores modernos usam otimizações em tempo de execução.

No V8, por exemplo, existe um fluxo com interpretador e otimizador.

Ideia prática:

- o código começa executando;
- o motor observa padrões;
- funções muito usadas podem ser otimizadas;
- se os padrões mudam, otimizações podem ser descartadas.

Por isso, código previsível e com tipos mais estáveis tende a ser mais fácil de otimizar.

Exemplo:

```js
function somar(a, b) {
    return a + b;
}

somar(1, 2);
somar(3, 4);
somar("a", "b");
```

Misturar tipos pode tornar o comportamento menos previsível para otimizações.

Isso não significa que você precisa micro-otimizar tudo. Primeiro escreva código claro.

---

# 9 - Motor JavaScript e navegador

O motor JavaScript não é o navegador inteiro.

O navegador também possui outras partes responsáveis por:

- interpretar HTML;
- interpretar CSS;
- montar DOM;
- calcular layout;
- pintar pixels na tela;
- gerenciar rede;
- controlar eventos.

O JavaScript conversa com essas APIs do navegador, mas elas não pertencem ao motor puro da linguagem.

---

# 10 - Exemplo prático completo

```js
function criarUsuario(nome) {
    return {
        nome,
        ativo: true
    };
}

function exibirUsuario(usuario) {
    console.log(usuario.nome);
}

const usuario = criarUsuario("Nícolas");

exibirUsuario(usuario);
```

Nesse exemplo:

- funções entram e saem da call stack;
- o objeto retornado fica na heap;
- a variável `usuario` guarda referência;
- o motor executa as instruções;
- `console.log` usa uma API disponível no ambiente.

---

# 11 - Erros comuns

### Achar que JavaScript é só interpretado

Motores modernos fazem otimizações e compilação em tempo de execução.

### Confundir motor com navegador

DOM, CSS, layout e rede são recursos do navegador. O motor executa JavaScript.

### Tentar otimizar antes de medir

Entender o motor é útil, mas micro-otimização sem evidência costuma piorar legibilidade.

---

# 12 - Relação com outros estudos

Este conteúdo se conecta com memória, DOM, eventos, assincronismo e event loop.

Antes de estudar DOM e eventos, vale entender que o motor JavaScript executa o código, mas o navegador fornece as APIs para manipular a página.

---

# 13 - Conclusão

O motor JavaScript é quem transforma código em execução.

Entender parser, AST, call stack, heap, garbage collector e otimizações ajuda a enxergar melhor o que acontece por trás do código, sem perder o foco principal: escrever código claro, previsível e fácil de manter.
