# Instalacao e estrutura inicial do projeto

## 1. O que este documento explica

Este documento explica como iniciar um projeto C# usando Playwright como biblioteca de automacao de navegador.

O foco aqui nao e criar um projeto de teste com NUnit, xUnit ou MSTest.

O foco e criar uma base para automacao real, usando um projeto console ou uma estrutura parecida.

Exemplo de uso:

```txt
Aplicacao C# inicia
Playwright abre navegador
Automacao acessa sistema legado
Automacao executa um fluxo
Aplicacao finaliza e registra resultado
```

Esse formato e simples para estudar e tambem serve como base para evoluir depois para Worker, agendamento ou servico.

## 2. Pre-requisitos

Antes de usar Playwright com C#, voce precisa ter:

- .NET SDK instalado;
- um editor, como Visual Studio ou VS Code;
- terminal funcionando;
- acesso a internet para instalar pacotes e navegadores;
- conhecimento basico de `async` e `await`;
- conhecimento basico de projetos C#.

Tambem e importante entender que o Playwright baixa navegadores controlados por ele.

Isso significa que instalar o pacote NuGet nao e sempre suficiente. Depois de instalar o pacote, normalmente voce tambem precisa instalar os navegadores.

## 3. Criando um projeto console

Um projeto console e um bom ponto de partida para estudar Playwright.

Comando:

```bash
dotnet new console -n PlaywrightAutomacao
```

Depois entre na pasta:

```bash
cd PlaywrightAutomacao
```

Esse projeto cria uma aplicacao simples com um arquivo `Program.cs`.

Para estudos iniciais, isso e suficiente.

## 4. Instalando o pacote do Playwright

Para usar Playwright como biblioteca, instale o pacote:

```bash
dotnet add package Microsoft.Playwright
```

Esse pacote permite criar o Playwright pelo C# e controlar navegadores.

Depois, rode:

```bash
dotnet build
```

O build e importante porque ele gera arquivos usados pelo Playwright, incluindo o script de instalacao dos navegadores.

## 5. Instalando os navegadores

Depois do build, instale os navegadores.

O comando geralmente segue este formato:

```bash
pwsh bin/Debug/net8.0/playwright.ps1 install
```

O trecho `net8.0` pode mudar conforme a versao do seu projeto.

Exemplos:

```txt
net8.0
net9.0
net10.0
```

Se o seu projeto estiver em `net9.0`, o caminho pode ser:

```bash
pwsh bin/Debug/net9.0/playwright.ps1 install
```

Esse comando baixa os navegadores usados pelo Playwright.

## 6. Primeiro codigo

Exemplo simples no `Program.cs`:

```csharp
using Microsoft.Playwright;

using var playwright = await Playwright.CreateAsync();

await using var browser = await playwright.Chromium.LaunchAsync(new()
{
    Headless = false
});

var page = await browser.NewPageAsync();

await page.GotoAsync("https://example.com");

Console.WriteLine(await page.TitleAsync());
```

Esse codigo:

- cria o Playwright;
- abre o Chromium;
- deixa o navegador visivel com `Headless = false`;
- cria uma nova pagina;
- acessa `https://example.com`;
- imprime o titulo da pagina.

## 7. O que e Headless

`Headless` define se o navegador aparece visualmente ou roda em segundo plano.

Com `Headless = false`:

```csharp
await playwright.Chromium.LaunchAsync(new()
{
    Headless = false
});
```

O navegador abre na tela.

Isso e bom para:

- estudar;
- depurar;
- ver o que a automacao esta fazendo;
- entender onde o fluxo quebra.

Com `Headless = true`, ou sem configurar, o navegador pode rodar sem interface visivel.

Isso e comum em:

- servidores;
- pipelines;
- execucoes agendadas;
- automacoes que ja estao estaveis.

Para aprender, use `Headless = false`.

## 8. Estrutura inicial recomendada

No inicio, voce pode deixar tudo em `Program.cs`.

Mas conforme o fluxo cresce, o codigo fica dificil de manter.

Uma estrutura simples para automacao:

```txt
PlaywrightAutomacao/
  Program.cs
  Services/
    SistemaLegadoAutomation.cs
  Models/
    Cliente.cs
  Config/
    SistemaLegadoOptions.cs
```

Ideia de responsabilidade:

```txt
Program.cs
Inicia a aplicacao e chama a automacao.

SistemaLegadoAutomation.cs
Contem o fluxo de navegador.

Cliente.cs
Representa os dados que serao preenchidos.

SistemaLegadoOptions.cs
Representa configuracoes como URL e usuario.
```

No comeco, nao precisa criar muitas camadas.

Comece simples e organize quando o codigo comecar a repetir.

## 9. Exemplo com metodo separado

Exemplo:

```csharp
using Microsoft.Playwright;

await ExecutarAsync();

static async Task ExecutarAsync()
{
    using var playwright = await Playwright.CreateAsync();

    await using var browser = await playwright.Chromium.LaunchAsync(new()
    {
        Headless = false
    });

    var page = await browser.NewPageAsync();

    await page.GotoAsync("https://example.com");

    var title = await page.TitleAsync();

    Console.WriteLine(title);
}
```

Esse formato ja separa a execucao em um metodo.

Depois, esse metodo pode virar uma classe propria.

## 10. Cuidados com credenciais

Evite fazer isso:

```csharp
var usuario = "admin";
var senha = "123456";
```

Credenciais nao devem ficar fixas no codigo.

Opcoes melhores:

- variaveis de ambiente;
- User Secrets em ambiente de desenvolvimento;
- arquivo de configuracao fora do Git;
- cofre de segredos em ambiente profissional.

Mesmo em estudo, vale criar o habito correto.

## 11. Cuidados com arquivos gerados

Automacoes podem gerar:

- screenshots;
- logs;
- arquivos baixados;
- estado de autenticacao;
- relatorios;
- evidencias de erro.

Esses arquivos nem sempre devem ir para o Git.

Exemplo de itens que podem ser ignorados:

```txt
bin/
obj/
evidencias/
downloads/
playwright/.auth/
```

O arquivo `playwright/.auth/` merece cuidado especial, porque pode conter cookies, tokens e dados de sessao.

## 12. Boas praticas iniciais

Boas praticas para a estrutura inicial:

- comece com projeto console para aprender;
- instale `Microsoft.Playwright` quando for usar como biblioteca;
- rode `dotnet build` antes de instalar navegadores;
- use `Headless = false` durante estudos;
- separe o codigo quando o fluxo crescer;
- nao coloque credenciais no codigo;
- ignore arquivos gerados;
- documente comandos usados na instalacao;
- teste com uma pagina simples antes de ir para sistema real.

## 13. Conclusao

A instalacao do Playwright com C# envolve tres passos principais:

```txt
Criar projeto
Instalar pacote Microsoft.Playwright
Instalar navegadores
```

Para automacoes reais, o melhor inicio e usar Playwright como biblioteca em um projeto console.

Depois que a base estiver clara, voce pode evoluir para uma estrutura mais profissional com configuracao, logs, services e execucao agendada.

Fontes para estudo:

- https://playwright.dev/dotnet/docs/library
- https://playwright.dev/dotnet/docs/intro
- https://learn.microsoft.com/en-us/aspnet/core/security/app-secrets
