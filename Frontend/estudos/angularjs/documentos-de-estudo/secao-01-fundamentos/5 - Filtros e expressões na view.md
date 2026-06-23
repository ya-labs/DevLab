# 5 - Filtros e expressões na view

Filtros e expressões são recursos usados para transformar e mostrar dados diretamente na view.

Eles ajudam a deixar o HTML mais expressivo e menos verboso.

---

## 1. O que são expressões

Expressões são pequenas instruções que o AngularJS avalia dentro da view.

Exemplo:

```html
<p>{{ 2 + 2 }}</p>
```

Outro exemplo:

```html
<p>{{ usuario.nome }}</p>
```

Expressões servem para:

- exibir valores;
- acessar propriedades;
- chamar lógicas simples;
- montar saídas dinâmicas.

---

## 2. O que são filtros

Filtros transformam um valor antes de ele ser exibido.

Sintaxe:

```html
{{ valor | filtro }}
```

Exemplo:

```html
<p>{{ nome | uppercase }}</p>
```

Se `nome` for `ana`, o resultado será `ANA`.

---

## 3. Por que isso existe

Filtros existem para deixar a view mais prática e expressiva.

Em vez de transformar tudo no controller, você pode formatar diretamente na exibição.

Isso é util para:

- formatação de texto;
- formatação de moeda;
- ordenação de listas;
- limitação de itens;
- exibição condicional de dados.

---

## 4. Filtros nativos mais usados

### uppercase

Converte para maiúsculas.

```html
{{ nome | uppercase }}
```

### lowercase

Converte para minúsculas.

```html
{{ nome | lowercase }}
```

### currency

Formatação de moeda.

```html
{{ preco | currency }}
```

### date

Formata datas.

```html
{{ dataCadastro | date:"dd/MM/yyyy" }}
```

### limitTo

Limita tamanho de texto ou quantidade de itens.

```html
{{ descricao | limitTo:50 }}
```

### orderBy

Ordena listas.

```html
<li ng-repeat="item in itens | orderBy:'nome'">{{ item.nome }}</li>
```

### filter

Filtra listas por critério.

```html
<li ng-repeat="item in itens | filter:busca">{{ item.nome }}</li>
```

---

## 5. Exemplo prático

```html
<div ng-app="app" ng-controller="ProdutoCtrl">
	<p>{{ nome | uppercase }}</p>
	<p>{{ preco | currency }}</p>
	<p>{{ dataCadastro | date:"dd/MM/yyyy" }}</p>

	<input ng-model="busca" placeholder="Buscar produto" />

	<ul>
		<li ng-repeat="produto in produtos | filter:busca | orderBy:'nome'">
			{{ produto.nome }} - {{ produto.preco | currency }}
		</li>
	</ul>
</div>
```

```js
const app = angular.module("app", []);

app.controller("ProdutoCtrl", function($scope) {
	$scope.nome = "notebook";
	$scope.preco = 3500;
	$scope.dataCadastro = new Date();
	$scope.busca = "";

	$scope.produtos = [
		{ nome: "Mouse", preco: 80 },
		{ nome: "Teclado", preco: 150 },
		{ nome: "Monitor", preco: 1200 }
	];
});
```

---

## 6. Expressões x filtros

### Expressão

Avalia um valor ou pequena lógica.

```html
{{ total + desconto }}
```

### Filtro

Transforma a saída.

```html
{{ nome | uppercase }}
```

Resumo simples:

- expressão calcula;
- filtro formata.

---

## 7. Erros comuns

### Colocar lógica pesada na view

Filtro não deve virar regra complexa de negócio.

### Confundir formatação com processamento

A view é lugar de apresentação, não de regra central do sistema.

### Usar filtro sem necessidade

Se a transformação for complexa, talvez seja melhor preparar o dado no controller ou service.

---

## 8. Boas práticas

- usar filtros para apresentação;
- manter expressões simples;
- evitar cálculos grandes dentro do HTML;
- usar filtros nativos quando suficiente;
- criar filtros customizados apenas quando houver reaproveitamento real.

---

## 9. Relação com outros conteúdos

Esse tema se conecta com:

- Interpolacao em Frontend/estudos/angularjs/documentos-de-estudo/secao-01-fundamentos/3 - Interpolação e two-way binding.md;
- Diretivas em Frontend/estudos/angularjs/documentos-de-estudo/secao-01-fundamentos/4 - Diretivas nativas essenciais.md;
- Filtros customizados em Frontend/estudos/angularjs/documentos-de-estudo/secao-04-componentizacao-diretivas/5 - Refatorando telas para componentes.md.

---

## Conclusão

Expressões e filtros tornam a view do AngularJS mais legível e declarativa.

Usados com critério, eles ajudam a exibir dados de forma limpa sem empurrar lógica demais para o HTML.
