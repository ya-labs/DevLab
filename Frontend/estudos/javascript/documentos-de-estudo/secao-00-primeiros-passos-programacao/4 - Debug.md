# Debug em JavaScript

Debug é o processo de identificar, analisar e corrigir erros em um programa.

Durante o desenvolvimento, é comum que o código apresente comportamentos inesperados. Esses problemas podem estar relacionados a valores incorretos, condições mal definidas, funções mal utilizadas, erros de lógica, requisições assíncronas ou falhas na comunicação com APIs.

Debugar é investigar o funcionamento do código para entender onde o problema acontece e como ele pode ser corrigido.

---

# 1. O que é debug?

Debug é a prática de encontrar e corrigir bugs.

Bug é qualquer erro ou comportamento inesperado em um sistema.

Exemplo:

```js
const idade = "18";

if (idade === 18) {
    console.log("Maior de idade");
} else {
    console.log("Menor de idade");
}
````

Nesse exemplo, o resultado será:

```txt
Menor de idade
```

Isso acontece porque o valor `"18"` é uma string, enquanto `18` é um number.

Como o operador `===` compara valor e tipo, os valores são considerados diferentes.

Correção:

```js
const idade = 18;

if (idade === 18) {
    console.log("Maior de idade");
} else {
    console.log("Menor de idade");
}
```

---

# 2. Tipos de erro

Nem todo erro aparece de forma explícita no console. Alguns erros interrompem a execução do programa, enquanto outros apenas geram resultados incorretos.

## 2.1 Erro explícito

É o erro exibido diretamente pelo JavaScript.

Exemplo:

```js
const usuario = null;

console.log(usuario.nome);
```

Esse código gera um erro, pois não é possível acessar a propriedade `nome` de um valor `null`.

---

## 2.2 Erro lógico

É quando o código executa, mas gera um resultado incorreto.

Exemplo:

```js
const preco = 100;
const desconto = 20;

const total = preco + desconto;

console.log(total);
```

O resultado será:

```txt
120
```

Porém, se o objetivo era aplicar um desconto, o correto seria:

```js
const total = preco - desconto;
```

Erros lógicos costumam ser mais difíceis de identificar, pois nem sempre geram mensagens de erro.

---

# 3. Mentalidade para debugar

Antes de alterar o código, é importante responder a três perguntas:

```txt
O que eu esperava que acontecesse?
O que realmente aconteceu?
Em qual ponto o comportamento deixou de ser o esperado?
```

O debug deve ser feito com base em evidências.

Evite alterar várias partes do código ao mesmo tempo sem entender a causa do problema.

---

# 4. Usando console.log

O `console.log` é uma das formas mais simples de inspecionar valores durante a execução do programa.

Exemplo:

```js
function calcularTotal(preco, quantidade) {
    console.log("Preço:", preco);
    console.log("Quantidade:", quantidade);

    const total = preco * quantidade;

    console.log("Total:", total);

    return total;
}

calcularTotal(10, 3);
```

Saída:

```txt
Preço: 10
Quantidade: 3
Total: 30
```

---

# 5. Escrevendo logs claros

Evite logs sem contexto:

```js
console.log(valor);
console.log(valor2);
console.log(valor3);
```

Prefira logs descritivos:

```js
console.log("Valor do produto:", valor);
console.log("Quantidade:", valor2);
console.log("Total calculado:", valor3);
```

Também é possível imprimir os dados como objeto:

```js
console.log({
    preco,
    quantidade,
    total
});
```

Isso facilita a leitura e a análise dos valores.

---

# 6. Usando console.table

O `console.table` é útil para visualizar arrays de objetos.

Exemplo:

```js
const usuarios = [
    { id: 1, nome: "Ana", idade: 20 },
    { id: 2, nome: "Carlos", idade: 25 },
    { id: 3, nome: "João", idade: 17 }
];

