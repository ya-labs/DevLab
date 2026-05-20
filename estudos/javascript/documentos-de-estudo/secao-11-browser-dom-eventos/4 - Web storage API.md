## 1 - O que é a Web Storage API?

A Web Storage API permite salvar dados no navegador do usuário.

Ela é usada quando o front-end precisa guardar informações simples, como:

- Tema claro/escuro
- Token de login
- Preferências do usuário
- Dados temporários de formulário
- Carrinho de compras
- Configurações locais
etc.

Os dados ficam salvos em formato de texto, usando chave e valor.

Exemplo:

```js
localStorage.setItem('tema', 'escuro');
localStorage.getItem('tema'); // 'escuro'
```

Nesse caso:
```js
"tema" = chave
"escuro" = valor
```

---

## 2 - Tipos de Web Storage

``localStorage`` e ``sessionStorage``

A diferença é o tempo que o dado fica salvo.

### LocalStorage

Salva dados sem data de expiração.
Ou seja, mesmo que o usuário feche o navegador, desligue o computador ou reinicie a página,
os dados permanecem salvos.
Exemplo:

```js
localStorage.setItem('tema', 'escuro');
```

Para buscar:

```js
const tema = localStorage.getItem('tema');
console.log(tema); // 'escuro'
```

Resultado:
```js
'escuro'
```

### SessionStorage

O sessionStorage salva dados apenas enquanto a aba estiver aberta.
Se o usuário fechar a aba, os dados são apagados.

Exemplo:
```js
sessionStorage.setItem('paginaAtual', 'checkout');
``` 

Para buscar:

```js
const paginaAtual = sessionStorage.getItem('paginaAtual');
console.log(paginaAtual); // 'checkout'
```

Resultado:
```js
'checkout'
```
---
## 3 - Principais métodos

Salvar dados:
```js
localStorage.setItem('chave', 'valor');
```

Buscar dados:
```js
localStorage.getItem('chave');
```

Remover dados:
```js
localStorage.removeItem('chave');
```

Limpar todos os dados:
```js
localStorage.clear();
```

Pegar uma chave pela posição:
```js
localStorage.key(0); // retorna a chave na posição 0
```
---
## 4 - Trabalhando com objetos

A Web Storage API só aceita strings.
Então, se tentarmos salvar um objeto, será convertido para string e retornará ``"[object Object]".``

Errado:
```js
const usuario = {
    nome: 'João',
    idade: 30
};

localStorage.setItem('usuario', usuario);
```
Resultado:
```js
'[object Object]'
```

O correto é usar ``JSON.stringify()`` para converter o objeto em string corretamente:

```js
const usuario = {
    nome: 'João',
    idade: 30
};

localStorage.setItem('usuario', JSON.stringify(usuario));
```

Para recuperar o objeto, usamos ``JSON.parse()``:

```js
const usuarioString = localStorage.getItem('usuario');
const usuario = JSON.parse(usuarioString);
console.log(usuario); 
```
Resultado:
```js
{ nome: 'João', idade: 30 }
```
### E a mesma coisa funciona para Arrays:
```js
const frutas = ['maçã', 'banana', 'laranja'];
localStorage.setItem('frutas', JSON.stringify(frutas));
```
Para recuperar:
```js
const frutasString = localStorage.getItem('frutas');
const frutas = JSON.parse(frutasString);
console.log(frutas); 
```
Resultado:
```js
['maçã', 'banana', 'laranja']
```
---
## 5 - Observação de segurança

Não se deve usar Web Storage para guardar informações muito sensíveis.
Evite salvar:
- senhas
- dados bancários
- documentos pessoais
- informações privadas importantes

O ``localStorage`` pode ser acessado pelo JavaScript da página. Então, se o site tiver
uma falha de segurança como [XSS](2%20-%20DOM.md#innerhtml), esses dados podem ser roubados.

Também é bom lembrar que o Web Storage tem um limite de armazenamento (geralmente cerca de 5MB por domínio).
Se tentar salvar mais do que isso, pode ocorrer um erro.