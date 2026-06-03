# Prototype em JavaScript

JavaScript usa protótipos para compartilhar propriedades e métodos entre objetos.

Mesmo quando usamos `class`, por baixo dos panos o JavaScript continua trabalhando com prototype.

---

# 1 - O que é prototype

Prototype é um objeto usado como base para outros objetos.

Quando você tenta acessar uma propriedade ou método, o JavaScript procura primeiro no próprio objeto. Se não encontrar, ele procura no protótipo. Esse caminho é chamado de prototype chain.

Exemplo:

```js
const pessoa = {
    nome: "Nícolas"
};

console.log(pessoa.toString());
```

`toString` não foi criado dentro de `pessoa`, mas funciona porque foi encontrado em `Object.prototype`.

---

# 2 - [[Prototype]], __proto__ e .prototype

Todo objeto possui uma ligação interna chamada `[[Prototype]]`.

Em estudos, às vezes vemos `__proto__` para visualizar essa ligação.

```js
const obj = {};

console.log(obj.__proto__ === Object.prototype); // true
```

Mas no código real, evite manipular `__proto__` diretamente.

Já `.prototype` é uma propriedade de funções construtoras.

```js
function Pessoa(nome) {
    this.nome = nome;
}

Pessoa.prototype.falar = function() {
    return `Olá, eu sou ${this.nome}`;
};

const pessoa = new Pessoa("Nícolas");

console.log(pessoa.falar());
```

Resumo:

- `obj.__proto__`: protótipo de um objeto;
- `Funcao.prototype`: objeto que será usado como protótipo das instâncias criadas com `new`.

---

# 3 - Como a prototype chain funciona

```js
function Usuario(nome) {
    this.nome = nome;
}

Usuario.prototype.saudacao = function() {
    return `Olá, ${this.nome}`;
};

const usuario = new Usuario("Nícolas");

console.log(usuario.saudacao());
```

Busca do JavaScript:

1. procura `saudacao` em `usuario`;
2. não encontra;
3. procura em `Usuario.prototype`;
4. encontra e executa.

Esse mecanismo permite compartilhar métodos sem duplicar a função em cada objeto.

---

# 4 - O que o new faz

Quando usamos `new`, o JavaScript faz alguns passos internamente.

```js
function Produto(nome) {
    this.nome = nome;
}

const produto = new Produto("Arroz");
```

De forma simplificada:

1. cria um objeto vazio;
2. liga esse objeto a `Produto.prototype`;
3. executa `Produto` com `this` apontando para o novo objeto;
4. retorna o objeto criado.

---

# 5 - Por que prototype existe

Prototype evita duplicação de métodos.

Exemplo ruim:

```js
function criarUsuario(nome) {
    return {
        nome,
        falar: function() {
            return `Olá, ${nome}`;
        }
    };
}
```

Cada usuário criado recebe uma nova função `falar`.

Com prototype:

```js
function Usuario(nome) {
    this.nome = nome;
}

Usuario.prototype.falar = function() {
    return `Olá, ${this.nome}`;
};
```

Agora o método fica compartilhado.

---

# 6 - Relação com classes

Classes são uma sintaxe mais moderna e organizada para trabalhar com esse mesmo mecanismo.

```js
class Usuario {
    constructor(nome) {
        this.nome = nome;
    }

    falar() {
        return `Olá, ${this.nome}`;
    }
}
```

O método `falar` vai para `Usuario.prototype`.

Por isso, estudar prototype ajuda a entender o que classes realmente fazem.

---

# 7 - Erros comuns

### Achar que class eliminou prototype

Classes em JavaScript continuam usando prototype internamente.

### Alterar prototypes nativos sem necessidade

```js
Array.prototype.meuMetodo = function() {};
```

Isso pode causar conflitos e comportamentos inesperados.

### Confundir `__proto__` com `.prototype`

`__proto__` é ligação de objeto. `.prototype` é propriedade de função construtora.

---

# 8 - Relação com outros estudos

Prototype se conecta com objetos, funções, classes e `this`.

Antes de estudar classes, vale entender pelo menos a ideia de prototype chain.

---

# 9 - Conclusão

Prototype é o mecanismo central de compartilhamento e herança em JavaScript.

Mesmo que no código moderno você use mais `class`, entender prototype ajuda a compreender melhor objetos, métodos, instâncias e o comportamento real da linguagem.
