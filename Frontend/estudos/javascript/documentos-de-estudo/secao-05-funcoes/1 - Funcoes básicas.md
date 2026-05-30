# Funções em JavaScript

Funções são blocos de código reutilizáveis que executam uma tarefa específica.

Elas permitem organizar o código, evitar repetição e separar responsabilidades.

Exemplo:

```js
function saudacao() {
    console.log("Olá");
}
````

Nesse exemplo, foi criada uma função chamada `saudacao`.

---

# 1. Por que usar funções?

Sem funções:

```js
console.log("Bem-vindo");
console.log("Bem-vindo");
console.log("Bem-vindo");
```

Com função:

```js
function mostrarMensagem() {
    console.log("Bem-vindo");
}

mostrarMensagem();
mostrarMensagem();
mostrarMensagem();
```

A função evita repetição e facilita manutenção.

Se precisar alterar a mensagem, basta mudar em um único lugar.

---

# 2. Criando uma função

Sintaxe:

```js
function nomeDaFuncao() {
    // código
}
```

Exemplo:

```js
function dizerOla() {
    console.log("Olá");
}
```

Criar a função não executa ela automaticamente.

---

# 3. Chamando uma função

Para executar uma função, é necessário chamá-la.

Exemplo:

```js
function dizerOla() {
    console.log("Olá");
}

dizerOla();
```

Resultado:

```txt
Olá
```

Os parênteses executam a função.

Sem eles:

```js
dizerOla
```

A função não será executada.

---

# 4. Parâmetros

Parâmetros são valores que a função recebe.

Exemplo:

```js
function cumprimentar(nome) {
    console.log("Olá, " + nome);
}
```

Chamando:

```js
cumprimentar("Ana");
```

Resultado:

```txt
Olá, Ana
```

`nome` existe apenas dentro da função.

---

# 5. Mais de um parâmetro

Uma função pode receber vários parâmetros.

Exemplo:

```js
function apresentar(nome, idade) {
    console.log(nome + " tem " + idade + " anos");
}
```

Chamando:

```js
apresentar("Carlos", 25);
```

Resultado:

```txt
Carlos tem 25 anos
```

A ordem importa.

```js
apresentar(25, "Carlos");
```

Resultado incorreto.

---

# 6. Retorno

Funções podem devolver valores usando `return`.

Exemplo:

```js
function somar(a, b) {
    return a + b;
}
```

Uso:

```js
const resultado = somar(10, 5);

console.log(resultado);
```

Resultado:

```txt
15
```

Sem `return`, a função não devolve valor útil.

---

# 7. Diferença entre console.log e return

Com `console.log`:

```js
function somar(a, b) {
    console.log(a + b);
}
```

Isso apenas exibe o valor.

Com `return`:

```js
function somar(a, b) {
    return a + b;
}
```

Agora o valor pode ser armazenado, reutilizado ou manipulado.

Exemplo:

```js
const total = somar(10, 5) * 2;
```

---

# 8. Funções sem retorno

Nem toda função precisa retornar algo.

Exemplo:

```js
function mostrarMensagem() {
    console.log("Operação concluída");
}
```

Ela apenas executa uma ação.

---

# 9. Valores padrão

Parâmetros podem ter valores padrão.

Exemplo:

```js
function cumprimentar(nome = "Visitante") {
    console.log("Olá, " + nome);
}
```

Chamando:

```js
cumprimentar();
```

Resultado:

```txt
Olá, Visitante
```

---

# 10. Escopo

Variáveis criadas dentro da função só existem nela.

Exemplo:

```js
function teste() {
    const nome = "Ana";
}

console.log(nome);
```

Isso gera erro.

Porque `nome` só existe dentro da função.

---

# 11. Função com lógica simples

Exemplo:

```js
function verificarIdade(idade) {
    if (idade >= 18) {
        return "Maior de idade";
    }

    return "Menor de idade";
}
```

Uso:

```js
console.log(verificarIdade(20));
```

Resultado:

```txt
Maior de idade
```

---

# 12. Boas práticas

## Use nomes claros

Ruim:

```js
function x() {
}
```

Melhor:

```js
function calcularTotal() {
}
```

---

## Uma função, uma responsabilidade

Ruim:

```js
function fazerTudo() {
}
```

Melhor:

```js
calcularPreco()
validarUsuario()
enviarEmail()
```

---

## Prefira funções pequenas

Funções muito grandes dificultam leitura e manutenção.

---

# Conclusão

Funções são fundamentais em JavaScript.

Elas permitem reutilizar código, organizar responsabilidades e tornar a aplicação mais legível.

Entender criação, parâmetros, retorno e escopo é a base para trabalhar com funções mais avançadas futuramente.