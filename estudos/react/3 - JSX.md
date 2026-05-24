    ```js
O que é e por que o React usa JSX

----------------------------------------------------------------------

problema que o JSX resolve:

no AngularJS:

HTML → separado
JS → separado
lógica → conectada via diretivas (ng-click, ng-if, etc.)

existe uma separação forte entre template e lógica.

no React, a ideia é diferente:
a interface é tratada como parte da lógica

----------------------------------------------------------------------

o que é o JSX de verdade
é uma sintaxe que permite escrever estrutura de interface dentro do JavaScript
exemplo:
return <button>Iniciar Treino</button>;
parece HTML, mas é convertido para JavaScript por baixo

esse código <button>Iniciar treino</button>
vira algo como React.createElement('button', null, 'Iniciar treino');

----------------------------------------------------------------------

Porque o React usa isso:
1 - unir lógica + interface

em vez de separar HTML em um lugar, JS no outro
é escrito tudo junto: return isLogged ? <Dashboard/> : <Login/>;

Isso simplifica muito a lógica de renderização.

2 - poder usar JS direto na interface
exemplo:
const nome = "Nícolas";
return <h1>Olá, {nome}</h1>;

3 - controle total via estado
no React, a UI depende de estado

JSX facilita escrever:
return isLoading ? <Loading /> : <Content />;

