# O que e Playwright com CSharp

## 1. O que e

Playwright e uma ferramenta de automacao de navegador criada pela Microsoft.

Com ela, voce consegue controlar um navegador por codigo, como se uma pessoa estivesse usando a tela.

Na pratica, o codigo pode:

- abrir um site;
- acessar uma pagina;
- clicar em botoes;
- preencher campos;
- selecionar opcoes;
- enviar formularios;
- esperar elementos aparecerem;
- capturar textos da tela;
- tirar prints;
- baixar arquivos;
- ler informacoes da pagina.

O Playwright e muito conhecido por testes automatizados de ponta a ponta, tambem chamados de testes E2E. Mas ele nao serve apenas para testes.

Ele tambem pode ser usado para automacoes reais, principalmente quando um sistema antigo nao possui API e a unica forma de inserir ou consultar informacoes e pela interface web.

Exemplo de uso real:

```txt
Sistema legado nao possui API.
Usuario precisa cadastrar varios dados manualmente.
Automacao abre o navegador.
Automacao faz login.
Automacao preenche os campos.
Automacao envia o formulario.
Automacao registra se deu certo ou erro.
```

Nesse caso, o Playwright funciona como uma ponte entre o seu codigo C# e um sistema web que so pode ser operado pela tela.

## 2. Por que usar com CSharp

O Playwright pode ser usado com varias linguagens, como JavaScript, TypeScript, Python, Java e C#.

Usar Playwright com C# faz sentido quando o projeto ou a empresa ja usa o ecossistema .NET.

Isso permite integrar a automacao com:

- aplicacoes console;
- Workers;
- APIs ASP.NET;
- servicos em background;
- logs do .NET;
- configuracoes em `appsettings.json`;
- banco de dados;
- filas;
- tarefas agendadas;
- sistemas internos.

Por exemplo, voce pode ter uma aplicacao C# que busca dados em um banco e usa Playwright para preencher esses dados em um sistema legado.

Fluxo:

```txt
Aplicacao C# busca dados
Playwright abre o sistema legado
Playwright preenche a tela
Sistema legado salva os dados
Aplicacao C# registra log da execucao
```

O ponto importante e que o Playwright nao substitui uma API. Ele automatiza a interface quando a API nao existe ou nao esta disponivel.

## 3. Playwright e teste automatizado

O uso mais comum do Playwright e criar testes automatizados.

Um teste automatizado verifica se uma aplicacao esta funcionando como esperado.

Exemplo:

```txt
Abrir pagina de login
Preencher usuario e senha
Clicar em entrar
Verificar se a pagina inicial apareceu
```

Esse tipo de teste simula o comportamento de um usuario real.

Em C#, o Playwright pode ser usado com frameworks de teste como:

- NUnit;
- xUnit;
- MSTest.

Mas essa nao e a unica forma de usar Playwright.

Para automacoes de producao, voce pode usar o pacote `Microsoft.Playwright` diretamente em um projeto console, Worker ou outro tipo de aplicacao .NET.

## 4. Playwright como automacao de navegador

No contexto deste estudo, o foco principal nao e teste automatizado.

O foco e:

```txt
Playwright com C# para automacao de navegador em sistemas reais.
```

Isso e util quando:

- o sistema nao oferece API;
- o sistema e legado;
- a integracao precisa acontecer pela tela;
- tarefas manuais sao repetitivas;
- o processo precisa gerar evidencias;
- a automacao precisa preencher dados em massa;
- a empresa nao pode alterar o sistema original.

Exemplo simples:

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

Esse codigo:

- cria uma instancia do Playwright;
- abre o Chromium;
- cria uma nova pagina;
- acessa um endereco.

A partir disso, voce pode interagir com a pagina usando codigo.

## 5. Principais partes do Playwright

Ao estudar Playwright com C#, alguns conceitos aparecem o tempo todo.

### Playwright

Representa a entrada principal da biblioteca.

E a partir dele que voce acessa os navegadores:

```csharp
using var playwright = await Playwright.CreateAsync();
```

### Browser

Representa o navegador aberto.

Exemplo:

```csharp
await using var browser = await playwright.Chromium.LaunchAsync();
```

O navegador pode ser Chromium, Firefox ou WebKit.

### BrowserContext

Representa um contexto isolado dentro do navegador.

Pense nele como um perfil separado do navegador, com seus proprios cookies, sessoes e armazenamento.

Isso e importante quando voce precisa controlar login, sessao e isolamento entre execucoes.

### Page

Representa uma aba ou pagina do navegador.

Exemplo:

```csharp
var page = await browser.NewPageAsync();
```

E nela que voce navega, clica, preenche campos e captura informacoes.

### Locator

Representa uma forma de encontrar um elemento na tela.

Exemplo:

```csharp
await page.GetByLabel("Usuario").FillAsync("admin");
```

O locator e um dos conceitos mais importantes do Playwright, porque toda automacao depende de encontrar elementos corretamente.

## 6. Onde isso aparece em codigo real

Em uma automacao real, voce normalmente cria um fluxo parecido com este:

```csharp
using Microsoft.Playwright;

using var playwright = await Playwright.CreateAsync();

await using var browser = await playwright.Chromium.LaunchAsync(new()
{
    Headless = false
});

var page = await browser.NewPageAsync();

await page.GotoAsync("https://sistema-legado.com/login");

await page.GetByLabel("Usuario").FillAsync("meu_usuario");
await page.GetByLabel("Senha").FillAsync("minha_senha");
await page.GetByRole(AriaRole.Button, new() { Name = "Entrar" }).ClickAsync();
```

Esse exemplo mostra a ideia central:

- abrir navegador;
- acessar uma pagina;
- localizar campos;
- preencher dados;
- clicar em um botao.

Em um sistema real, voce tambem precisaria tratar erros, registrar logs, proteger credenciais e validar se a acao foi concluida.

## 7. Boas praticas iniciais

Algumas boas praticas desde o comeco:

- evite deixar usuario e senha direto no codigo;
- prefira locators claros, como `GetByRole`, `GetByLabel` e `GetByText`;
- evite depender de tempo fixo sempre que possivel;
- registre logs das etapas principais;
- tire screenshot quando houver erro;
- separe o codigo em classes quando o fluxo crescer;
- trate falhas de carregamento e elementos que nao aparecem;
- documente o que a automacao faz e quais riscos existem.

Automacao de navegador e poderosa, mas tambem e sensivel. Se a tela do sistema mudar, a automacao pode quebrar.

## 8. Conclusao

Playwright com C# permite controlar navegadores por codigo.

Ele e muito usado para testes E2E, mas tambem pode ser usado em automacoes reais, especialmente quando um sistema legado nao possui API.

Neste estudo, o foco sera usar Playwright como ferramenta de automacao de navegador dentro do ecossistema .NET.

Antes de avancar, e importante entender bem estes conceitos:

- Playwright cria a automacao;
- Browser representa o navegador;
- Page representa a aba;
- Locator encontra elementos;
- C# organiza a regra da automacao.

Fonte principal para estudo:

- https://playwright.dev/dotnet/
- https://playwright.dev/dotnet/docs/library
