# 1 - Módulos e bootstrap

Em AngularJS, o módulo é a base organizacional da aplicação.

Ele registra os artefatos que a aplicação vai usar, como controller, service, directive, filtro e configurações.

O bootstrap e o processo de inicialização do AngularJS na página.

---

## 1. O que é um módulo

Um módulo é um container lógico da aplicação.

Exemplo:
```js
const app = angular.module("app", []);
```

Nesse exemplo:

- `app` é o nome do módulo;
- `[]` representa dependências;
- o Angular passa a conhecer esse módulo.

---

## 2. Por que o módulo existe

O módulo existe para organizar a aplicação e agrupar o que pertence ao mesmo contexto.

Sem isso, o código ficaria espalhado e difícil de entender.

Com módulo, você consegue:

- separar áreas do sistema;
- registrar dependências;
- estruturar controllers e services;
- iniciar a aplicação de forma previsível.

---

## 3. Criando e recuperando módulo

### Criar módulo

```js
const app = angular.module("app", []);
```

Diferença prática:

- com `[]`, você cria o módulo;
- sem `[]`, você acessa um módulo já criado.

---

## 4. Dependências do módulo

O segundo parâmetro de `angular.module` recebe as dependências.

```js
const app = angular.module("app", ["ngRoute"]);
```

Isso quer dizer que o módulo `app` depende do módulo `ngRoute`.

Esse padrão é importante porque AngularJS trabalha muito com injeção de dependência.

---

## 5. O que é bootstrap

Bootstrap é o processo de iniciar o AngularJS na página.

Normalmente ele acontece quando o framework encontra `ng-app`.

Exemplo:

```html
<html ng-app="app">
```

Nesse momento, o AngularJS procura o módulo chamado `app` e começa a preparar a aplicação.

---

## 6. Como isso funciona na prática

```html
<!DOCTYPE html>
<html ng-app="app">
<head>
	<meta charset="UTF-8" />
	<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.8.2/angular.min.js"></script>
</head>
<body>
	<div ng-controller="MainCtrl">
		<p>{{ titulo }}</p>
	</div>

	<script>
		const app = angular.module("app", []);

		app.controller("MainCtrl", function($scope) {
			$scope.titulo = "AngularJS iniciado";
		});
	</script>
</body>
</html>
```

Fluxo:
1. o navegador carrega a página;
2. o Angular encontra `ng-app`;
3. o módulo `app` é localizado;
4. o controller é registrado;
5. a view recebe os dados;
6. a página passa a funcionar em AngularJS.

---

## 7. Erros comuns

### Esquecer de declarar o módulo

Se `ng-app` aponta para um módulo inexistente, a aplicação não sobe corretamente.

### Misturar tudo em um único módulo sem critério

Projetos maiores precisam de organização por responsabilidade.

### Criar módulo mas não registrar nada nele

O módulo existe para agrupar os artefatos da aplicação.

---

## 8. Boas práticas

- criar um módulo principal para entrada da aplicação;
- separar módulos por área quando o projeto crescer;
- manter nomes consistentes;
- registrar dependências de forma explícita;
- usar bootstrap simples e previsível.

---

## 9. Relação com outros conteúdos

Este assunto se conecta com:

- Controllers e $scope em Frontend/estudos/angularjs/documentos-de-estudo/secao-01-fundamentos/2 - Controllers e $scope.md;
- Diretivas em Frontend/estudos/angularjs/documentos-de-estudo/secao-01-fundamentos/4 - Diretivas nativas essenciais.md;
- Estrutura e organizacao em Frontend/estudos/angularjs/documentos-de-estudo/secao-02-arquitetura-organizacao/3 - Estrutura de pastas em projetos legados.md.

---

## Conclusão

Módulo e bootstrap são o ponto de partida do AngularJS.

Se você entende bem esse início, fica muito mais fácil compreender como o framework conecta view, controller e dependências.
