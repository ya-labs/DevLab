# Cliques botoes e interacoes com tela

## 1. O que sao interacoes com tela

Interacoes com tela sao as acoes que a automacao executa na pagina.

Exemplos:

- clicar em botoes;
- clicar em links;
- preencher campos;
- marcar checkboxes;
- selecionar opcoes;
- pressionar teclas;
- abrir menus;
- fechar modais;
- passar o mouse;
- enviar arquivos.

Em uma automacao com Playwright, essas acoes simulam parte do comportamento de um usuario real.

## 2. Clique simples

O clique e uma das interacoes mais comuns.

Exemplo:

```csharp
await page.GetByRole(AriaRole.Button, new() { Name = "Salvar" }).ClickAsync();
```

Esse codigo:

- localiza um botao chamado `Salvar`;
- espera ele estar pronto para interacao;
- executa o clique.

Tambem pode clicar em link:

```csharp
await page.GetByRole(AriaRole.Link, new() { Name = "Clientes" }).ClickAsync();
```

## 3. O que o Playwright verifica antes do clique

Antes de clicar, o Playwright costuma verificar se o elemento esta pronto para receber a acao.

Ele pode verificar se o elemento esta:

- visivel;
- estavel;
- habilitado;
- recebendo eventos;
- disponivel para interacao.

Isso e chamado de actionability.

Na pratica, isso reduz varios erros comuns.

Exemplo:

```txt
Botao existe no HTML, mas ainda esta invisivel.
Playwright espera antes de clicar.
```

Mesmo assim, voce ainda precisa escrever boas esperas quando a tela depende de carregamentos complexos.

## 4. Clique duplo

Para clique duplo, use `DblClickAsync`.

Exemplo:

```csharp
await page.GetByText("Registro 123").DblClickAsync();
```

Isso pode aparecer em sistemas antigos onde abrir um registro depende de duplo clique em uma linha.

Use apenas quando o sistema realmente exige duplo clique.

Se houver botao de editar, normalmente e melhor clicar no botao.

## 5. Clique com botao direito

Para clique com botao direito:

```csharp
await page.GetByText("Registro 123").ClickAsync(new()
{
    Button = MouseButton.Right
});
```

Isso pode ser usado quando o sistema possui menu de contexto.

Mas esse tipo de interacao tende a ser mais fragil.

Sempre que houver um caminho mais direto pela tela, prefira o caminho mais simples.

## 6. Hover

`HoverAsync` passa o mouse sobre um elemento.

Exemplo:

```csharp
await page.GetByText("Relatorios").HoverAsync();
```

Isso e util quando um menu aparece apenas ao passar o mouse.

Exemplo:

```csharp
await page.GetByText("Relatorios").HoverAsync();
await page.GetByRole(AriaRole.Link, new() { Name = "Vendas" }).ClickAsync();
```

Em sistemas legados, menus com hover sao comuns.

Nesses casos, espere o item do submenu aparecer antes de clicar.

## 7. Pressionando teclas

Voce pode pressionar teclas pelo elemento ou pelo teclado da pagina.

Exemplo em um campo:

```csharp
await page.GetByLabel("Busca").FillAsync("cliente");
await page.GetByLabel("Busca").PressAsync("Enter");
```

Exemplo pelo teclado:

```csharp
await page.Keyboard.PressAsync("Escape");
```

Teclas comuns:

```txt
Enter
Escape
Tab
ArrowDown
ArrowUp
Control+A
```

Use `Tab` com cuidado, porque depende da ordem dos elementos na tela.

## 8. Menus e submenus

Muitos sistemas legados usam menus.

Exemplo de fluxo:

```txt
Passar mouse em Cadastros
Clicar em Clientes
Esperar tela de Clientes abrir
```

Codigo:

```csharp
await page.GetByText("Cadastros").HoverAsync();
await page.GetByRole(AriaRole.Link, new() { Name = "Clientes" }).ClickAsync();
await page.GetByRole(AriaRole.Heading, new() { Name = "Clientes" }).WaitForAsync();
```

