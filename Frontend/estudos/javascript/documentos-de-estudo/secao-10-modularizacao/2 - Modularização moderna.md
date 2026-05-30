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

## 1 - Single Responsibility (SRP)

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
checkout -> 
```js
function finalizarPedido(pedido) {
    salvarNoBancoMySQL(pedido);
    enviarEmailSMTP(pedido.cliente.email);
    gerarPdfComBibliotecaXPTO(pedido);
}
```

problema:
esse código sabe detalhes demais.

ele sabe:
- qual banco
- como envia email
- qual biblioteca gera PDF

quebra se trocar:
- MySQL por PostgreSQL
- SMTP por API de email
- PDF lib

isso é acoplamento forte, o módulo depende de detalhes de implementação de outros.

Versão melhor:

```js
function finalizarPedido(pedido, pedidoRepo, notificacaoService, notaService) {
    pedidoRepo.salvar(pedido);
    notificacaoService.enviarConfirmacao(pedido);
    notaService.gerar(pedido);
}
```
No exemplo, o módulo recebe dependências externas e usa apenas seus comportamentos esperados.

Ele não sabe como pedidoRepo salva, como notificacaoService envia email ou como notaService gera PDF. Ele só sabe que precisa dessas operações, mas não como elas são implementadas.

## analogia fácil

> <span style="color: white; font-weight: bold">alto acoplamento:</span>

você dirige e precisa saber:

- como motor funciona
- como câmbio funciona
- como injeção funciona

> <span style="color: white; font-weight: bold">baixo acoplamento:</span>

você só usa:

acelerar
frear
virar

detalhes internos ficam escondidos.

isso é abstração + baixo acoplamento.

## o conceito correto

baixo acoplamento NÃO é:

<span style="color: #bd5353;">"usar menos imports"</span>
<span style="color: #bd5353;">"dividir arquivos"</span>

baixo acoplamento é:

<span style="color: #64ac6e;">depender de contratos/comportamentos, não implementações específicas</span>

> <span style="color: white; font-weight: bold">baixo acoplamento não significa usar menos imports, significa depender menos de implementações concretas.</span>

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

A principal vantagem desse padrão:
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

# 5 - Arquiteturas relacionadas à modularização

- Clean architecture
- Hexagonal
- Vertical Slice
- Feature-First
- Camadas (Layered Architecture)
- Onion Architecture
- Microservices

Essas arquiteturas aprofundam conceitos de modularização e organização de sistemas, e podem ser estudadas separadamente.

---

# 6 - Modularização + escalabilidade

Em sistemas maiores, é comum evoluir para módulos mais independentes:
> <span style="color:white;">Módulos independentes</span>
```
/modules
    /auth
    /billing
    /orders
```

uma boa modularização facilita futuras separações arquiteturais, incluindo extração para serviços independentes.

# 7 - modularização + bundlers (webpack, vite)

