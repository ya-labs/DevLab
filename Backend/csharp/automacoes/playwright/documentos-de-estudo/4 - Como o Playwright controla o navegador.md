# Como o Playwright controla o navegador

## 1. Ideia principal

Playwright controla o navegador por codigo.

Em vez de uma pessoa usar mouse e teclado, o programa envia comandos para o navegador.

Exemplo:

```txt
Pessoa:
Abre o navegador, digita a URL, clica no campo e preenche.

Playwright:
Cria uma pagina, navega para a URL, localiza o campo e preenche.
```

O resultado visual pode ser parecido, mas a execucao acontece por comandos escritos em C#.

## 2. Fluxo basico

O fluxo basico do Playwright costuma seguir esta ordem:

```txt
Criar Playwright
Abrir navegador
Criar pagina
Acessar URL
Interagir com elementos
Fechar recursos
```

Em codigo:

```csharp
using Microsoft.Playwright;

using var playwright = await Playwright.CreateAsync();

await using var browser = await playwright.Chromium.LaunchAsync(new()
{
    Headless = false
});

var page = await browser.NewPageAsync();

await page.GotoAsync("https://example.com");
```

Esse e o ponto de partida de quase toda automacao.

## 3. Playwright

O objeto `playwright` e a entrada principal da biblioteca.

Ele e criado assim:

```csharp
using var playwright = await Playwright.CreateAsync();
```

Com ele, voce acessa os navegadores suportados:

```csharp
playwright.Chromium
playwright.Firefox
playwright.Webkit
```

Cada um representa um motor de navegador.

Na maioria dos estudos iniciais, voce pode comecar com Chromium.

## 4. Browser

O `browser` representa o navegador aberto.

Exemplo:

```csharp
await using var browser = await playwright.Chromium.LaunchAsync();
```

Quando voce chama `LaunchAsync`, o Playwright inicia um navegador.

Voce pode configurar esse navegador.

Exemplo:

```csharp
await using var browser = await playwright.Chromium.LaunchAsync(new()
{
    Headless = false,
    SlowMo = 100
});
```

`Headless = false` mostra o navegador na tela.

`SlowMo = 100` deixa as acoes mais lentas, ajudando a visualizar o fluxo durante o estudo.

## 5. Page

`Page` representa uma aba do navegador.

Exemplo:

```csharp
var page = await browser.NewPageAsync();
```

Com `page`, voce consegue:

- navegar para uma URL;
- clicar;
- preencher campos;
- ler textos;
- esperar elementos;
- tirar screenshots;
- avaliar JavaScript na pagina.

Exemplo:

```csharp
await page.GotoAsync("https://example.com");
```

A maior parte da automacao acontece a partir de `page`.

## 6. BrowserContext

`BrowserContext` representa um ambiente isolado dentro do navegador.

Pense nele como um perfil separado.

Cada contexto pode ter:

- cookies proprios;
- local storage proprio;
- sessao propria;
- configuracoes proprias;
- paginas proprias.

Exemplo:

```csharp
var context = await browser.NewContextAsync();
var page = await context.NewPageAsync();
```

Esse formato e melhor quando voce precisa controlar sessao, cookies ou autenticacao.

Em automacoes reais, `BrowserContext` costuma ser mais importante do que parece no inicio.

## 7. Locator

`Locator` e a forma recomendada de encontrar elementos na pagina.

Exemplo:

```csharp
var campoUsuario = page.GetByLabel("Usuario");

await campoUsuario.FillAsync("admin");
```

O locator nao e apenas uma busca simples.

Ele trabalha junto com o mecanismo de espera do Playwright.

Isso significa que o Playwright tenta encontrar o elemento no momento da acao e espera quando faz sentido.

Exemplo direto:

```csharp
await page.GetByRole(AriaRole.Button, new() { Name = "Entrar" }).ClickAsync();
```

Esse codigo procura um botao chamado `Entrar` e clica nele.

## 8. Como as acoes acontecem

Quando voce chama uma acao, como `ClickAsync`, o Playwright verifica se o elemento pode receber a acao.

Antes de clicar, ele pode verificar se o elemento esta:

- presente na pagina;
- visivel;
- estavel;
- habilitado;
- disponivel para interacao.

Isso evita varios erros comuns de automacao.

Exemplo:

```csharp
await page.GetByRole(AriaRole.Button, new() { Name = "Salvar" }).ClickAsync();
```

O Playwright nao simplesmente clica de qualquer jeito. Ele tenta garantir que o elemento esteja pronto para receber o clique.

## 9. Exemplo de preenchimento

Exemplo:

```csharp
await page.GetByLabel("Nome").FillAsync("Nicolas");
await page.GetByLabel("Email").FillAsync("nicolas@example.com");

await page.GetByRole(AriaRole.Button, new() { Name = "Salvar" }).ClickAsync();
```

Esse fluxo:

- encontra o campo pelo label `Nome`;
- preenche o nome;
- encontra o campo pelo label `Email`;
- preenche o email;
- encontra o botao `Salvar`;
- clica no botao.

Essa forma e mais legivel do que depender de seletores CSS complexos logo de inicio.

## 10. Quando usar CSS ou XPath

Em sistemas legados, nem sempre a tela possui bons labels, roles ou textos claros.

Nesses casos, pode ser necessario usar CSS ou XPath.

Exemplo com CSS:

```csharp
await page.Locator("#usuario").FillAsync("admin");
```

Exemplo com XPath:

```csharp
await page.Locator("xpath=//input[@name='usuario']").FillAsync("admin");
```

CSS e XPath devem ser usados com cuidado.

Eles podem ficar frageis se a estrutura HTML mudar.

Quando possivel, prefira locators baseados no que o usuario ve:

- `GetByRole`;
- `GetByLabel`;
- `GetByText`;
- `GetByPlaceholder`.

## 11. O que acontece no final

Quando o programa termina, os recursos precisam ser liberados.

Por isso aparece:

```csharp
using var playwright = await Playwright.CreateAsync();
await using var browser = await playwright.Chromium.LaunchAsync();
```

`using var` libera o objeto ao final do escopo.

`await using var` libera de forma assincrona.

Isso e importante porque o navegador representa recursos externos, como processo, conexoes e paginas abertas.

## 12. Boas praticas

Boas praticas para controlar o navegador:

- use `Headless = false` enquanto estiver aprendendo;
- use `SlowMo` quando precisar visualizar o fluxo;
- prefira `Locator` em vez de buscar elementos manualmente;
- escolha locators legiveis;
- use `BrowserContext` quando precisar controlar sessao;
- libere recursos com `using` e `await using`;
- evite esperas fixas sem necessidade;
- registre logs nas etapas importantes.

## 13. Conclusao

Playwright controla o navegador criando uma camada de automacao entre o codigo C# e a pagina web.

Os principais conceitos sao:

- `Playwright`: entrada da biblioteca;
- `Browser`: navegador aberto;
- `BrowserContext`: ambiente isolado;
- `Page`: aba ou pagina;
- `Locator`: forma de encontrar elementos.

Entender essa estrutura ajuda a escrever automacoes mais organizadas e menos confusas.

Fontes para estudo:

- https://playwright.dev/dotnet/docs/library
- https://playwright.dev/dotnet/docs/api/class-playwright
- https://playwright.dev/dotnet/docs/locators