O importante e confirmar que a tela esperada abriu.

## 9. Modais

Modais sao janelas internas da pagina.

Exemplos:

```txt
Confirmar exclusao
Aviso de erro
Selecao de cliente
Mensagem de sessao expirada
```

Exemplo:

```csharp
await page.GetByRole(AriaRole.Button, new() { Name = "Excluir" }).ClickAsync();
await page.GetByRole(AriaRole.Button, new() { Name = "Confirmar" }).ClickAsync();
```

Melhorando:

```csharp
await page.GetByRole(AriaRole.Dialog).WaitForAsync();
await page.GetByRole(AriaRole.Button, new() { Name = "Confirmar" }).ClickAsync();
```

Esperar o modal aparecer deixa o fluxo mais confiavel.

## 10. Upload de arquivo

Para campos de upload, use `SetInputFilesAsync`.

Exemplo:

```csharp
await page.Locator("input[type='file']").SetInputFilesAsync("C:\\arquivos\\documento.pdf");
```

Esse comando define o arquivo no campo.

Se o sistema abre um botao visual que aciona um input escondido, talvez seja necessario localizar o `input[type='file']`.

Em automacoes reais, valide se o arquivo foi aceito.

Exemplo:

```csharp
await page.GetByText("Arquivo anexado com sucesso").WaitForAsync();
```

## 11. Exemplo completo

Exemplo de interacoes:

```csharp
await page.GotoAsync("https://sistema-legado.com/home");

await page.GetByText("Cadastros").HoverAsync();
await page.GetByRole(AriaRole.Link, new() { Name = "Clientes" }).ClickAsync();

await page.GetByRole(AriaRole.Heading, new() { Name = "Clientes" }).WaitForAsync();

await page.GetByRole(AriaRole.Button, new() { Name = "Novo" }).ClickAsync();

await page.GetByLabel("Nome").FillAsync("Nicolas Silva");
await page.GetByLabel("Email").FillAsync("nicolas@example.com");

await page.GetByRole(AriaRole.Button, new() { Name = "Salvar" }).ClickAsync();

await page.GetByText("Cliente salvo com sucesso").WaitForAsync();
```

Esse fluxo:

- abre a tela inicial;
- usa menu;
- entra em clientes;
- clica em novo;
- preenche campos;
- salva;
- valida sucesso.

## 12. Erros comuns

Erros comuns em interacoes:

- clicar antes da tela carregar;
- usar seletor muito fragil;
- nao esperar modal aparecer;
- clicar em texto que aparece em mais de um lugar;
- depender de `Tab` para tudo;
- usar tempo fixo como solucao principal;
- nao validar se a acao funcionou;
- nao tratar sessao expirada;
- nao registrar em qual etapa a automacao falhou.

Quando uma automacao quebra, muitas vezes o problema nao e o clique em si, mas a falta de confirmacao antes ou depois dele.

## 13. Boas praticas

Boas praticas:

- clique em elementos com locator claro;
- espere menus, modais e telas aparecerem;
- valide o resultado da acao;
- prefira botao e link com `GetByRole`;
- use `HoverAsync` apenas quando necessario;
- evite dependencia excessiva de teclado;
- trate confirmacoes;
- capture screenshot em erro;
- registre a etapa atual no log;
- mantenha fluxos grandes separados em metodos.

## 14. Conclusao

Cliques e interacoes sao o centro da automacao de navegador.

Mas uma boa automacao nao e feita apenas de cliques.

Ela precisa:

- localizar o elemento correto;
- esperar o momento certo;
- executar a acao;
- confirmar o resultado;
- tratar falhas.

Em sistemas legados, esse cuidado e ainda mais importante, porque as telas podem ser lentas, antigas e inconsistentes.

Fontes para estudo:

- https://playwright.dev/dotnet/docs/input
- https://playwright.dev/dotnet/docs/actionability
- https://playwright.dev/dotnet/docs/locators
