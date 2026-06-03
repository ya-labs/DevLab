# Classes em JavaScript

Classes são uma sintaxe moderna para criar objetos com propriedades e métodos compartilhados.

Elas foram adicionadas no ES6 e deixam o código mais organizado quando precisamos representar entidades com comportamento.

---

# 1 - O que é uma classe

Uma classe funciona como um molde para criar objetos.

```js
class Pessoa {
    constructor(nome, idade) {
        this.nome = nome;
        this.idade = idade;
    }

    falar() {
        return `Olá, meu nome é ${this.nome}`;
    }
}

const pessoa = new Pessoa("Nícolas", 20);

console.log(pessoa.falar());
```

Nesse exemplo:

- `class Pessoa` define o molde;
- `constructor` inicializa os dados;
- `new Pessoa(...)` cria uma instância;
- `falar` é um método compartilhado no prototype.

---

# 2 - Classes e prototype

Mesmo usando `class`, JavaScript continua baseado em prototype.

```js
class Animal {
    falar() {
        return "Som genérico";
    }
}

console.log(Animal.prototype.falar);
```

Métodos definidos dentro da classe ficam em `Classe.prototype`.

Esse assunto se conecta com `Frontend/estudos/javascript/documentos-de-estudo/secao-09-orientacao-objetos/1 - Prototype.md`.

---

# 3 - Constructor

O `constructor` executa automaticamente quando uma instância é criada.

```js
class Produto {
    constructor(nome, preco) {
        this.nome = nome;
        this.preco = preco;
    }
}

const produto = new Produto("Arroz", 20);
```

Use o `constructor` para receber os dados necessários para iniciar o objeto.

---

# 4 - Métodos

Métodos representam comportamentos da classe.

```js
class Carrinho {
    constructor(itens) {
        this.itens = itens;
    }

    calcularTotal() {
        return this.itens.reduce(function(total, item) {
            return total + item.preco;
        }, 0);
    }
}

const carrinho = new Carrinho([
    { nome: "Arroz", preco: 20 },
    { nome: "Feijão", preco: 12 }
]);

console.log(carrinho.calcularTotal()); // 32
```

O método usa `this.itens` para acessar os dados da instância.

---

# 5 - Herança com extends

`extends` permite criar uma classe baseada em outra.

```js
class Usuario {
    constructor(nome) {
        this.nome = nome;
    }

    identificar() {
        return this.nome;
    }
}

class Administrador extends Usuario {
    podeExcluirUsuarios() {
        return true;
    }
}

const admin = new Administrador("Nícolas");

console.log(admin.identificar());
console.log(admin.podeExcluirUsuarios());
```

Use herança com cuidado. Em muitos projetos modernos, composição costuma ser mais simples do que criar hierarquias grandes.

---

# 6 - Campos privados

JavaScript moderno permite campos privados usando `#`.

```js
class Conta {
    #saldo;

    constructor(saldoInicial) {
        this.#saldo = saldoInicial;
    }

    consultarSaldo() {
        return this.#saldo;
    }
}

const conta = new Conta(100);

console.log(conta.consultarSaldo()); // 100
```

Campos privados ajudam a proteger detalhes internos da classe.

---

# 7 - Quando usar classes

Classes fazem sentido quando existe:

- uma entidade com estado próprio;
- comportamento relacionado a esse estado;
- necessidade de criar várias instâncias;
- regra que fica mais clara agrupada em um objeto.

Exemplos:

- `Carrinho`;
- `Pedido`;
- `Cliente`;
- `ValidadorFormulario`;
- `ServicoAutenticacao`.

Para objetos simples de dados, objeto literal geralmente basta.

---

# 8 - Erros comuns

### Usar classe para qualquer coisa

```js
class Formatador {
    formatarNome(nome) {
        return nome.trim();
    }
}
```

Se não existe estado, uma função simples pode ser melhor.

```js
function formatarNome(nome) {
    return nome.trim();
}
```

### Perder contexto do this

```js
const metodo = carrinho.calcularTotal;

metodo(); // pode perder o this
```

Esse problema é aprofundado em `Frontend/estudos/javascript/documentos-de-estudo/secao-09-orientacao-objetos/3 - this, bind, call e apply.md`.

### Criar herança profunda demais

Hierarquias grandes dificultam manutenção.

Prefira estruturas simples.

---

# 9 - Relação com outros estudos

Classes dependem de objetos, funções, prototype e `this`.

Antes de usar classes em projeto real, vale entender que elas organizam comportamento, mas não substituem a necessidade de pensar em responsabilidade clara.

---

# 10 - Conclusão

Classes são úteis quando ajudam a representar entidades com estado e comportamento.

No JavaScript moderno, elas são uma forma mais legível de usar o sistema de protótipos, mas devem ser usadas com critério. Para dados simples ou funções utilitárias, soluções mais simples costumam ser melhores.
