# Captura de dados da pagina

## 1. O que e captura de dados

Captura de dados e o processo de ler informacoes exibidas na pagina.

Em automacoes com Playwright, nem sempre voce quer apenas preencher campos.

Muitas vezes voce tambem precisa extrair informacoes.

Exemplos:

```txt
Ler mensagem de sucesso
Capturar numero de protocolo
Ler status de um pedido
Extrair linhas de uma tabela
Verificar valor exibido
Conferir se um cadastro existe
Capturar texto de erro
```

Em sistemas sem API, a tela pode ser a unica fonte disponivel para consultar dados.

## 2. Por que capturar dados da tela

Capturar dados da tela e util quando:

- o sistema nao possui API;
- a informacao so aparece na interface;
- a automacao precisa validar resultado;
- a automacao precisa gerar relatorio;
- a automacao precisa registrar protocolo;
- a automacao precisa tomar decisao com base no texto da pagina.

Exemplo:

```txt
Automacao cadastra um cliente.
Sistema mostra: Protocolo 12345 gerado com sucesso.
Automacao captura o protocolo.
Automacao salva o protocolo no banco ou no log.
```

Sem essa captura, voce sabe que clicou em salvar, mas nao sabe qual resultado o sistema retornou.

## 3. InnerTextAsync

`InnerTextAsync` pega o texto visivel de um elemento.

Exemplo:

```csharp
var mensagem = await page.GetByText("Cadastro realizado").InnerTextAsync();
```

Outro exemplo:

```csharp
var status = await page.Locator("#status").InnerTextAsync();

Console.WriteLine(status);
```

Esse metodo e bastante usado para textos que aparecem na tela.

## 4. TextContentAsync

`TextContentAsync` pega o conteudo de texto de um elemento.

Exemplo:

```csharp
var texto = await page.Locator("#mensagem").TextContentAsync();
```

Diferença pratica:

```txt
InnerTextAsync:
mais proximo do texto visivel para o usuario.

TextContentAsync:
mais proximo do conteudo de texto no HTML.
```

Na maioria dos estudos iniciais, `InnerTextAsync` costuma ser mais intuitivo.

## 5. InputValueAsync

Para capturar o valor de um campo, use `InputValueAsync`.

Exemplo:

```csharp
var nome = await page.GetByLabel("Nome").InputValueAsync();
```

Isso e diferente de `InnerTextAsync`.

Campos de formulario normalmente guardam valor no atributo `value`, nao como texto interno.

Exemplo:

```csharp
var cpf = await page.GetByLabel("CPF").InputValueAsync();

Console.WriteLine(cpf);
```

Use `InputValueAsync` para inputs e textareas.

## 6. GetAttributeAsync

`GetAttributeAsync` pega o valor de um atributo HTML.

Exemplo:

```csharp
var href = await page.GetByRole(AriaRole.Link, new() { Name = "Detalhes" }).GetAttributeAsync("href");
```

Outros exemplos:

```csharp
var valor = await page.Locator("#cliente").GetAttributeAsync("data-id");
var classe = await page.Locator("#mensagem").GetAttributeAsync("class");
var src = await page.Locator("img.logo").GetAttributeAsync("src");
```

Isso e util quando o dado nao aparece diretamente como texto.

Em sistemas legados, alguns valores importantes podem estar em atributos escondidos.

## 7. Capturando lista de textos

Para capturar varios textos, use `AllInnerTextsAsync`.

Exemplo:

```csharp
var nomes = await page.Locator("table tbody tr td:first-child").AllInnerTextsAsync();

foreach (var nome in nomes)
{
    Console.WriteLine(nome);
}
```

Esse codigo:

- localiza a primeira coluna de cada linha da tabela;
- captura os textos;
- imprime cada nome.

Esse tipo de captura aparece muito em tabelas de resultado.

## 8. Capturando dados de tabela

Tabelas sao comuns em sistemas administrativos.

Exemplo de captura simples:

```csharp
var linhas = page.Locator("table tbody tr");
var quantidade = await linhas.CountAsync();

for (var i = 0; i < quantidade; i++)
{
    var linha = linhas.Nth(i);

    var colunas = await linha.Locator("td").AllInnerTextsAsync();

    Console.WriteLine(string.Join(" | ", colunas));
}
```

Esse codigo:

- localiza todas as linhas;
- conta quantas existem;
- percorre cada linha;
- captura os textos das colunas;
- imprime os dados.

Em um projeto real, voce poderia transformar cada linha em um objeto C#.

## 9. Capturando mensagem de sucesso

