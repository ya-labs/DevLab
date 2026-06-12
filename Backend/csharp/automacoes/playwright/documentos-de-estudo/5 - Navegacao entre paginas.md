# Navegacao entre paginas

## 1. O que e navegacao

Navegacao e o processo de mudar a pagina atual do navegador.

Em uma automacao com Playwright, isso pode acontecer quando:

- voce acessa uma URL diretamente;
- clica em um link;
- envia um formulario;
- faz login;
- e redirecionado para outra tela;
- abre uma nova aba;
- volta para uma pagina anterior.

Exemplo simples:

```csharp
await page.GotoAsync("https://example.com");
```

Esse comando manda a pagina acessar uma URL.

## 2. Por que navegacao e importante

Muitas automacoes quebram porque o codigo tenta interagir com a tela antes de ela estar pronta.

Exemplo de problema:

```txt
Automacao clica em Entrar.
Sistema demora para carregar a proxima pagina.
Codigo tenta clicar em Cadastro.
O botao Cadastro ainda nao apareceu.
Automacao falha.
```

Por isso, entender navegacao e carregamento e essencial.

Em sistemas legados, isso e ainda mais importante, porque as telas podem ser lentas, ter redirecionamentos ou carregar partes da pagina aos poucos.

## 3. Acessando uma URL

O jeito mais direto de navegar e usar `GotoAsync`.

Exemplo:

```csharp
await page.GotoAsync("https://example.com");
```

Depois disso, voce pode interagir com a pagina.

Exemplo:

```csharp
await page.GotoAsync("https://example.com");

var titulo = await page.TitleAsync();

Console.WriteLine(titulo);
```

Esse codigo:

- acessa a pagina;
- pega o titulo;
- imprime no console.

## 4. Navegando apos login

Um caso comum e fazer login e esperar a proxima pagina.

Exemplo:

```csharp
await page.GotoAsync("https://sistema-legado.com/login");

await page.GetByLabel("Usuario").FillAsync("admin");
await page.GetByLabel("Senha").FillAsync("senha");

await page.GetByRole(AriaRole.Button, new() { Name = "Entrar" }).ClickAsync();

await page.GetByText("Pagina inicial").WaitForAsync();
```

Esse exemplo:

- acessa a tela de login;
- preenche usuario;
- preenche senha;
- clica em entrar;
- espera um texto da pagina inicial aparecer.

O ultimo passo e importante.

Ele confirma que a navegacao terminou e que a pagina esperada apareceu.

## 5. Esperar a URL mudar

Outra forma de confirmar a navegacao e esperar a URL.

Exemplo:

```csharp
await page.GetByRole(AriaRole.Button, new() { Name = "Entrar" }).ClickAsync();

await page.WaitForURLAsync("**/home");
```

Esse codigo espera a URL terminar com `/home`.

Isso ajuda quando o sistema redireciona depois de uma acao.

Exemplo de fluxo:

```txt
/login
clicou em Entrar
/home
```

Se a URL nao mudar, pode ser sinal de erro no login ou falha de carregamento.

## 6. Navegando por links e botoes

Nem toda navegacao usa `GotoAsync`.

Muitas vezes voce navega clicando em links ou botoes.

Exemplo:

```csharp
await page.GetByRole(AriaRole.Link, new() { Name = "Clientes" }).ClickAsync();
```

Depois do clique, voce pode esperar um elemento da proxima pagina:

```csharp
await page.GetByRole(AriaRole.Heading, new() { Name = "Clientes" }).WaitForAsync();
```

Esse formato e bom porque espera algo concreto da tela.

## 7. Esperar elemento em vez de esperar tempo fixo

Uma pratica ruim e depender sempre de tempo fixo.

Exemplo ruim:

```csharp
await page.WaitForTimeoutAsync(5000);
```

Esse codigo espera 5 segundos, mesmo que a tela carregue em 1 segundo.

E tambem pode falhar se a tela demorar 6 segundos.

Melhor:

```csharp
await page.GetByText("Cadastro realizado com sucesso").WaitForAsync();
```

