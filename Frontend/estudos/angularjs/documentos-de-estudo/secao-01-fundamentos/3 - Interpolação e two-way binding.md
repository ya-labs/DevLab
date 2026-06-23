# 3 - Interpolação e two-way binding

Interpolação é uma forma de exibir valores do JavaScript dentro do HTML.

Two-way binding é a sincronização em duas direções entre view e modelo.

---

## 1. O que é interpolação

Interpolação é o uso de `{{ }}` para mostrar dados na tela.

Exemplo:

```html
<p>Olá, {{ nome }}</p>
```

Se `nome` for `Ana`, a tela mostra:

```txt
Olá, Ana
```

---

## 2. Por que interpolação existe

Ela existe para permitir que a view mostre dados dinâmicos sem manipular o DOM na mão.

Isso deixa o HTML mais declarativo e o código mais previsível.

---

## 3. Exemplo completo

```html
<div ng-app="app" ng-controller="MainCtrl">
	<p>Nome: {{ nome }}</p>
	<p>Idade: {{ idade }}</p>
</div>
```

```js
const app = angular.module("app", []);

app.controller("MainCtrl", function($scope) {
	$scope.nome = "Nicolas";
	$scope.idade = 20;
});
```

---

## 4. O que é two-way binding

Two-way binding significa que a alteração pode acontecer nos dois lados:

- da view para o JavaScript;
- do JavaScript para a view.

Exemplo:

```html
<div ng-app="app" ng-controller="MainCtrl">
	<input ng-model="nome" />
	<p>{{ nome }}</p>
</div>
```

```js
const app = angular.module("app", []);

app.controller("MainCtrl", function($scope) {
	$scope.nome = "";
});
```

## 5. Diferença entre {{ }} e ng-model

### Interpolação

- exibe valores no HTML;
- é leitura da view;
- não recebe entrada do usuário.

### ng-model

- liga um input à uma variável;
- permite leitura e escrita;
- participa do two-way binding.

Resumo simples:

- `{{ nome }}` mostra;
- `ng-model="nome"` conecta e sincroniza.

---

## 6. Quando isso atualiza a tela

Se a mudança acontece dentro do fluxo do AngularJS, a tela atualiza automaticamente.

Exemplos:

- `ng-click`;
- `ng-model`;
- `$http`;
- `$timeout`.

Quando a mudança acontece fora do AngularJS, pode ser necessário avisar o framework.

Esse assunto se conecta com o digest cycle, que vem depois na trilha.

---

## 7. Exemplo com interação real

```html
<div ng-app="app" ng-controller="MainCtrl">
	<input ng-model="nome" placeholder="Digite seu nome" />
	<p>Bem-vindo, {{ nome }}!</p>
</div>
```

```js
const app = angular.module("app", []);

app.controller("MainCtrl", function($scope) {
	$scope.nome = "";
});
```

Aqui:

- o input altera o modelo;
- a interpolação mostra o valor imediatamente;
- o usuário vê a mudança sem recarregar a página.

---

## 8. Erros comuns

### Confundir interpolação com input

`{{ }}` não captura valor digitado.

### Usar ng-model sem necessidade

Se o valor só precisa ser exibido, interpolação basta.

### Esperar atualização fora do Angular sem entender o ciclo

Isso gera tela que parece "presa".

---

## 9. Boas práticas

- usar interpolação para exibição;
- usar `ng-model` para formulários e entrada de dados;
- manter nomes claros de variáveis no scope;
- evitar lógica complexa dentro da view;
- lembrar que binding depende do ciclo do AngularJS.

---

## 10. Relação com outros conteúdos

Esse tema se conecta com:

- Controllers e $scope em Frontend/estudos/angularjs/documentos-de-estudo/secao-01-fundamentos/2 - Controllers e $scope.md;
- Digest cycle em Frontend/estudos/angularjs/documentos-de-estudo/secao-03-scope-digest-ciclo-vida/2 - Digest cycle e watchers.md;
- Forms em Frontend/estudos/angularjs/documentos-de-estudo/secao-07-forms-validacao/1 - Forms no AngularJS.md.

---

## Conclusão

Interpolação mostra dados e two-way binding sincroniza dados.

Os dois conceitos são a base da sensação de reatividade no AngularJS.
