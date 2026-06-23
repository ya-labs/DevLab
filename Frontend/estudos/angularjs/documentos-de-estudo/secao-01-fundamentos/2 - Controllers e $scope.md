# 2 - Controllers e $scope

Controller é o ponto onde a lógica da tela fica organizada.

O `$scope` é o contexto que liga essa lógica com a view.

---

## 1. O que é um controller

Um controller é uma função usada para controlar o comportamento de uma parte da interface.

Exemplo:

```js
app.controller("MainCtrl", function($scope) {
	$scope.nome = "";
});
```

Ele é responsável por:

- preparar dados para a tela;
- expor funções para eventos;
- coordenar a interação entre view e service;
- manter a lógica da tela em um lugar previsível.

---

## 2. O que é o #scope

O `$scope` é o objeto onde o controller coloca dados e funções que a view pode acessar.

Exemplo:

```js
app.controller("MainCtrl", function($scope) {
	$scope.titulo =  "Painel";
	$scope.salvar = function() {
		console.log("Salvo");
	};
});
```

Na view:

```html
<div ng-controller="MainCtrl">
	<h1>{{ titulo }}</h1>
	<button ng-click="salvar()">Salvar</button>
</div>
```

---

## 3. Por que esse padrão existe

Ele existe para separar a lógica da interface do HTML puro.

Sem controller e scope, a tela ficaria cheia de JavaScript solto e difícil de manter.

---

## 4. Fluxo da interação

1. o Angular instancia o controller;
2. ele injeta o `$scope`;
3. o controller adiciona dados e funções;
4. a view acessa esses valores;
5. a interface reage a mudanças.

---

## 5. Exemplo prático

```html
<div ng-app="app" ng-controller="UsuarioCtrl">
	<input ng-model="nome" placeholder="Digite seu nome" />
	<button ng-click="saudar()">Saudar</button>
	<p>{{ mensagem }}</p>
</div>
```

```js
const app = angular.module("app", []);

app.controller("UsuarioCtrl", function($scope) {
	$scope.nome = "";
	$scope.mensagem = "";

	$scope.saudar = function() {
		$scope.mensagem = "Ola, " + $scope.nome;
	};
});
```

O que acontece:

- `ng-model` atualiza `$scope.nome`;
- `ng-click` chama a função do controller;
- a mensagem muda no `$scope`;
- a view reflete a mudança.

---

## 6. O que o controller não deve fazer

Controller não deve virar depósito de regra de negócio complexa.

Evite:

- requisições HTTP diretas espalhadas sem necessidade;
- lógica reutilizável duplicada;
- manipulação extensa de dados que deveria estar em service.

O ideal é deixar controller pequeno e objetivo.

---

## 7. $scope x dados locais

Variáveis declaradas dentro da função do controller sem `$scope` não ficam disponíveis para a view.

```js
app.controller("TesteCtrl", function($scope) {
	const nome = "Ana";
	$scope.idade = 20;
});
```

Na view, `nome` não aparece, mas `idade` aparece.

Porque a view só enxerga o que está no `$scope`.

---

# 8. Erros comuns

### Esquecer de usar $scope

Se o valor precisa ir para a view, ele deve estar no scope.

### Colocar tudo no controller

Isso torna a tela difícil de manter

### Achar que controller é igual service

Controller organiza a tela; service centraliza a lógica reutilizável.

---

### 9. Boas práticas

- manter controller enxuto;
- usar nomes claros para funções da tela;
- delegar regra reutilizável para service;
- expor no `$scope` apenas o que a view precisa;
- evitar acoplamento desnecessário com DOM.

---

## 10. Relação com outros conteúdos

Esse tema se conecta com:

- Modulos e bootstrap em Frontend/estudos/angularjs/documentos-de-estudo/secao-01-fundamentos/1 - Módulos e bootstrap.md;
- Scope e digest em Frontend/estudos/angularjs/documentos-de-estudo/secao-03-scope-digest-ciclo-vida/2 - Digest cycle e watchers.md;
- Services em Frontend/estudos/angularjs/documentos-de-estudo/secao-02-arquitetura-organizacao/1 - Controller vs Service vs Factory.md.

---

## Conclusão

Controller e `$scope` são a ponte mais básica entre lógica e interface em AngularJS.

Quando você domina isso, o resto da arquitetura fica muito mais fácil de entender.