Nesse caso, a automacao espera uma condicao real da tela.

O ponto importante e:

```txt
Espere por algo que indique que a pagina esta pronta.
```

## 8. Navegacao com sistemas lentos

Sistemas legados podem ser lentos por varios motivos:

- servidor antigo;
- banco pesado;
- tela com muito JavaScript;
- rede instavel;
- paginas com frames;
- redirecionamentos;
- sessoes expiradas;
- modais inesperados.

Por isso, a automacao precisa confirmar cada etapa.

Exemplo:

```csharp
await page.GetByRole(AriaRole.Link, new() { Name = "Novo cliente" }).ClickAsync();

await page.GetByLabel("Nome").WaitForAsync();
```

Aqui a automacao nao assume que a tela abriu. Ela espera o campo `Nome` aparecer.

## 9. Capturando a URL atual

Em alguns momentos, pode ser util verificar onde a automacao esta.

Exemplo:

```csharp
Console.WriteLine(page.Url);
```

Isso pode ajudar em logs.

Exemplo:

```csharp
Console.WriteLine($"Pagina atual: {page.Url}");
```

Em uma automacao real, registrar a URL atual pode ajudar a entender onde o fluxo quebrou.

## 10. Lidando com nova aba

Alguns sistemas abrem relatorios, comprovantes ou documentos em uma nova aba.

Nesses casos, voce precisa capturar a nova pagina.

Exemplo:

```csharp
var novaPaginaTask = page.Context.WaitForPageAsync();

await page.GetByRole(AriaRole.Link, new() { Name = "Abrir relatorio" }).ClickAsync();

var novaPagina = await novaPaginaTask;

await novaPagina.WaitForLoadStateAsync();
```

Esse fluxo:

- prepara a espera por uma nova pagina;
- clica no link;
- captura a nova aba;
- espera o carregamento.

Esse tipo de caso aparece bastante em sistemas antigos.

## 11. Exemplo completo

Exemplo de navegacao em um fluxo simples:

```csharp
using Microsoft.Playwright;

using var playwright = await Playwright.CreateAsync();

await using var browser = await playwright.Chromium.LaunchAsync(new()
{
    Headless = false
});

var page = await browser.NewPageAsync();

await page.GotoAsync("https://sistema-legado.com/login");

await page.GetByLabel("Usuario").FillAsync("admin");
await page.GetByLabel("Senha").FillAsync("senha");
await page.GetByRole(AriaRole.Button, new() { Name = "Entrar" }).ClickAsync();

await page.WaitForURLAsync("**/home");

await page.GetByRole(AriaRole.Link, new() { Name = "Clientes" }).ClickAsync();

await page.GetByRole(AriaRole.Heading, new() { Name = "Clientes" }).WaitForAsync();

Console.WriteLine($"Pagina atual: {page.Url}");
```

Esse exemplo mostra:

- login;
- redirecionamento;
- navegacao para outra tela;
- espera por elemento;
- log da URL atual.

## 12. Boas praticas

Boas praticas para navegacao:

- use `GotoAsync` para acessar uma URL direta;
- espere a proxima tela antes de continuar;
- prefira esperar elementos reais da pagina;
- use `WaitForURLAsync` quando a mudanca de URL for importante;
- evite `WaitForTimeoutAsync` como solucao principal;
- registre a URL atual em caso de erro;
- trate cenarios de sessao expirada;
- fique atento a novas abas;
- valide se a pagina esperada realmente abriu.

## 13. Conclusao

Navegacao e uma das partes mais importantes de uma automacao com Playwright.

Nao basta clicar e assumir que a proxima tela esta pronta.

Uma automacao confiavel precisa esperar sinais reais:

- URL esperada;
- texto esperado;
- campo visivel;
- botao disponivel;
- titulo da pagina;
- mensagem de sucesso.

Em sistemas legados, esse cuidado evita muitos erros intermitentes.

Fontes para estudo:

- https://playwright.dev/dotnet/docs/navigations
- https://playwright.dev/dotnet/docs/actionability
- https://playwright.dev/dotnet/docs/locators