console.table(usuarios);
```

No console do navegador, os dados serão exibidos em formato de tabela.

---

# 7. console.warn e console.error

Além de `console.log`, existem outros métodos úteis.

## console.warn

Indica um aviso:

```js
console.warn("Usuário não possui e-mail cadastrado");
```

## console.error

Indica um erro:

```js
console.error("Erro ao carregar usuários");
```

Esses métodos ajudam a diferenciar mensagens comuns, avisos e erros.

---

# 8. Debugando condicionais

Condicionais são uma fonte comum de erros.

Exemplo:

```js
const idade = 17;

if (idade > 18) {
    console.log("Pode entrar");
} else {
    console.log("Não pode entrar");
}
```

Se a regra for permitir pessoas com 18 anos ou mais, a condição está incorreta.

Correção:

```js
if (idade >= 18) {
    console.log("Pode entrar");
}
```

Para debugar condicionais, imprima os valores analisados:

```js
console.log("Idade:", idade);
console.log("Condição idade >= 18:", idade >= 18);
```

---

# 9. Debugando loops

Loops podem apresentar erros relacionados ao índice, à condição de parada ou aos dados percorridos.

Exemplo:

```js
const nomes = ["Ana", "Carlos", "João"];

for (let i = 0; i <= nomes.length; i++) {
    console.log(nomes[i]);
}
```

Saída:

```txt
Ana
Carlos
João
undefined
```

O erro está na condição:

```js
i <= nomes.length
```

Como arrays começam no índice `0`, o último índice válido é `length - 1`.

Correção:

```js
for (let i = 0; i < nomes.length; i++) {
    console.log(nomes[i]);
}
```

Para debugar loops:

```js
for (let i = 0; i < nomes.length; i++) {
    console.log("Índice:", i);
    console.log("Valor:", nomes[i]);
}
```

---

# 10. Debugando funções

Ao debugar uma função, verifique:

```txt
Quais parâmetros ela recebeu?
O que acontece dentro dela?
Qual valor ela retorna?
```

Exemplo:

```js
function somar(a, b) {
    return a + b;
}

console.log(somar("10", 5));
```

Resultado:

```txt
105
```

O problema ocorre porque `"10"` é uma string.

Debug:

```js
function somar(a, b) {
    console.log("Valor de a:", a, typeof a);
    console.log("Valor de b:", b, typeof b);

    return a + b;
}

console.log(somar("10", 5));
```

---

# 11. Debugando objetos

Objetos podem gerar erros quando uma propriedade esperada não existe.

Exemplo:

```js
const usuario = {
    nome: "Ana",
    endereco: null
};

console.log(usuario.endereco.rua);
```

Esse código gera erro porque `endereco` é `null`.

Correção com verificação:

```js
if (usuario.endereco) {
    console.log(usuario.endereco.rua);
}
```

Correção com optional chaining:

```js
console.log(usuario.endereco?.rua);
```

---

# 12. Debugando arrays

Arrays vazios ou índices inexistentes podem gerar `undefined`.

Exemplo:

```js
const produtos = [];

console.log(produtos[0].nome);
```

Esse código gera erro porque `produtos[0]` é `undefined`.

Correção:

```js
if (produtos.length > 0) {
    console.log(produtos[0].nome);
}
```

Ou:

```js
console.log(produtos[0]?.nome);
```

---

# 13. Debugando código assíncrono

Código assíncrono exige atenção à ordem de execução.

Exemplo:

```js
let usuario;

fetch("https://api.exemplo.com/usuario")
    .then(response => response.json())
    .then(data => {
        usuario = data;
    });

console.log(usuario);
```

O `console.log` provavelmente exibirá:

```txt
undefined
```

Isso acontece porque o `fetch` ainda não terminou quando o `console.log` foi executado.

Forma correta:

```js
fetch("https://api.exemplo.com/usuario")
    .then(response => response.json())
    .then(data => {
        console.log(data);
    });