Depois de salvar um cadastro, muitas vezes o sistema mostra uma mensagem.

Exemplo:

```csharp
await page.GetByRole(AriaRole.Button, new() { Name = "Salvar" }).ClickAsync();

var mensagemLocator = page.Locator(".mensagem-sucesso");

await mensagemLocator.WaitForAsync();

var mensagem = await mensagemLocator.InnerTextAsync();

Console.WriteLine(mensagem);
```

Esse fluxo:

- clica em salvar;
- espera a mensagem aparecer;
- captura o texto;
- imprime ou registra.

Em uma automacao de producao, essa mensagem pode definir o status do processamento.

## 10. Capturando erro

Tambem e importante capturar erro.

Exemplo:

```csharp
var erroLocator = page.Locator(".mensagem-erro");

if (await erroLocator.IsVisibleAsync())
{
    var erro = await erroLocator.InnerTextAsync();

    Console.WriteLine($"Erro encontrado: {erro}");
}
```

Esse tipo de verificacao ajuda a registrar o motivo da falha.

Mas cuidado: se o elemento nao existir, dependendo do locator e do metodo, voce pode precisar tratar timeout ou verificar contagem.

Exemplo:

```csharp
var erros = page.Locator(".mensagem-erro");

if (await erros.CountAsync() > 0)
{
    var erro = await erros.First.InnerTextAsync();

    Console.WriteLine(erro);
}
```

## 11. Captura com decisao

Automacoes reais muitas vezes precisam decidir o que fazer.

Exemplo:

```csharp
await page.GetByLabel("CPF").FillAsync("00000000000");
await page.GetByRole(AriaRole.Button, new() { Name = "Buscar" }).ClickAsync();

await page.WaitForLoadStateAsync(LoadState.DOMContentLoaded);

var nenhumRegistro = page.GetByText("Nenhum registro encontrado");

if (await nenhumRegistro.IsVisibleAsync())
{
    Console.WriteLine("Cliente nao encontrado. Pode cadastrar.");
}
else
{
    Console.WriteLine("Cliente ja existe. Nao cadastrar novamente.");
}
```

Esse exemplo usa o texto da pagina para decidir o proximo passo.

## 12. Screenshot como evidencia

Capturar dados tambem pode envolver evidencias visuais.

Exemplo:

```csharp
await page.ScreenshotAsync(new()
{
    Path = "evidencias/cadastro-cliente.png",
    FullPage = true
});
```

Isso salva um print da pagina.

Screenshots sao uteis para:

- erro;
- auditoria;
- comprovante;
- investigacao;
- validacao manual posterior.

Em producao, organize bem a pasta de evidencias.

## 13. Exemplo completo

Exemplo de captura de protocolo:

```csharp
await page.GetByRole(AriaRole.Button, new() { Name = "Salvar" }).ClickAsync();

var mensagem = page.Locator(".mensagem-sucesso");

await mensagem.WaitForAsync();

var textoMensagem = await mensagem.InnerTextAsync();

Console.WriteLine($"Resultado: {textoMensagem}");

await page.ScreenshotAsync(new()
{
    Path = "evidencias/ultimo-cadastro.png",
    FullPage = true
});
```

Esse fluxo:

- salva o formulario;
- espera a mensagem;
- captura o texto;
- registra o resultado;
- tira screenshot.

## 14. Boas praticas

Boas praticas para captura de dados:

- espere o elemento aparecer antes de ler;
- use `InnerTextAsync` para texto visivel;
- use `InputValueAsync` para campos;
- use `GetAttributeAsync` para atributos;
- capture mensagens de sucesso e erro;
- registre dados importantes no log;
- tire screenshot em falhas;
- trate tabelas com cuidado;
- nao dependa de textos instaveis sem necessidade;
- transforme dados capturados em objetos quando o fluxo crescer.

## 15. Conclusao

Capturar dados da pagina e essencial em automacoes de sistemas sem API.

Nao basta clicar e preencher.

Uma automacao real precisa ler respostas da tela para saber o que aconteceu.

Os metodos mais importantes neste ponto sao:

- `InnerTextAsync`;
- `TextContentAsync`;
- `InputValueAsync`;
- `GetAttributeAsync`;
- `AllInnerTextsAsync`;
- `ScreenshotAsync`.

Com esses recursos, a automacao consegue validar resultados, registrar evidencias e tomar decisoes com base no estado real da pagina.

Fontes para estudo:

- https://playwright.dev/dotnet/docs/locators
- https://playwright.dev/dotnet/docs/screenshots
- https://playwright.dev/dotnet/docs/api/class-locator
