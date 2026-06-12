# Esperas carregamento e sincronizacao

## 1. O que sao esperas

Esperas sao formas de fazer a automacao aguardar ate que a pagina esteja pronta para a proxima acao.

Em uma automacao real, a tela nem sempre responde imediatamente.

Exemplos:

```txt
Pagina demora para carregar
Botao aparece depois de uma consulta
Tabela e preenchida via JavaScript
Modal abre com atraso
Login redireciona depois de alguns segundos
Campo fica habilitado apenas depois de selecionar outra opcao
```

Se a automacao nao esperar corretamente, ela pode tentar agir antes da hora.

## 2. O problema de sincronizacao

Sincronizacao e o alinhamento entre o tempo da automacao e o tempo da pagina.

Exemplo de problema:

```txt
Automacao clica em Buscar.
Sistema ainda esta carregando os resultados.
Automacao tenta ler a tabela.
Tabela ainda esta vazia.
Automacao falha ou captura dados errados.
```

Esse tipo de erro e comum em sistemas antigos e em paginas com carregamento parcial.

O objetivo das esperas e evitar esse desencontro.

## 3. Auto-waiting do Playwright

O Playwright possui esperas automaticas em muitas acoes.

Por exemplo, antes de clicar, ele pode esperar o elemento estar:

- visivel;
- estavel;
- habilitado;
- pronto para receber eventos.

Exemplo:

```csharp
await page.GetByRole(AriaRole.Button, new() { Name = "Salvar" }).ClickAsync();
```

O Playwright nao clica de qualquer jeito. Ele tenta garantir que o botao esteja acionavel.

Mesmo assim, auto-waiting nao resolve todos os casos.

Voce ainda precisa esperar resultados da aplicacao.

## 4. Esperar por elemento

Uma das melhores formas de espera e aguardar um elemento importante aparecer.

Exemplo:

```csharp
await page.GetByText("Cadastro realizado com sucesso").WaitForAsync();
```

Esse codigo espera a mensagem aparecer.

Outro exemplo:

```csharp
await page.GetByLabel("Nome").WaitForAsync();
```

Esse codigo espera o campo `Nome` estar disponivel.

Esse tipo de espera e melhor do que esperar um tempo fixo, porque depende de um sinal real da tela.

## 5. Esperar por URL

Quando uma acao redireciona para outra pagina, voce pode esperar a URL mudar.

Exemplo:

```csharp
await page.GetByRole(AriaRole.Button, new() { Name = "Entrar" }).ClickAsync();

await page.WaitForURLAsync("**/home");
```

Esse fluxo:

- clica em entrar;
- espera a URL chegar em `/home`.

Isso e comum depois de login.

Mas cuidado: nem todo sistema muda a URL.

Alguns sistemas carregam conteudo na mesma pagina.

Nesses casos, espere um elemento da tela.

## 6. WaitForLoadStateAsync

`WaitForLoadStateAsync` espera um estado de carregamento da pagina.

Exemplo:

```csharp
await page.WaitForLoadStateAsync(LoadState.DOMContentLoaded);
```

Estados comuns:

```txt
DOMContentLoaded
Load
NetworkIdle
```

`DOMContentLoaded` indica que o HTML inicial foi carregado.

`Load` indica que a pagina terminou o evento de carregamento.

`NetworkIdle` espera a rede ficar parada por um tempo.

Use `NetworkIdle` com cuidado, porque algumas paginas mantem requests ativos e podem nunca ficar totalmente paradas.

## 7. Esperar por resposta de rede

As vezes, o melhor sinal e uma resposta HTTP.

Exemplo:

```csharp
var responseTask = page.WaitForResponseAsync(response =>
    response.Url.Contains("/clientes") && response.Status == 200
);

await page.GetByRole(AriaRole.Button, new() { Name = "Buscar" }).ClickAsync();

var response = await responseTask;
```

Esse fluxo:

- prepara a espera pela resposta;
- clica em buscar;
- aguarda a resposta esperada.