```

Com `async/await`:

```js
async function buscarUsuario() {
    const response = await fetch("https://api.exemplo.com/usuario");
    const usuario = await response.json();

    console.log(usuario);
}

buscarUsuario();
```

---

# 14. Usando try/catch

O `try/catch` permite tratar erros em operações que podem falhar.

Exemplo:

```js
async function carregarUsuarios() {
    try {
        const response = await fetch("https://api.exemplo.com/usuarios");
        const usuarios = await response.json();

        console.log(usuarios);
    } catch (error) {
        console.error("Erro ao carregar usuários:", error);
    }
}
```

O bloco `catch` captura erros ocorridos dentro do `try`.

---

# 15. Verificando status HTTP

Nem todo erro de API é capturado automaticamente pelo `catch`.

Por isso, é importante verificar a propriedade `ok` da resposta:

```js
if (!response.ok) {
    throw new Error("Erro na requisição: " + response.status);
}
```

Exemplo completo:

```js
async function carregarUsuarios() {
    try {
        const response = await fetch("https://api.exemplo.com/usuarios");

        if (!response.ok) {
            throw new Error("Erro na requisição: " + response.status);
        }

        const usuarios = await response.json();

        console.log(usuarios);
    } catch (error) {
        console.error("Erro ao carregar usuários:", error);
    }
}
```

---

# 16. DevTools do navegador

O DevTools é a ferramenta de desenvolvimento integrada ao navegador.

Para abrir:

```txt
F12
```

Ou:

```txt
Botão direito na página > Inspecionar
```

Principais abas:

```txt
Elements
Console
Sources
Network
Application
```

---

# 17. Aba Console

A aba Console exibe:

```txt
Mensagens do console.log
Erros JavaScript
Avisos
Resultados de comandos executados manualmente
```

Também é possível executar comandos diretamente nela:

```js
document.querySelector("h1");
```

---

# 18. Aba Sources

A aba Sources permite analisar os arquivos JavaScript carregados pela página.

Nela é possível:

```txt
Adicionar breakpoints
Pausar a execução do código
Ver valores de variáveis
Executar o código passo a passo
```

---

# 19. Breakpoints

Breakpoint é um ponto de parada no código.

Quando a execução chega nessa linha, o navegador pausa o JavaScript.

Exemplo:

```js
function calcularTotal(preco, quantidade) {
    const total = preco * quantidade;

    return total;
}

calcularTotal(10, 3);
```

Ao colocar um breakpoint na linha abaixo:

```js
const total = preco * quantidade;
```

É possível verificar os valores de `preco` e `quantidade` antes da conta ser executada.

---

# 20. Palavra-chave debugger

A palavra-chave `debugger` força uma pausa na execução do código quando o DevTools está aberto.

Exemplo:

```js
function calcularTotal(preco, quantidade) {
    debugger;

    const total = preco * quantidade;

    return total;
}

calcularTotal(10, 3);
```

Esse recurso é útil durante a investigação de problemas.

Importante: remova `debugger` antes de finalizar o código.

---

# 21. Execução passo a passo

Ao pausar o código em um breakpoint, é possível executar linha por linha.

Principais comandos:

## Step over

Executa a próxima linha sem entrar dentro de funções chamadas.

## Step into

Entra dentro da função chamada.

## Step out

Sai da função atual e retorna para a função que a chamou.

Exemplo:

```js
function somar(a, b) {
    return a + b;
}

function calcular() {
    const resultado = somar(10, 5);

    console.log(resultado);
}

