  ```js
Escrevendo e entendendo o código básico

_________________________________________________

function App() {
  return <button>Iniciar treino</button>;
}

export default App;

_________________________________________________

- > return <button>Iniciar treino</button>;

o return define o que a função vai devolver

só que aqui ela não devolve número nem texto simples
ela devolve um botão

_________________________________________________

⚠️ detalhe importante

isso aqui:

<button>Iniciar treino</button>

isso se chama JSX 
é uma forma de escrever interface dentro do JavaScript

_________________________________________________

export default App;

essa linha permite que o React use esse componente

basicamente você está dizendo:
“esse componente aqui pode ser usado no app”
