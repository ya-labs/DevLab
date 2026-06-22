# 1 - O que é AngularJS 1.x

AngularJS 1.x é um framework JavaScript criado para construir interfaces web dinâmicas.

Ele surgiu para resolver um problema comum da época: páginas com muito HTML estático e JavaScript espalhado, difícil de manter.

Com AngularJS 1.x, você consegue:

- conectar dados do JavaScript com a tela;
- reagir a eventos de usuário;
- separar responsabilidades com controller, service e directive;
- organizar aplicações maiores sem cair em scripts soltos.

---

## 1. O que significa 1.x

Quando falamos AngularJS 1.x, estamos falando da família de versões 1.0 até 1.8.

Exemplos:

- 1.2.x;
- 1.5.x;
- 1.7.x;
- 1.8.x.

O ponto importante: AngularJS 1.x não é o mesmo framework que Angular moderno (Angular 2+).

---

## 2. Por que AngularJS existiu

Antes de frameworks populares, era comum fazer assim:

- buscar elemento no DOM manualmente;
- atualizar texto no HTML na mão;
- lidar com eventos sem padrão;
- misturar regra de negócio com manipulação de tela.

AngularJS trouxe uma abordagem mais estruturada:

- declaração no HTML com diretivas;
- data binding;
- injeção de dependência;
- modularização da aplicação.

---

## 3. Conceitos centrais

### Módulo

É o container principal da aplicação.

```js
const app = angular.module("app", []);
```

### Controller

Liga a view com a lógica da tela.

```js
app.controller("MainCtrl", function($scope) {
    $scope.titulo = "Painel";
});
```

### Scope

Contexto que conecta dados entre controller e view.

### Service

Camada para lógica reutilizável e integração com dados.

### Directive

Extensão de comportamento no HTML.

---

## 4. Como funciona na prática

Exemplo mínimo:

```html
<!DOCTYPE html>
<html ng-app="app">
<head>
    <meta charset="UTF-8" />
    <title>Exemplo AngularJS</title>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.8.2/angular.min.js"></script>
</head>
<body ng-controller="MainCtrl">
    <input ng-model="nome" placeholder="Digite seu nome" />
    <p>Olá, {{ nome }}.</p>

    <script>
        const app = angular.module("app", []);

        app.controller("MainCtrl", function($scope) {
            $scope.nome = "";
        });
    </script>
</body>
</html>
```

O que acontece:

- ng-app inicia o módulo;
- ng-controller instancia o controller;
- ng-model conecta input com variável;
- {{ nome }} exibe o valor da variável;
- quando o usuário digita, a tela atualiza automaticamente.

---

## 5. Onde AngularJS ainda aparece

Mesmo sendo tecnologia legada, ele ainda aparece em:

- sistemas internos antigos;
- projetos corporativos com ciclo longo;
- apps híbridos com Cordova;
- produtos sem time dedicado para migração imediata.

---

## 6. Erros comuns de quem está iniciando

### Confundir AngularJS com Angular moderno

São frameworks diferentes.

### Colocar regra de negócio pesada no controller

Controller deve ficar focado em comportamento de tela.

### Usar rootScope para tudo

Isso aumenta acoplamento e dificulta manutenção.

### Ignorar digest cycle

Sem entender digest e watchers, fica difícil debugar tela que não atualiza.

---

## 7. Boas práticas desde o início

- preferir service para regras reutilizáveis;
- manter controller pequeno e objetivo;
- nomear módulos e arquivos com padrão;
- evitar manipulação direta de DOM no controller;
- estudar bem scope, digest e performance.

---

## 8. Relação com a trilha de JavaScript

Antes de aprofundar AngularJS, vale revisar:

- Promises e async em Frontend/estudos/javascript/documentos-de-estudo/secao-08-assincronismo/1 - Promises e async.md;
- DOM em Frontend/estudos/javascript/documentos-de-estudo/secao-11-browser-dom-eventos/2 - DOM.md;
- Eventos em Frontend/estudos/javascript/documentos-de-estudo/secao-11-browser-dom-eventos/3 - Eventos.md;
- Fetch API em Frontend/estudos/javascript/documentos-de-estudo/secao-12-http-integracao/1 - Fetch API.md.

Esses assuntos sustentam boa parte do uso real em AngularJS.

---

## Conclusão

AngularJS 1.x foi uma tecnologia muito importante na evolução do frontend.

Hoje ele deve ser estudado com foco em manutenção de legado, entendimento de arquitetura antiga e transição para soluções modernas sem quebrar sistemas em produção.