ESM entra aqui forte ([ver explicação em ES6 Modules](1%20-%20ES6%20Modules.md#o-que-e-esm)):
- [tree-shaking](1%20-%20ES6%20Modules.md#o-que-e-tree-shaking)
- code splitting
- lazy loading

---

# 8 - Modularização + testes

Uma boa modularização facilita muito a criação de testes, porque cada parte do sistema pode ser testada de forma isolada.

Quando um módulo tem uma responsabilidade clara, fica mais fácil verificar se ele funciona corretamente sem depender do sistema inteiro.

Exemplo:

```js
// usuarioService.js
export function criarUsuario(dados, repo) {
    if (!dados.nome) {
        throw new Error("Nome é obrigatório");
    }

    return repo.salvar(dados);
}
```

No teste, não é necessário usar o banco real:

```js
const repoMock = {
    salvar: jest.fn(),
};

criarUsuario({ nome: "Nícolas" }, repoMock);

expect(repoMock.salvar).toHaveBeenCalled();
```

Nesse caso, o teste verifica apenas a regra do `usuarioService`, sem depender de banco, API ou arquivos externos.

Quando o código é muito acoplado, testar fica mais difícil, porque uma função simples pode acabar exigindo várias dependências reais para funcionar.

Resumo:
- módulos pequenos são mais fáceis de testar
- baixo acoplamento facilita mocks
- responsabilidades claras reduzem testes complexos
- código modular permite testar partes específicas do sistema

### Extra: introdução ao Jest

Framework de testes para JavaScript. Muito usado para testar código.

exemplo:
```js
function somar(a, b) {
    return a + b;
}
```
Teste:
```js
test("deve somar corretamente", () => {
    expect(somar(2, 3)).toBe(5);
});
```
Nesse caso:
- test() define um teste
- expect() verifica um resultado esperado
- toBe() compara o valor retornado

jest.fn() cria uma função falsa (mock), usada para simular comportamentos em testes.

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
- inicialização parcial
- comportamento inconsistente
- bugs silenciosos

## 4 - Abstração prematura

Cenário simples
É necessário cadastrar usuário.

normal:
```js
function cadastrarUsuario (usuario) {
    salvar(usuario);
}
```
simples.

abstração prematura:
```js
class AbstractUserPersistenceFactoryManager {
    criarPersistencia() {
        if (tipoBanco === 'mysql') {
            return new MySQLUserRepository();
        } else if (tipoBanco === 'postgres') {
            return new PostgresUserRepository();
        } else {
            throw new Error('Banco de dados não suportado');
        }
    }
}
```

só que projeto:
- tem 1 banco
- 1 cadastro
- nunca vai trocar isso

outro exemplo:
É necessário formatar nome:
```js
formatarNome(nome) {
    return nome.trim().toUpperCase();
}
```

mas cria:
```js
class NomeFormatterManager
class NomeFormatterFactory
class AbstractNomeFormatterBase
```
Utilizando de Factory, Manager e Abstract Base para algo simples demais.

<span style="color: #64ac6e;">Abstração saudável:</span>
problema REAL apareceu -> abstrai.

<span style="color: #bd5353;">Abstração prematura:</span>
problema IMAGINADO -> abstrai.

---

# 10 - Bundlers

Bundlers são ferramentas que analisam seu projeto inteiro e empacotam os arquivos para execução otimizada

Em muitas aplicações modernas, ainda usamos bundlers para otimização, mesmo com suporte nativo a módulos no navegador.

O bundler resolve isso.

Ele:
- lê imports do projeto
- entende dependências
- junta arquivos
- remove código morto
- otimiza assets
- divide código quando necessário

Exemplo:

Projeto:
```
/src
    main.js
    usuario.js
    pedido.js
```

código:

```js
// main.js
import { criarUsuario } from './usuario.js';
import { criarPedido } from './pedido.js';
```

Sem bundler:

O navegador precisa carregar main.js, usuario.js e pedido.js separadamente, o que gera múltiplas requisições HTTP.

Resultando:
- projeto lento
- muitos requests
- sem otimização
- sem minificação
- sem code splitting

Eles existem para transformar código de desenvolvimento em código de produção.

Com bundler, vira algo como:

```
dist/app.bundle.js
```

Processado e otimizado.

## Principais bundlers

> <span style="color: white; font-weight: bold">Webpack</span>

- Muito popular historicamente.
- Extremamente configurável.
- Usado em muitos projetos legados e grandes aplicações.

> <span style="color: white; font-weight: bold">Vite</span>

- Padrão moderno.
- Muito mais rápido no desenvolvimento.
- Usa [ESM](1%20-%20ES6%20Modules.md#o-que-e-esm) nativamente durante dev
- Build final geralmente usa Rollup internamente

> <span style="color: white; font-weight: bold">Rollup</span>

- Excelente para bibliotecas.
- Muito eficiente em [tree-shaking](1%20-%20ES6%20Modules.md#o-que-e-tree-shaking).

> <span style="color: white; font-weight: bold">Parcel</span>

- Mais simples
- Quase zero configuração

## Conceitos importantes

> <span style="color: white; font-weight: bold">Bundle</span> 

Arquivo final gerado:

```
app.bundle.js (padrão de nome, pode ser customizado)
```

> <span style="color: white; font-weight: bold">Code splitting</span>

Divide bundle em partes menores.

Ao invés de:

```
app gigante com 5mb
```

Vira:

```
main.js
dashboard.chunk.js
admin.chunk.js
```

Carrega sob demanda.

> <span style="color: white; font-weight: bold">Lazy loading</span>

Carregamento tardio.

Exemplo:

```js
const dashboard = await import('./dashboard.js');
```

Só carrega quando necessário.

---

# 11 - Dependency injection

Dependency injection (DI) é um padrão onde dependências são fornecidas externamente ao módulo, em vez de serem criadas dentro dele.

Objetivo:

reduzir acoplamento.

> <span style="color: #bd5353;">Sem DI:</span>

```js
class PedidoService {
    constructor() {
        this.emailService = new SmtpEmailService();
    }

    finalizar() {
        this.emailService.enviar();
    }
}
```

Problema:

`PedidoService` depende diretamente de `SmtpEmailService`.

Se trocar implementação para `SendgridEmailService`
Precisa alterar o código.

> <span style="color: #64ac6e;">Com DI:</span>

```js
class PedidoService {
    constructor(emailService) {
        this.emailService = emailService;
    }

    finalizar() {
        this.emailService.enviar();
    }
}
```

Uso:

```js
const pedidoService = new PedidoService(new SmtpEmailService());
```

Ou:

```js
const pedidoService = new PedidoService(new SendgridEmailService());
```

Agora a classe só espera que a dependência possua o método enviar()

```js
enviar();
```

Não da implementação concreta.

## Benefícios:
- baixo acoplamento
- troca fácil de implementações
- testes mais simples
- código mais flexível
- maior reutilização

## Em testes

> <span style="color: #bd5353;">Sem DI:</span>

difícil mockar.

> <span style="color: #64ac6e;">Com DI:</span>

```js
const mockEmailService = {
    enviar() {
        console.log("mock");
    },
};

new PedidoService(mockEmailService);
```

Muito mais simples.

---

# 12 - Separation of concerns

Significa separar responsabilidades distintas.

Cada parte do sistema deve cuidar de sua própria preocupação.

Exemplo de preocupações:
- interface
- regras de negócio
- persistência
- validação
- autenticação

### Errado:

```js
function cadastrarUsuario(dados) {
    validarDados(dados);

    fetch('/api/usuarios', {
        method: 'POST',
        body: JSON.stringify(dados),
    });

    atualizarTela();

    enviarEmailBoasVindas();
}
```

Essa função faz tudo.

Mistura:

- validação
- API
- UI
- notificação

### Certo:

```js
usuarioValidator.validar(dados);
usuarioRepository.salvar(dados);
usuarioNotifier.enviarBoasVindas(dados);
usuarioView.atualizar();
```

Cada responsabilidade separada.

### Benefícios:

- manutenção simples
- menos bugs
- testes melhores
- código legível
- reutilização

Modularização é uma ferramenta para aplicar separation of concerns, mas não garante isso sozinha. É necessário projetar os módulos com essa filosofia em mente.

---

# 13 - Public API do módulo

Todo módulo expõe apenas o necessário.

Isso é sua API pública.

Exemplo:

```js
// usuario.js
export function criarUsuario () {}
export function buscarUsuario () {}
```

Essas funções fazem parte da API pública.
Outros módulos podem usá-las.

### O que não faz parte

```js
function validarCPFInternamente() {}
function normalizarDados() {}
```

não exportadas, inacessíveis externamente ao módulo

### Ideia central

O módulo define:
`O que o mundo externo pode usar`
E esconde:
`Como aquilo funciona internamente`

### Analogia: controle remoto

API pública:
```
Ligar
Desligar
Volume
```

Interno:

```
Circuitos
Processamento
Hardware
```

Usuário não precisa saber.

### Benefícios
- reduz acoplamento
- protege implementação
- facilita manutenção
- evita uso indevido

---

# 14 - Encapsulamento na modularização

Encapsulamento significa esconder detalhes internos e expor apenas o necessário.

Modularização ajuda diretamente nisso.

### Exemplo:

```js
// pagamento.js

function validarCartao() {}
function autenticarBanco() {}
function gerarToken() {}

export function processarPagamento() {
    validarCartao();
    autenticarBanco();
    gerarToken();
}
```

Exposto:

```js
processarPagamento();
```

### Por que isso importa?

Se outro módulo pudesse chamar:

```js
autenticarBanco();
```

Diretamente:
- quebraria fluxo
- poderia expor operações sensíveis
- permitiria uso incorreto

### Relação com OOP

Mesmo fora de classes, módulos oferecem encapsulamento.

Não é exclusivo de orientação a objetos.

---

# 15 - Anti-patterns reais

Anti-pattern = solução comum que parece boa, mas gera problemas reais.

### 1 - God module

Um módulo gigante que faz tudo.

Exemplo:
```js
UserManager.js
```

Com:
- login
- cadastro
- email
- banco
- relatórios
- permissões
Problema:
- impossível manter
- alto acoplamento
- difícil de testar

### 2 - Utils gigante

```js
utils.js
```

com 300 funções.

Problema:
vira lixeira de código, um arquivo que colocamos qualquer função que não encontramos lugar específico.

### 3 - Helpers genéricos

```js
helpers.js
common.js
misc.js
```

Nomes vagos.
Problema: 
- Nínguem sabe responsabilidade real.

### 4 - [Dependências circulares](#9---erros-comuns)

### 5 - [Abstrações prematuras](#9---erros-comuns)

### 6 - Barrel file em excesso

Criar: 
```
index.js
```
para tudo.

Problemas: 
- dependências circulares
- imports desnecessários
- bundle pior

### 7 - Vazar implementação interna

Exemplo:
```js
export function validarCPFInternamente() {}
```

Mesmo sendo detalhe privado.

Problema:
- outros módulos passam a depender disso.

Depois fica difícil refatorar.

### 8 - Módulos acoplados demais

```js
PedidoService cria EmailService cria PDFService cria Logger
```

Problema:
- efeito dominó em mudanças

### 9 - Arquitetura astronauta

Overengineering.

Criar:
- factories
- strategies
- adapters
- builders

sem necessidade real.

Problema:

código difícil de entender.

### Regra prática
Se sua modularização:
- aumentou complexidade
- dificultou entendimento
- dificultou manutenção

provavelmente foi mal aplicada. 