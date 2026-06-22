# 3 - AngularJS vs Angular moderno

Um erro muito comum é tratar AngularJS e Angular moderno como se fossem a mesma tecnologia.

Não são.

Eles têm base, arquitetura e experiência de desenvolvimento diferentes.

---

## 1. Diferença essencial

AngularJS:

- framework baseado em scope, controllers e directives;
- foco em arquitetura MVC antiga;
- JavaScript tradicional.

Angular moderno (2+):

- framework baseado em componentes;
- TypeScript como padrão;
- arquitetura e tooling modernos.

---

## 2. Comparação rápida

## Arquitetura

- AngularJS: controller + scope + template.
- Angular moderno: component + class + template.

## Binding

- AngularJS: forte uso de two-way binding automático.
- Angular moderno: fluxo mais explícito, com unidirecional como base mental em muitos cenários.

## Programação

- AngularJS: JavaScript.
- Angular moderno: TypeScript.

## Reatividade

- AngularJS: digest cycle + watchers.
- Angular moderno: change detection com estratégia mais moderna e integração maior com RxJS.

## Ferramentas

- AngularJS: ecossistema antigo.
- Angular moderno: CLI, build moderno, padrões atuais de projeto.

---

## 3. Exemplo mental equivalente

Em AngularJS, uma tela simples costuma nascer assim:

```js
const app = angular.module("app", []);

app.controller("ProdutoCtrl", function($scope) {
	$scope.nome = "Notebook";
});
```

No Angular moderno, a mesma ideia aparece no componente:

```ts
import { Component } from "@angular/core";

@Component({
	selector: "app-produto",
	template: "<p>{{ nome }}</p>"
})
export class ProdutoComponent {
	nome = "Notebook";
}
```

A intenção é parecida: exibir dado na tela.

A estrutura e o ecossistema são diferentes.

---

## 4. O que muda no dia a dia do desenvolvedor

No AngularJS:

- você lida mais com controller e scope;
- precisa dominar bem digest/watchers;
- encontra bastante código legado sem padrão único.

No Angular moderno:

- você trabalha com componentes, módulos e serviços em TypeScript;
- usa ecossistema mais padronizado;
- geralmente encontra melhor integração com ferramentas modernas.

---

## 5. Erros comuns nessa comparação

### Achar que migrar é só copiar código

Migração exige ajustar arquitetura e modelo mental.

### Ignorar custo de negócio

Nem todo sistema precisa migrar tudo imediatamente.

### Tratar AngularJS como sem valor

Ele ainda sustenta produtos importantes e exige conhecimento técnico real para manutenção.

---

## 6. Boas práticas para estudar os dois

- entender primeiro os fundamentos de JavaScript;
- estudar AngularJS com foco em legado e manutenção;
- estudar Angular moderno com foco em novos projetos;
- comparar conceitos equivalentes para acelerar aprendizado.

---

## 7. Ponte com a trilha deste repositório

Para apoiar essa comparação, vale revisar:

- Funções básicas em Frontend/estudos/javascript/documentos-de-estudo/secao-05-funcoes/1 - Funções básicas.md;
- Funções avançadas em Frontend/estudos/javascript/documentos-de-estudo/secao-05-funcoes/2 - Funções avançadas.md;
- Modularização moderna em Frontend/estudos/javascript/documentos-de-estudo/secao-10-modularizacao/2 - Modularização moderna.md.

Esses assuntos deixam a transição de conceito muito mais clara.

---

## Conclusão

AngularJS e Angular moderno compartilham o nome Angular, mas representam fases diferentes do desenvolvimento frontend.

Entender essa diferença evita expectativas erradas e melhora muito a qualidade das decisões em projetos reais.