Isso ajuda quando a tela carrega dados de forma assincrona.

Mesmo usando Playwright pela interface, entender requests pode ajudar muito.

## 8. WaitForTimeoutAsync

`WaitForTimeoutAsync` espera um tempo fixo.

Exemplo:

```csharp
await page.WaitForTimeoutAsync(3000);
```

Isso espera 3 segundos.

Esse metodo deve ser usado com cuidado.

Problemas:

- se a tela carregar em 1 segundo, voce perde tempo;
- se a tela carregar em 5 segundos, a automacao falha;
- o teste ou automacao fica mais lenta;
- o problema real fica escondido.

Use tempo fixo apenas quando houver uma justificativa clara.

Para estudo e debug, pode ajudar. Para producao, prefira esperar condicoes reais.

## 9. Timeout

Timeout e o tempo maximo que o Playwright espera antes de considerar erro.

Voce pode configurar timeout em uma acao:

```csharp
await page.GetByText("Sucesso").WaitForAsync(new()
{
    Timeout = 10000
});
```

Esse codigo espera ate 10 segundos.

Tambem pode configurar timeout padrao:

```csharp
page.SetDefaultTimeout(10000);
```

Isso define um tempo padrao para a pagina.

Em sistemas legados, as telas podem ser mais lentas, mas aumentar timeout nao deve ser a unica solucao.

O ideal e esperar sinais corretos.

## 10. Exemplo ruim e exemplo melhor

Exemplo ruim:

```csharp
await page.GetByRole(AriaRole.Button, new() { Name = "Buscar" }).ClickAsync();
await page.WaitForTimeoutAsync(5000);

var texto = await page.Locator("#resultado").InnerTextAsync();
```

Problema:

```txt
O codigo espera 5 segundos sem saber se o resultado apareceu.
```

Exemplo melhor:

```csharp
await page.GetByRole(AriaRole.Button, new() { Name = "Buscar" }).ClickAsync();

await page.Locator("#resultado").WaitForAsync();

var texto = await page.Locator("#resultado").InnerTextAsync();
```

Agora o codigo espera o elemento real.

## 11. Exemplo completo

Exemplo:

```csharp
await page.GotoAsync("https://sistema-legado.com/clientes");

await page.GetByLabel("Nome").FillAsync("Nicolas");

var responseTask = page.WaitForResponseAsync(response =>
    response.Url.Contains("/clientes") && response.Status == 200
);

await page.GetByRole(AriaRole.Button, new() { Name = "Buscar" }).ClickAsync();

await responseTask;

await page.GetByText("Nicolas").WaitForAsync(new()
{
    Timeout = 10000
});
```

Esse fluxo:

- abre a tela de clientes;
- preenche busca;
- prepara espera da resposta;
- clica em buscar;
- espera resposta;
- espera o texto aparecer.

## 12. Boas praticas

Boas praticas:

- espere elementos reais da tela;
- use `WaitForURLAsync` quando houver redirecionamento;
- use `WaitForResponseAsync` quando a tela depender de request;
- evite `WaitForTimeoutAsync` como solucao principal;
- configure timeout adequado para sistemas lentos;
- registre em qual etapa a espera falhou;
- capture screenshot quando um elemento nao aparecer;
- nao avance sem confirmar que a tela esta pronta;
- prefira sinais de negocio, como mensagem de sucesso.

## 13. Conclusao

Esperas sao essenciais para automacoes confiaveis.

O Playwright ja possui auto-waiting, mas isso nao elimina a necessidade de esperar sinais da aplicacao.

Em sistemas legados, sincronizacao e uma das partes mais importantes do trabalho.

Uma boa automacao nao espera apenas tempo.

Ela espera evidencias:

- URL correta;
- campo visivel;
- tabela carregada;
- mensagem exibida;
- resposta HTTP concluida;
- botao habilitado.

Fontes para estudo:

- https://playwright.dev/dotnet/docs/actionability
- https://playwright.dev/dotnet/docs/navigations
- https://playwright.dev/dotnet/docs/api/class-page
