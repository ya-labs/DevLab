# 4 - Diretivas nativas essenciais

Diretivas são instruções que você coloca no HTML para dizer ao AngularJS como aquele trecho deve se comportar.

As diretivas nativas são uma das marcas mais importantes do framework.

---

## 1. O que é uma diretiva

Diretiva é um atributo, elemento ou comportamento que o AngularJS entende e processa.

Exemplo:

```html
<input ng-model="nome" />
```

Aqui, `ng-model` é uma diretiva.

---

## 2. Por que diretivas existem

Elas existem para tornar o HTML dinâmico sem precisar manipular tudo manualmente no JavaScript.

Com diretivas, a view fica mais declarativa.

---

## 3. Diretivas nativas mais importantes

### ng-app

Define o ponto de início da aplicação.

```html
<div ng-controller="MainCtrl"></div>
```

### ng-model

Faz bind de formulário com o scope.

```html
<input ng-model="nome" />
```

### ng-click

Executa uma função ao clicar.

```html
<button ng-click="salvar()">Salvar</button>
```

### ng-repeat

Repete os elementos para cada item de uma lista.

```html
<li ng-repeat="item in itens">{{ item }}</li>
```

### ng-if

Mostra ou remove o elemento do DOM.

```html
<p ng-if="logado">Bem-vindo</p>
```

### ng-show e ng-hide

Controlam exibição via CSS.

```html
<p ng-show="visivel">Texto</p>
```

### ng-class

Aplica classe dinamicamente.

```html
<p ng-class="{ ativo: isAtivo }">Status</p>
```

### ng-disabled

Desabilita elemento com base em condição.

```html
<button ng-disabled="!podeSalvar">Salvar</button>
```

---

## 4. Exemplo prático

```html
<div ng-app="app" ng-controller="ListaCtrl">
	<input ng-model="novoItem" placeholder="Novo item" />
	<button ng-click="adicionar()">Adicionar</button>

	<ul>
		<li ng-repeat="item in itens">{{ item }}</li>
	</ul>
</div>
```

```js
const app = angular.module("app", []);

app.controller("ListaCtrl", function($scope) {
	$scope.novoItem = "";
	$scope.itens = ["Arroz", "Feijao"];

	$scope.adicionar = function() {
		if ($scope.novoItem.trim() === "") {
			return;
		}

		$scope.itens.push($scope.novoItem);
		$scope.novoItem = "";
	};
});
```

Esse exemplo usa:

- `ng-app` para iniciar;
- `ng-controller` para ligar a tela;
- `ng-model` para o input;
- `ng-click` para ação;
- `ng-repeat` para lista.

---

## 5. Diferenças importantes

### ng-if x ng-show

- `ng-if` remove e recria o elemento;
- `ng-show` apenas esconde com CSS.

### ng-repeat x loop manual

- `ng-repeat` integra com o AngularJS;
- loop manual costuma exigir manipulação de DOM.

### ng-model x value fixo

- `ng-model` sincroniza entrada;
- valor fixo só exibe.

---

## 6. Erros comuns

### Usar diretiva sem contexto de scope

Se a variável não existe no controller, a view não consegue refletir corretamente.

### Exagerar em lógica dentro do HTML

Diretiva não é lugar para regra complexa.

### Confundir ng-if com ng-show

Os dois parecem iguais, mas o comportamento interno é diferente.

---

## 7. Boas práticas

- usar a diretiva certa para a necessidade certa;
- manter o HTML declarativo;
- evitar repetição desnecessária de comportamento;
- usar `ng-repeat` com cuidado em listas grandes;
- preferir diretivas para expressar comportamento de view.

---

## 8. Relação com outros conteúdos

Esse assunto se conecta com:

- Interpolação e two-way binding em Frontend/estudos/angularjs/documentos-de-estudo/secao-01-fundamentos/3 - Interpolação e two-way binding.md;
- Controller e $scope em Frontend/estudos/angularjs/documentos-de-estudo/secao-01-fundamentos/2 - Controllers e $scope.md;
- Componentização e directives em Frontend/estudos/angularjs/documentos-de-estudo/secao-04-componentizacao-diretivas/1 - Directive: conceito e estrutura.md.

---

## Conclusão

Diretivas são uma das bases da declaratividade no AngularJS.

Quando você entende as nativas essenciais, consegue ler e escrever muito mais do comportamento de tela do framework.
