# 1 - Modularização moderna ≠ só arquivos separados

um erro comum é pensar:

> <span style="color:white;">"Modularizar = dividir em vários arquivos"</span>

Isso é o nível 1.

No mercado, modularização significa:

> <span style="color:white;">Organizar o código por responsabilidade, domínio e isolamento.</span>

ou seja:
- não é só separar
- é separar com intenção arquitetural

---

# 2 - Princípios que guiam a modularização moderna

## 1 - Single responsibility (SRP)

Cada módulo deve ter uma única responsabilidade clara

exemplo negativo:
```js
export function formatarNome() {}
export function calcularFrete() {}
export function conectaBanco() {}
```

exemplo positivo:
```js
// format/formatNome.js
export function formatarNome(nome) {
    return nome.trim().toUpperCase();
}

// frete/calcularFrete.js
export function calcularFrete(peso, distancia) {
    return peso * distancia * 0.1;
}

// database/conectaBanco.js
export function conectaBanco() {
    return { status: 'conectado' };
}
```

Isso facilita:
- manutenção
- testes
- reutilização

---

## 2 - Baixo acoplamento

módulos não devem depender fortemente uns dos outros

exemplo negativo:
```js
import { salvarPedido } from '../pedido/service.js';
import { enviarEmail } from '../email/service.js';
import { gerarNota } from '../nota/service.js';
```

módulo fazendo tudo = acoplamento alto.

exemplo positivo:
```js
// pedido/service.js
export function criarPedido(dados, servicoNotificacao) {
    const pedido = { id: Date.now(), ...dados };
    servicoNotificacao.confirmarPedido(pedido);
    return pedido;
}

// email/service.js
export function confirmarPedidoPorEmail(pedido) {
    console.log(`Email enviado para o pedido ${pedido.id}`);
}

// app.js
import { criarPedido } from './pedido/service.js';
import { confirmarPedidoPorEmail } from './email/service.js';

const servicoNotificacao = {
    confirmarPedido: confirmarPedidoPorEmail,
};

criarPedido({ cliente: 'Nicolas', total: 199.9 }, servicoNotificacao);
```

Aqui, o módulo de pedido depende de um contrato simples (confirmarPedido), e não de uma implementação específica.
Isso reduz acoplamento e facilita troca de estratégia (email, SMS, push) sem alterar a regra de negócio.

## 3 - Alta coesão

Coisas relacionadas ficam juntas

exemplo:
```
/usuario
    usuario.service.js
    usuario.controller.js
    usuario.repository.js
```
tudo que é de usuário fica no mesmo lugar.

--- 

# 3 - Padrão real de organização

Estrutura por feature (feature-based)
Padrão muito utilizado pelo mercado moderno (React, Angular, Backend...)

```
/src
    /modules
        /usuario
            usuario.service.js
            usuario.controller.js
            usuario.repository.js
        /produto
            produto.service.js
            produto.controller.js
            produto.repository.js
    /shared
        /utils
            formatarData.js
            calcularDesconto.js
        /components
            Button.js
            Modal.js
```

A força dessa arquitetura é explicada:
O sistema é organizado por domínio de negócio, não por tipo técnico. Isso facilita a evolução do sistema, pois cada módulo é responsável por um aspecto específico do negócio, e as dependências são controladas. O código fica mais fácil de entender, manter e escalar.

Estrutura antiga:
```
/controllers
/services
/repositories
```
> Espalha tudo

Moderna:
```
/usuario
/pedido
```
> Agrupa por domínio, não por tipo técnico.

Um domínio é, resumidamente, uma parte do sistema que tem uma responsabilidade específica e um conjunto de regras de negócio relacionadas. Por exemplo, o domínio de "usuário" é responsável por tudo relacionado à gestão de usuários, como cadastro, autenticação e perfil.

---

# 4 - index.js (barrel file)

Muito usado, pouca gente entende o real propósito.

problema:
```js
import { criarUsuario } from './modules/usuario/usuario.service.js';
```
> Importação verbosa, difícil de manter.

solução, criar um index.js em cada módulo:
```js
// modules/usuario/index.js
export * from './usuario.service.js';
export * from './usuario.controller.js';
export * from './usuario.repository.js';
```

Agora, a importação fica mais limpa:
```js
import { criarUsuario } from './modules/usuario';
```

- Limpa imports
- Desacopla estrutura interna

index.js é apenas um exemplo, o importante é ter um ponto de entrada claro para cada módulo, seja ele index.js ou outro nome. O objetivo é facilitar o consumo do módulo sem expor detalhes internos.

O nome index.js é uma convenção, vem da prática de criar um ponto de entrada padrão para módulos em JavaScript, "index" significa "índice" ou "entrada principal".

> <span style="color:white;">Útil, mas usar com critério.</span>

podem gerar:
- imports desnecessários 
- circular dependency
- bundle maior dependendo do bundler 

---

# Tipos principais de arquitetura

- [Layered](#Layered)
- [Clean architecture](#Clean%20architecture)
- [Hexagonal](#Hexagonal)
- [Vertical slice](#Vertical%20slice)
- [Feature-first](#Feature%20first)
- [Camadas (layered architecture)](#Camadas-layered%20architecture)
- [Onion architecture](#Onion%20architecture)
- [Microservices](#Microservices)

---

# 6 - Modularização + escalabilidade

Ao crescer, o projeto evolui para:
> <span style="color:white;">Módulos independentes</span>
```
/modules
    /auth
    /billing
    /orders
```
Cada módulo pode virar:
- microserviço
- lib separada

# 7 - modularização + bundlers (webpack, vite)

ESM entra aqui forte:
- tree-shaking
- code splitting
- lazy loading

^^^ APROFUNDAR

---

# 8 - Modularização + testes

Módulos bem separados:
- fácil de testar
- fácil de mockar

```js
import * as repo from "./repo.js";
jest.spyOn(repo, "salvar")
```
isso só funciona bem com baixo acoplamento.
^^^ APROFUNDAR

---

# 9 - Erros comuns

## 1 - utils gigante

```js
utils.js com 500 funções:
export function formatarData() {}
export function calcularDesconto() {}
export function validarEmail() {}
...
```

Isso vira um monstro difícil de manter.
O ideal é separar por domínio:
```
/format/formatarData.js
/desconto/calcularDesconto.js
/validacao/validarEmail.js
```

## 2 - Módulos sem responsabilidade clara
```js
helpers.js
common.js
```

Nome genérico = código mal organizado
O ideal para módulos é ter um propósito claro e específico

## 3 - Dependências circulares
```js
A importa B
B importa A
```

Pode:
- gerar undefined
- incialização parcial
- comportamento inconsistente
- bugs silenciosos

## 4 - Abstração precoce

Basicamente, querer modularizar demais sem necessidade.
-> Cria complexidade inútil

Exemplo:
```js
// Módulo de usuário com 2 funções
export function criarUsuario() {}
export function deletarUsuario() {}

// Módulo de autenticação com 1 função
export function autenticar() {}
```

-> Módulos com poucas responsabilidades, mas sem necessidade real de separação.

---

# 10 - Bundlers

---

# 11 - Dependency injection

---

# 12 - Separation of concerns

---

# 13 - Public API do módulo

---

# 14 - Encapsulamento na modularização

---

# 15 - Anti-patterns reais