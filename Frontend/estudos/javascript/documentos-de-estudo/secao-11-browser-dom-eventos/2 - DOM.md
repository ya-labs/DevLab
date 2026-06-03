# DOM

DOM significa Document Object Model.

Ele é a representação em objetos da página HTML dentro do navegador. Com o DOM, o JavaScript consegue ler, alterar, criar e remover elementos da página enquanto ela está sendo usada.

---

# 1 - O que é o DOM

Quando o navegador carrega um HTML, ele transforma esse documento em uma árvore de objetos.

Exemplo de HTML:

```html
<h1 id="titulo">Olá</h1>
<button id="botao">Trocar título</button>
```

O navegador cria objetos que representam esses elementos.

O JavaScript não altera diretamente o arquivo HTML original. Ele altera os objetos que representam a página atual.

---

# 2 - Por que o DOM existe

O DOM existe para permitir que linguagens como JavaScript interajam com o documento carregado.

Com ele, podemos:

- alterar textos;
- trocar classes CSS;
- criar elementos;
- remover elementos;
- reagir a cliques;
- ler valores de inputs;
- montar listas dinamicamente;
- atualizar parte da tela sem recarregar a página.

Sem DOM, a página seria muito mais estática.

---

# 3 - document

`document` é o objeto principal usado para acessar a página.

```js
const titulo = document.getElementById("titulo");

console.log(titulo.textContent);
```

`document` é fornecido pelo navegador.

Ele não faz parte do JavaScript puro da linguagem. Ele é uma API do ambiente web.

---

# 4 - Buscando elementos

Formas comuns:

```js
const titulo = document.getElementById("titulo");
const botao = document.querySelector("#botao");
const itens = document.querySelectorAll(".item");
```

Na prática, `querySelector` e `querySelectorAll` são muito usados porque aceitam seletores CSS.

```js
const primeiroCard = document.querySelector(".card");
```

`querySelector` retorna o primeiro elemento encontrado.

`querySelectorAll` retorna uma lista de elementos.

---

# 5 - Alterando texto e HTML

Para alterar texto, prefira `textContent`.

```js
const titulo = document.querySelector("#titulo");

titulo.textContent = "Título alterado";
```

Para inserir HTML, existe `innerHTML`.

```js
const conteudo = document.querySelector("#conteudo");

conteudo.innerHTML = "<strong>Mensagem</strong>";
```

Use `innerHTML` com cuidado. Se o conteúdo vier do usuário, pode abrir risco de XSS.

---

# 6 - Alterando classes e estilos

Para classes:

```js
const menu = document.querySelector("#menu");

menu.classList.add("aberto");
menu.classList.remove("fechado");
menu.classList.toggle("ativo");
```

Para estilo direto:

```js
menu.style.display = "block";
```

Em projetos reais, geralmente é melhor alternar classes CSS do que espalhar muitos estilos inline no JavaScript.

---

# 7 - Eventos

Eventos permitem reagir a ações do usuário.

```js
const botao = document.querySelector("#botao");
const titulo = document.querySelector("#titulo");

botao.addEventListener("click", function() {
    titulo.textContent = "Título alterado";
});
```

Nesse exemplo:

- o JavaScript busca o botão;
- registra um evento de clique;
- quando o usuário clica, a função callback executa;
- o texto do título é alterado.

---

# 8 - Criando elementos

```js
const lista = document.querySelector("#lista");

const item = document.createElement("li");
item.textContent = "Novo item";

lista.appendChild(item);
```

Isso é útil para montar elementos dinamicamente.

Em aplicações modernas com React, o DOM normalmente é manipulado pelo framework. Mesmo assim, entender DOM ajuda a compreender o que está acontecendo por baixo.

---

# 9 - DOM não é a tela

DOM é a estrutura de objetos.

A tela é o resultado visual renderizado pelo navegador.

Quando o DOM muda, o navegador pode precisar:

- recalcular layout;
- redesenhar partes da tela;
- repintar elementos.

Por isso, muitas alterações repetidas no DOM podem afetar performance.

---

# 10 - Exemplo prático completo

```html
<input id="nome" placeholder="Digite seu nome">
<button id="adicionar">Adicionar</button>
<ul id="lista"></ul>
```

```js
const inputNome = document.querySelector("#nome");
const botaoAdicionar = document.querySelector("#adicionar");
const lista = document.querySelector("#lista");

botaoAdicionar.addEventListener("click", function() {
    const nome = inputNome.value.trim();

    if (nome === "") {
        return;
    }

    const item = document.createElement("li");
    item.textContent = nome;

    lista.appendChild(item);
    inputNome.value = "";
});
```

Esse exemplo mostra:

- leitura de input;
- validação simples;
- criação de elemento;
- atualização da tela;
- evento de clique.

---

# 11 - Erros comuns

### Buscar elemento antes dele existir

Se o script roda antes do HTML ser carregado, o elemento pode vir como `null`.

Uma solução simples é colocar o script no final do `body` ou usar `type="module"` com atenção ao carregamento.

### Usar innerHTML com dados externos

```js
conteudo.innerHTML = comentarioUsuario;
```

Se o conteúdo não for confiável, isso pode gerar falha de segurança.

Prefira `textContent` para texto.

### Manipular DOM demais em loop

Muitas alterações repetidas podem causar custo visual.

Para listas grandes, monte os elementos com cuidado e evite trabalho desnecessário.

---

# 12 - Relação com outros estudos

DOM se conecta com motor JavaScript, eventos, funções, arrays, objetos e browser APIs.

Antes de estudar eventos com profundidade, vale dominar busca de elementos, alteração de texto, classes e criação de elementos.

---

# 13 - Conclusão

DOM é a ponte entre JavaScript e a página carregada no navegador.

Entender DOM ajuda a saber como páginas ficam interativas, como eventos mudam a tela e por que frameworks modernos ainda dependem, por baixo, de atualizações nessa estrutura.