calcular();
```

Se a execução estiver pausada nesta linha:

```js
const resultado = somar(10, 5);
```

`Step over` executa a função inteira.

`Step into` entra dentro da função `somar`.

---

# 22. Aba Network

A aba Network é usada para analisar requisições HTTP.

Ela mostra:

```txt
URL chamada
Método HTTP
Status da resposta
Tempo da requisição
Headers
Payload enviado
Resposta recebida
```

Essa aba é essencial para debugar integrações com APIs.

---

# 23. Debugando requisições

Exemplo:

```js
async function buscarProdutos() {
    const response = await fetch("https://api.exemplo.com/produtos");
    const produtos = await response.json();

    console.log(produtos);
}
```

Caso a requisição não funcione, verifique na aba Network:

```txt
A requisição foi enviada?
A URL está correta?
O status retornado foi 200, 400, 401, 403, 404 ou 500?
O servidor retornou JSON?
O payload enviado está correto?
```

---

# 24. Status HTTP comuns

## 200

A requisição foi bem-sucedida.

## 400

A requisição foi enviada com dados inválidos.

## 401

O usuário não está autenticado.

## 403

O usuário não possui permissão.

## 404

A rota ou recurso não foi encontrado.

## 500

Ocorreu um erro interno no servidor.

---

# 25. Debugando eventos

Eventos podem falhar quando o elemento não foi encontrado ou quando o script é executado antes do HTML estar carregado.

Exemplo:

```js
const botao = document.querySelector("#botao");

botao.addEventListener("click", function () {
    console.log("Botão clicado");
});
```

Para verificar se o elemento foi encontrado:

```js
console.log(botao);
```

Se o resultado for `null`, o elemento não existe no momento em que o JavaScript foi executado.

Solução comum:

```js
document.addEventListener("DOMContentLoaded", function () {
    const botao = document.querySelector("#botao");

    botao.addEventListener("click", function () {
        console.log("Botão clicado");
    });
});
```

---

# 26. Debugando this

O valor de `this` depende de como a função é chamada.

Exemplo:

```js
const usuario = {
    nome: "Ana",
    apresentar() {
        console.log(this.nome);
    }
};

const fn = usuario.apresentar;

fn();
```

Nesse caso, o resultado pode ser `undefined`, pois a função foi separada do objeto original.

Correção com `bind`:

```js
const fn = usuario.apresentar.bind(usuario);

fn();
```

---

# 27. Debugando escopo

Escopo define onde uma variável pode ser acessada.

Exemplo:

```js
function executar() {
    const nome = "Ana";
}

console.log(nome);
```

Esse código gera erro, pois `nome` existe apenas dentro da função `executar`.

Ao debugar problemas de escopo, verifique onde a variável foi declarada e onde está sendo utilizada.

---

# 28. Debugando tipos

Muitos erros acontecem por causa de tipos inesperados.

Exemplo:

```js
const valor = "10";

console.log(valor + 5);
```

Resultado:

```txt
105
```

Isso acontece porque `valor` é uma string.

Para verificar o tipo:

```js
console.log(typeof valor);
```

Correção:

```js
const valor = Number("10");

console.log(valor + 5);
```

Resultado:

```txt
15
```

---

# 29. Debugando NaN

`NaN` significa `Not a Number`.

Exemplo:

```js
const total = Number("abc") * 10;

console.log(total);
```

Resultado:

```txt
NaN
```

Correção com validação:

```js
const valor = Number("abc");

if (Number.isNaN(valor)) {
    console.log("Valor inválido");
}
```

---

# 30. Debugando undefined

`undefined` geralmente indica que uma variável ou propriedade não recebeu valor.

Exemplo:

```js
function exibirNome(nome) {
    console.log(nome);
}

exibirNome();
```

Resultado:

```txt
undefined
```

Correção com valor padrão:

```js
function exibirNome(nome = "Sem nome") {
    console.log(nome);
}
```

---

# 31. Debugando null

`null` representa ausência intencional de valor.

Exemplo:

```js
const usuario = null;

console.log(usuario.nome);
```

Esse código gera erro.

Correção:

```js
if (usuario !== null) {
    console.log(usuario.nome);
}
```

Ou:

```js
console.log(usuario?.nome);
```

---

# 32. Truthy e falsy

Alguns valores são tratados como falsos em condições.

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
const ativo = "false";

if (ativo) {
    console.log("Está ativo");
}
```

