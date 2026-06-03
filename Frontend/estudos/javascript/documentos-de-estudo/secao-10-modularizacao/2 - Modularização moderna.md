# Modularização moderna

Modularizar não significa apenas dividir código em vários arquivos.

Em projetos reais, modularização significa organizar o código por responsabilidade, domínio e intenção.

---

# 1 - O que é modularização moderna

Separar arquivos é só o primeiro passo.

Modularização moderna busca responder:

- qual é a responsabilidade deste arquivo?
- esse módulo sabe demais sobre outros módulos?
- essa função pertence mesmo aqui?
- esse código pode ser testado isoladamente?
- outro dev consegue entender essa organização?

Um bom módulo tem um motivo claro para existir.

---

# 2 - Por que modularização importa

Projetos crescem.

Sem modularização, é comum aparecer:

- arquivo gigante;
- função com muitas responsabilidades;
- regra duplicada;
- importação confusa;
- acoplamento forte;
- dificuldade para testar;
- manutenção lenta.

Modularização existe para tornar o projeto mais fácil de evoluir.

---

# 3 - Responsabilidade única

Um módulo deve ter uma responsabilidade principal.

Exemplo ruim:

```js
export function formatarNome(nome) {
    return nome.trim();
}

export function calcularFrete(peso, distancia) {
    return peso * distancia * 0.1;
}

export function conectarBanco() {
    return { status: "conectado" };
}
```

Essas funções não pertencem ao mesmo assunto.

Versão melhor:

```js
// formatadores/formatarNome.js
export function formatarNome(nome) {
    return nome.trim();
}
```

```js
// frete/calcularFrete.js
export function calcularFrete(peso, distancia) {
    return peso * distancia * 0.1;
}
```

Cada arquivo tem uma intenção mais clara.

---

# 4 - Baixo acoplamento

Acoplamento é o quanto um módulo depende de detalhes de outro.

Exemplo com acoplamento forte:

```js
function finalizarPedido(pedido) {
    salvarNoBancoMySQL(pedido);
    enviarEmailSMTP(pedido.cliente.email);
    gerarPdfComBibliotecaX(pedido);
}
```

Essa função sabe detalhes demais.

Versão melhor:

```js
function finalizarPedido(pedido, pedidoRepository, notificacaoService, notaService) {
    pedidoRepository.salvar(pedido);
    notificacaoService.enviarConfirmacao(pedido);
    notaService.gerar(pedido);
}
```

Agora a função depende de comportamentos, não de detalhes internos.

Não precisa aplicar isso em todo código pequeno, mas é uma ideia importante para sistemas maiores.

---

# 5 - Coesão

Coesão é o quanto as partes de um módulo pertencem ao mesmo assunto.

Arquivo coeso:

```js
export function formatarMoeda(valor) {
    return valor.toLocaleString("pt-BR", {
        style: "currency",
        currency: "BRL"
    });
}

export function formatarPercentual(valor) {
    return `${valor}%`;
}
```

As duas funções tratam formatação.

Arquivo pouco coeso:

```js
export function formatarMoeda(valor) {}
export function autenticarUsuario(usuario) {}
export function calcularFrete(pedido) {}
```

Assuntos misturados dificultam manutenção.

---

# 6 - Organização por domínio

Em projetos maiores, organizar apenas por tipo técnico pode ficar limitado.

Exemplo por tipo:

```txt
components/
services/
utils/
types/
```

Exemplo por domínio:

```txt
features/
  produtos/
    produtosService.js
    ProdutoCard.jsx
    produtosUtils.js
  pedidos/
    pedidosService.js
    PedidoCard.jsx
    pedidosUtils.js
```

Organização por domínio aproxima arquivos que mudam pelo mesmo motivo.

Em projetos pequenos, uma estrutura simples por tipo pode ser suficiente. Em projetos maiores, domínio costuma escalar melhor.

---

# 7 - Exemplo prático

Estrutura simples:

```txt
src/
  services/
    produtosService.js
  utils/
    formatarMoeda.js
  pages/
    produtosPage.js
```

`produtosService.js`:

```js
export async function buscarProdutos() {
    const response = await fetch("/api/produtos");

    if (!response.ok) {
        throw new Error("Erro ao buscar produtos");
    }

    return response.json();
}
```

`formatarMoeda.js`:

```js
export function formatarMoeda(valor) {
    return valor.toLocaleString("pt-BR", {
        style: "currency",
        currency: "BRL"
    });
}
```

`produtosPage.js`:

```js
import { buscarProdutos } from "../services/produtosService.js";
import { formatarMoeda } from "../utils/formatarMoeda.js";

async function carregarProdutos() {
    const produtos = await buscarProdutos();

    produtos.forEach(function(produto) {
        console.log(`${produto.nome} - ${formatarMoeda(produto.preco)}`);
    });
}

carregarProdutos();
```

Cada módulo tem um papel claro.

---

# 8 - Erros comuns

### Criar pasta demais cedo demais

Arquitetura exagerada atrapalha projeto pequeno.

Comece simples e evolua quando houver necessidade real.

### Criar arquivo genérico demais

`utils.js`, `helpers.js` e `functions.js` tendem a virar depósito de funções sem relação.

Prefira nomes mais específicos.

### Misturar regra de negócio com detalhe de tela

Se uma regra importante fica presa dentro de um clique de botão, ela fica difícil de reutilizar e testar.

---

# 9 - Relação com outros estudos

Este conteúdo depende de ES6 Modules.

Também se conecta com funções, Fetch API, React, serviços, componentes e organização de projetos reais.

---

# 10 - Conclusão

Modularização moderna é sobre clareza de responsabilidade.

O objetivo não é criar muitas pastas, mas deixar o código fácil de entender, testar e evoluir. A melhor estrutura é a mais simples que suporta bem o tamanho e a complexidade atual do projeto.
