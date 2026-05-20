# 1 - O que são eventos em JavaScript?

Eventos são acontecimentos que ocorrem dentro da aplicação e que o JavaScript pode detectar para executar alguma ação.
Por exemplo, a página tem elementos visuais:
- botão
- input
- formulário
- links
- imagens
- a própria janela do navegador

Sozinhos, eles não fazem nada além do comportamento padrão.

O JavaScript entra justamente para dizer:
- "Quando X acontecer, execute Y".

Exemplo:
- quando clicar no botão -> mostrar mensagem
- quando digitarem no input -> validar texto
- quando enviar o formulário -> processar dados
- quando apertarem Enter -> executar busca

Eventos tornam a interface interativa.

## Como isso funciona conceitualmente?

Imagine um restaurante.
Você não fica indo na cozinha a cada 2 segundos perguntando:
"Meu pedido ficou pronto?"
"Agora?"
"E agora?"

Você simplesmente espera ser chamado

Quando chamam:
algo aconteceu.

Seu cérebro reage,
Javascript funciona da mesma forma.

Em vez de ficar verificando continuamente se algo aconteceu, você registra interesse
naquele acontecimento.

A parte de avisar o JavaScript que algo aconteceu é o listener (ou ouvinte).

---

# 2 - Exemplo prático

HTML:

```html
<button id="meuBotao">Clique aqui</button>
```

JavaScript:

```js
const botao = document.getElementById('meuBotao');

botao.addEventListener('click', function() {
    alert('Botão clicado!');
});
```

## 1 - Selecionamos o elemento do botão usando `getElementById`.
```js
const botao = document.getElementById('meuBotao');
```
Aqui você pega o elemento do DOM.

Esse botão deixa de ser "só HTML" e vira um objeto manipulável pelo JavaScript.

Algo conceitualmente parecido com:

```js
{
    tagName: "BUTTON",
    id: "meuBotao",
    textContent: "Clique aqui",
}
```

## 2 - Registramos um evento de clique usando `addEventListener`.
```js
botao.addEventListener('click', function() {...});
```
literalmente adicionar um ouvinte.
O primeiro argumento é o tipo do evento, nesse caso "click".
O segundo argumento é a função que será executada quando o evento ocorrer.

## 3 - Tipo do evento
string que representa a ação que queremos ouvir.
```js
"click" 
```
-> quero ouvir eventos de clique.

Outros exemplos:
```js
"input"
"change"
"submit"
"keydown"
"mouseover"
```

## 4 - Função de callback
```js
function () {
    alert('Botão clicado!');
}
```
Essa função será executada quando o evento acontecer.

---

# 3 - O que acontece por trás?

Quando você escreve
```js
botao.addEventListener('click', minhaFuncao);
```
O navegador registra internamente algo parecido como:
```js
botao = {
    listeners: {
        click: [minhaFuncao]
    }
}
```
(Não é literalmente assim)

Quando o usuário clica:
1 - Sistema operacional detecta clique
2 - Navegador recebe evento
3 - Identifica qual elemento foi clicado
4 - Cria objeto representando o evento
5 - Executa funções registradas

Fluxo: 
`Usuário -> navegador -> evento -> JavaScript`

---

# 4 - O objeto `Event`

Quando um evento acontece, o navegador cria um objeto contendo informações sobre ele.
Esse objeto é passado automaticamente para a função de callback.

Exemplo:
```js
botao.addEventListener('click', function(event) {
    console.log(event);
});
```
Ao clicar, é possível visualizar algo como:
```js
PointerEvent
```
Esse objeto possui várias informações.

Exemplo conceitual:
```js
{
    type: "click",
    target: <button id="meuBotao">Clique aqui</button>,
    timestamp: 12345678,
    clientX: 150,
    clientY: 200,
}
```

## 1 - Target 

Uma das propriedades mais importantes:
```js
event.target
```
Significa:
<strong style="font-weight: bold;">quem disparou o evento.</strong>
Exemplo:
```js
botao.addEventListener('click', function(event) {
    console.log(event.target); 
});
```
Resultado:
```html
<button id="meuBotao">Clique aqui</button>
```

### Por que isso importa?

Permite código mais reutilizável.
Exemplo:
```js
document.addEventListener('click', function(event) {
    console.log(event.target); 
});
```
Agora qualquer clique na página mostra qual elemento foi clicado.
Muito usado em delegação de eventos.

---

# 5 - Vários listeners

Você pode registrar múltiplos listeners para o mesmo evento.

```js
botao.addEventListener('click', function() {
    console.log('Primeiro listener');
});
botao.addEventListener('click', function() {
    console.log('Segundo listener');
});
```
Ao clicar, ambos serão executados:
```js
"Primeiro listener"
"Segundo listener"
```

