# Seletores e locators

## 1. O que sao seletores

Seletores sao formas de encontrar elementos dentro de uma pagina.

Em uma automacao com Playwright, quase toda acao depende de encontrar algum elemento primeiro.

Exemplos:

```txt
Encontrar campo de usuario
Encontrar campo de senha
Encontrar botao Entrar
Encontrar mensagem de sucesso
Encontrar link Clientes
Encontrar linha de uma tabela
```

Depois que o elemento e encontrado, o Playwright consegue interagir com ele.

Exemplo:

```csharp
await page.GetByLabel("Usuario").FillAsync("admin");
```

Nesse caso, o Playwright procura um campo associado ao label `Usuario` e preenche com o texto `admin`.

## 2. O que e locator

`Locator` e a forma recomendada pelo Playwright para encontrar e interagir com elementos.

Ele representa uma busca por um elemento da pagina.

Exemplo:

```csharp
var campoUsuario = page.GetByLabel("Usuario");

await campoUsuario.FillAsync("admin");
```

O locator nao precisa encontrar o elemento imediatamente no momento em que a variavel e criada.

O Playwright resolve o locator no momento da acao.

Exemplo:

```csharp
await campoUsuario.FillAsync("admin");
```

Aqui ele tenta localizar o campo e preencher.

Isso ajuda em paginas que demoram um pouco para carregar.

## 3. Por que locators sao importantes

Uma automacao depende da estabilidade dos locators.

Se voce escolhe um locator ruim, a automacao fica fragil.

Exemplo fragil:

```csharp
await page.Locator("div > form > div:nth-child(2) > input").FillAsync("admin");
```

Esse seletor depende muito da estrutura do HTML.

Se alguem colocar uma `div` nova no formulario, a automacao pode quebrar.

Exemplo melhor:

```csharp
await page.GetByLabel("Usuario").FillAsync("admin");
```

Esse locator usa algo que faz sentido para o usuario: o texto do label.

## 4. GetByRole

`GetByRole` encontra elementos pelo papel de acessibilidade.

Exemplo:

```csharp
await page.GetByRole(AriaRole.Button, new() { Name = "Entrar" }).ClickAsync();
```

Esse codigo procura um botao chamado `Entrar`.

Ele e muito util para:

- botoes;
- links;
- caixas de texto;
- titulos;
- checkboxes;
- menus;
- opcoes.

Exemplo com link:

```csharp
await page.GetByRole(AriaRole.Link, new() { Name = "Clientes" }).ClickAsync();
```

Esse tipo de locator costuma ser mais proximo da forma como o usuario enxerga a tela.

## 5. GetByLabel

`GetByLabel` encontra campos pelo texto do label.

Exemplo:

```csharp
await page.GetByLabel("Nome").FillAsync("Nicolas");
```

Esse codigo procura um campo associado ao label `Nome`.

E muito usado em formularios.

Exemplo:

```csharp
await page.GetByLabel("Email").FillAsync("nicolas@example.com");
await page.GetByLabel("Senha").FillAsync("123456");
```

Esse formato e simples e legivel.

Em sistemas bem construidos, `GetByLabel` costuma funcionar muito bem.

## 6. GetByText

`GetByText` encontra elementos pelo texto visivel.

Exemplo:

```csharp
await page.GetByText("Cadastro realizado com sucesso").WaitForAsync();
```

Esse locator e util para validar mensagens.

Exemplos:

```csharp
await page.GetByText("Erro ao salvar").WaitForAsync();
await page.GetByText("Cliente cadastrado").WaitForAsync();
await page.GetByText("Nenhum registro encontrado").WaitForAsync();
```

Use `GetByText` principalmente quando voce quer confirmar que uma informacao apareceu na tela.

## 7. GetByPlaceholder

`GetByPlaceholder` encontra campos pelo placeholder.

Exemplo:

```csharp
await page.GetByPlaceholder("Digite seu usuario").FillAsync("admin");
```

Ele pode ser util quando o sistema nao tem label claro.

Mas existe um cuidado: placeholder nao substitui label.

Se o texto do placeholder mudar, a automacao pode quebrar.

Use quando nao houver uma opcao melhor.

## 8. Locator com CSS

Tambem e possivel usar seletores CSS.

Exemplo:

```csharp
await page.Locator("#usuario").FillAsync("admin");
```

Esse codigo procura um elemento com `id="usuario"`.

Outros exemplos:

```csharp
await page.Locator(".botao-salvar").ClickAsync();
await page.Locator("input[name='cpf']").FillAsync("00000000000");
await page.Locator("table tbody tr").CountAsync();
```

CSS e util quando:

- o sistema nao tem bons labels;
- os elementos possuem `id`;
- os elementos possuem `name`;
- a tela e antiga;
- os textos visiveis nao sao confiaveis.

## 9. Locator com XPath

XPath tambem pode ser usado.

Exemplo:

```csharp
await page.Locator("xpath=//input[@name='usuario']").FillAsync("admin");
```

XPath costuma aparecer em sistemas legados porque as telas nem sempre possuem boa estrutura.

Mas ele deve ser usado com cuidado.

XPath muito longo pode ficar fragil.

Exemplo fragil:

```csharp
await page.Locator("xpath=/html/body/div[2]/div[1]/form/table/tbody/tr[3]/td[2]/input").FillAsync("admin");
```

Esse locator depende demais da posicao do elemento.

Se a tela mudar um pouco, ele quebra.

## 10. Filtrando elementos

Quando existem varios elementos parecidos, voce pode filtrar.

Exemplo:

```csharp
var linhaCliente = page.Locator("tr").Filter(new()
{
    HasText = "Nicolas"
});

await linhaCliente.GetByRole(AriaRole.Button, new() { Name = "Editar" }).ClickAsync();
```

Esse exemplo:

- procura linhas da tabela;
- filtra a linha que contem `Nicolas`;
- clica no botao `Editar` dentro dessa linha.

Esse tipo de fluxo e muito comum em sistemas com tabelas.

## 11. Quando usar cada tipo

Ordem recomendada:

```txt
1. GetByRole
2. GetByLabel
3. GetByText
4. GetByPlaceholder
5. CSS
6. XPath
```

Essa ordem nao e uma regra absoluta.

Ela serve como guia.

Em sistemas legados, voce muitas vezes vai precisar usar CSS ou XPath. O importante e escolher o locator menos fragil possivel.

## 12. Boas praticas

Boas praticas para locators:

- prefira elementos com significado para o usuario;
- use `GetByRole` para botoes e links;
- use `GetByLabel` para campos;
- use `GetByText` para mensagens;
- evite seletores longos demais;
- evite depender de posicao visual;
- prefira `id` e `name` quando forem estaveis;
- isole locators importantes em metodos ou classes;
- teste o locator antes de usar em massa;
- documente casos frageis.

## 13. Conclusao

Locators sao uma das partes mais importantes do Playwright.

Uma automacao confiavel depende de bons locators.

Se o locator for claro e estavel, o codigo fica mais simples de entender e mais facil de manter.

Em sistemas modernos, prefira locators baseados em acessibilidade e texto.

Em sistemas legados, use CSS e XPath quando necessario, mas com cuidado para nao criar automacoes frageis demais.

Fontes para estudo:

- https://playwright.dev/dotnet/docs/locators
- https://playwright.dev/dotnet/docs/api/class-locator