Mesmo contendo o texto `"false"`, a string é considerada truthy porque possui conteúdo.

---

# 33. Checklist de debug

Quando encontrar um problema, siga esta ordem:

```txt
1. Leia a mensagem de erro com atenção.
2. Verifique o arquivo e a linha indicados.
3. Confirme os valores das variáveis.
4. Verifique os tipos com typeof.
5. Teste condições separadamente.
6. Confira se arrays e objetos possuem os dados esperados.
7. Verifique se as funções recebem os parâmetros corretos.
8. Em código assíncrono, confira se faltou await.
9. Em requisições, analise a aba Network.
10. Corrija uma coisa por vez.
```

---

# 34. Erros comuns em JavaScript

## Cannot read properties of undefined

Ocorre ao tentar acessar uma propriedade de algo que é `undefined`.

```js
const usuario = undefined;

console.log(usuario.nome);
```

---

## Cannot read properties of null

Ocorre ao tentar acessar uma propriedade de algo que é `null`.

```js
const usuario = null;

console.log(usuario.nome);
```

---

## is not defined

Ocorre quando uma variável não existe no escopo atual.

```js
console.log(nome);
```

---

## is not a function

Ocorre quando algo que não é função é chamado como função.

```js
const nome = "Ana";

nome();
```

---

## Unexpected token

Geralmente indica erro de sintaxe.

```js
if (true {
    console.log("Teste");
}
```

---

# 35. Erro de sintaxe e erro de lógica

## Erro de sintaxe

O JavaScript não consegue interpretar o código.

```js
const nome = "Ana
```

## Erro de lógica

O código executa, mas produz um resultado incorreto.

```js
const media = 5 + 7 / 2;

console.log(media);
```

Se a intenção era calcular a média entre 5 e 7, o correto seria:

```js
const media = (5 + 7) / 2;
```

---

# 36. Debug em pequenos blocos

Evite escrever muitas linhas de código antes de testar.

O ideal é validar pequenas partes durante o desenvolvimento.

Exemplo de processo:

```txt
Criar a função.
Testar a função.
Criar a condição.
Testar a condição.
Criar o loop.
Testar o loop.
Integrar as partes.
Testar novamente.
```

Esse processo facilita encontrar problemas antes que o código fique grande demais.

---

# 37. Exemplo completo

Código com erro:

```js
const produtos = [
    { nome: "Mouse", preco: "50" },
    { nome: "Teclado", preco: "100" },
    { nome: "Monitor", preco: "900" }
];

function calcularTotal(produtos) {
    let total = 0;

    for (let i = 0; i <= produtos.length; i++) {
        total += produtos[i].preco;
    }

    return total;
}

console.log(calcularTotal(produtos));
```

Problemas encontrados:

```txt
1. O loop usa <= em vez de <.
2. Os preços estão como string.
3. Na última execução, produtos[i] será undefined.
```

Versão com logs de debug:

```js
function calcularTotal(produtos) {
    let total = 0;

    for (let i = 0; i < produtos.length; i++) {
        console.log("Índice:", i);
        console.log("Produto:", produtos[i]);
        console.log("Preço:", produtos[i].preco, typeof produtos[i].preco);

        total += Number(produtos[i].preco);

        console.log("Total parcial:", total);
    }

    return total;
}
```

Versão corrigida:

```js
const produtos = [
    { nome: "Mouse", preco: 50 },
    { nome: "Teclado", preco: 100 },
    { nome: "Monitor", preco: 900 }
];

function calcularTotal(produtos) {
    let total = 0;

    for (let i = 0; i < produtos.length; i++) {
        total += produtos[i].preco;
    }

    return total;
}

console.log(calcularTotal(produtos));
```

---

# 38. Como pedir ajuda com um erro

Ao pedir ajuda, evite mensagens genéricas como:

```txt
Não funciona.
```

O ideal é informar:

```txt
O que eu esperava que acontecesse.
O que realmente aconteceu.
Qual erro apareceu.
Qual trecho de código está envolvido.
O que eu já tentei.
```

Exemplo:

```txt
Eu queria somar os preços dos produtos, mas o resultado está sendo concatenado como texto.
Era esperado retornar 150, mas está retornando 050100.
Percebi que os preços estão vindo como string.
Tentei usar Number(), mas ainda estou em dúvida sobre onde realizar essa conversão.
```

---

# 39. Boas práticas durante o debug

## Altere uma coisa por vez

Evite mudar várias partes do código ao mesmo tempo.

Isso facilita identificar qual alteração resolveu ou causou o problema.

---

## Leia a mensagem de erro completa

A mensagem de erro geralmente informa:

```txt
Tipo do erro
Arquivo
Linha
Possível causa
```

---

## Confirme os dados antes de assumir

Sempre verifique valores importantes antes de concluir que eles estão corretos.

Exemplo:

```js
console.log("Usuário recebido:", usuario);
```

---

## Remova logs temporários

Logs usados apenas durante o debug devem ser removidos antes de finalizar o código.

Exemplo de logs temporários:

```js
console.log("teste");
console.log("chegou aqui");
console.log("valor:", valor);
```

---

# 40. Exercícios práticos

## Exercício 1

O código abaixo deveria mostrar `"Maior de idade"`, mas não mostra.

Identifique o problema e corrija.

```js
const idade = "18";

if (idade === 18) {
    console.log("Maior de idade");
} else {
    console.log("Menor de idade");
}
```

---

## Exercício 2

O código abaixo imprime `undefined`.

Identifique o motivo e corrija.

```js
const nomes = ["Ana", "Carlos", "João"];

for (let i = 0; i <= nomes.length; i++) {
    console.log(nomes[i]);
}
```

---

## Exercício 3

O código abaixo deveria somar os preços, mas o resultado está incorreto.

Debugue e corrija.

```js
const produtos = [
    { nome: "Mouse", preco: "50" },
    { nome: "Teclado", preco: "100" }
];

let total = 0;

for (const produto of produtos) {
    total += produto.preco;
}

console.log(total);
```

---

## Exercício 4

O código abaixo gera erro.

Identifique o motivo e corrija.

```js
const usuario = {
    nome: "Ana",
    endereco: null
};

console.log(usuario.endereco.rua);
```

---

## Exercício 5

O código abaixo imprime `undefined`.

Explique o motivo.

```js
let usuario;

setTimeout(function () {
    usuario = {
        nome: "Carlos"
    };
}, 1000);

console.log(usuario);
```

---

# 41. Desafio final

Analise o código abaixo, encontre os problemas e corrija.

```js
const alunos = [
    { nome: "Ana", nota1: "8", nota2: "7" },
    { nome: "Carlos", nota1: "5", nota2: "6" },
    { nome: "João", nota1: "9", nota2: "10" }
];

function calcularMedia(aluno) {
    return aluno.nota1 + aluno.nota2 / 2;
}

for (let i = 0; i <= alunos.length; i++) {
    const media = calcularMedia(alunos[i]);

    if (media >= 7) {
        console.log(alunos[i].nome + " aprovado");
    } else {
        console.log(alunos[i].nome + " reprovado");
    }
}
```

Pistas:

```txt
Verifique o limite do loop.
Verifique os tipos das notas.
Verifique a ordem da conta.
Verifique se alunos[i] sempre existe.
```

---

# 42. Conclusão

Debug é uma habilidade essencial no desenvolvimento de software.

Saber debugar significa entender como o código está sendo executado, analisar valores, identificar a origem do problema e corrigir o comportamento de forma consciente.

Um bom processo de debug evita alterações aleatórias e melhora a qualidade do código.

Com prática, o desenvolvedor passa a identificar erros com mais rapidez, compreender melhor o funcionamento do programa e escrever soluções mais seguras.

```