## onclick vs addEventListener
Forma antiga:
```js
botao.onclick = function() {
    console.log('Clique!');
};
```
problema:
```js
botao.onclick = function() {
    console.log('Outro clique!');
};
botao.onclick = function() {
    console.log('Mais um outro clique!');
};
```
Nesse caso, apenas o último listener é mantido.
```js
"Mais um outro clique!"
```
---
# 6 - Eventos comuns
## 1 - click
```js
element.addEventListener('click', function() {...});
```
## 2 - keydown
```js
element.addEventListener('keydown', function(event) {
    console.log(event.key); // qual tecla foi pressionada
});
```
## 3 - input
```js
inputElement.addEventListener('input', function(event) {
    console.log(event.target.value); // valor atual do input
});
```
## 4 - change
```js
selectElement.addEventListener('change', function(event) {
    console.log(event.target.value); // valor selecionado
});
```
## 5 - submit
```js
formElement.addEventListener('submit', function(event) {
    event.preventDefault(); // evitar envio padrão
    console.log('Formulário enviado!');
});
```
## 6 - focus
```js
inputElement.addEventListener('focus', function() {
    console.log('Input focado!');
});
```
## 7 - blur
```js
inputElement.addEventListener('blur', function() {
    console.log('Input perdeu foco!');
});
```
## 8 - mouseover
```js
element.addEventListener('mouseover', function() {
    console.log('Mouse sobre o elemento!');
});
```
## 9 - mouseout
```js
element.addEventListener('mouseout', function() {
    console.log('Mouse saiu do elemento!');
});
```

## 10 - scroll
```js
window.addEventListener('scroll', function() {
    console.log('A página foi rolada!');
});
```

---

# 7 - preventDefault()
Alguns eventos possuem um comportamento padrão.

Exemplo:
Formulário.

Html:
```html
<form id="meuForm">
    <input type="text" name="nome" />
    <button type="submit">Enviar</button>
</form>
```

Ao enviar:
- página recarrega

Porque esse é o comportamento padrão.

Para impedir:
```js
formElement.addEventListener('submit', function(event) {
    event.preventDefault(); // impede comportamento padrão
    console.log('Formulário enviado!');
});
```
A função previne o comportamento padrão de acontecer.

# 8 - Eventos se propagam
Exemplo:

```html
<div id="pai">
    <button id="filho">Clique aqui</button>
</div>
```

JavaScript:
```js
div.addEventListener('click', function() {
    console.log('Div clicada!');
});

button.addEventListener('click', function() {
    console.log('Botão clicado!');
});
```

Clicando no botão:
```js
"Botão clicado!"
"Div clicada!"
```
Porque eventos sobem pela árvore DOM.

Isso se chama:
`Event Bubbling`

Fluxo:
`button -> div -> body -> html -> document`

O evento nasce no elemento clicado e sobe.

# 9 - stopPropagation()
Se quiser impedir que o evento suba:
```js
button.addEventListener('click', function(event) {
    event.stopPropagation(); // impede propagação
    console.log('Botão clicado!');
});
```
Agora, clicando no botão:
```js
"Botão clicado!"
```

---

# 10 - Event Capturing
Caminho inverso do bubbling.
Antes do evento chegar no alvo, ele pode descer pela árvore DOM.

Fluxo:
`document -> html -> body -> div -> button`

Ou seja:
Primeiro desce, depois sobe.
Normalmente usamos bubbling.

Mas dá pra ativar capturing:
```js
button.addEventListener('click', function() {
    console.log('Botão clicado!');
}, true); // true(terceiro argumento) ativa capturing
```
Fluxo real:
```
capturing ↓
target 🎯
bubbling ↑
```

---

# 11 - Event Delegation
Uma técnica muito usada.

Em vez de colocar evento em vários elementos...

Ruim:
```js   
todosBotoes.forEach(btn => {
    btn.addEventListener('click', fn);
});
```
Você usa bubbling a seu favor.

É possível colocar o evento no elemento pai e verifica o target.
```js
container.addEventListener('click', function(event) {
    if (event.target.matches('.btn')) {
        console.log("clicou no botão")
    }
});
```
Agora qualquer botão dentro funciona.

Vantagens:
- Menos memória
- Menos listeners
- Funciona com elementos criados dinamicamente
- Padrão real de mercado

---

# 12 - Eventos e [Event Loop](1%20-%20Motor%20JavaScript.md#7---entenda-o-event-loop-para-evitar-bugs) 

Clique:
```js
button.addEventListener('click', fn);
```

Quando usuário clica:
- navegador detecta
- callback vai pra fila
- event loop espera stack livre (sem código rodando)
- executa callback
Por isso parecem "assíncronos".

Eles fazem parte das MacroTasks.
