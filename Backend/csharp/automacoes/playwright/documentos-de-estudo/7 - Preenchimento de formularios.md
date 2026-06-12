# Preenchimento de formularios

## 1. O que e preenchimento de formularios

Preenchimento de formulario e uma das tarefas mais comuns em automacoes com Playwright.

Em sistemas reais, muitas rotinas dependem de inserir informacoes em telas.

Exemplos:

```txt
Cadastrar cliente
Atualizar pedido
Preencher dados fiscais
Enviar solicitacao
Consultar relatorio
Registrar atendimento
```

Quando o sistema nao possui API, o formulario vira o principal ponto de entrada dos dados.

## 2. Exemplo de formulario manual

Um fluxo manual pode ser assim:

```txt
Abrir tela de cadastro
Preencher nome
Preencher CPF
Preencher email
Selecionar estado
Marcar aceite
Clicar em salvar
Conferir mensagem de sucesso
```

Com Playwright, esse fluxo pode ser escrito em C#.

Exemplo:

```csharp
await page.GetByLabel("Nome").FillAsync("Nicolas Silva");
await page.GetByLabel("CPF").FillAsync("00000000000");
await page.GetByLabel("Email").FillAsync("nicolas@example.com");

await page.GetByRole(AriaRole.Button, new() { Name = "Salvar" }).ClickAsync();
```

Esse e o tipo de base que aparece em quase toda automacao de sistema legado.

## 3. FillAsync

`FillAsync` preenche um campo com um valor.

Exemplo:

```csharp
await page.GetByLabel("Nome").FillAsync("Nicolas");
```

Se o campo ja tiver algum texto, o `FillAsync` normalmente limpa o campo e coloca o novo valor.

Isso e util em formularios de edicao.

Exemplo:

```csharp
await page.GetByLabel("Telefone").FillAsync("11999999999");
```

Esse comando define o valor final do campo.

## 4. TypeAsync

`TypeAsync` simula digitacao caractere por caractere.

Exemplo:

```csharp
await page.GetByLabel("Nome").TypeAsync("Nicolas");
```

Ele pode ser util quando o sistema possui mascaras ou scripts antigos que reagem a cada tecla.

Exemplo comum:

```txt
Campo CPF aplica mascara enquanto o usuario digita.
Campo busca endereco depois que CEP e digitado.
Campo valida valor a cada tecla.
```

Nesses casos, `TypeAsync` pode funcionar melhor do que `FillAsync`.

Mas para a maioria dos campos simples, `FillAsync` e mais direto.

## 5. PressAsync

`PressAsync` simula uma tecla.

Exemplo:

```csharp
await page.GetByLabel("Busca").FillAsync("cliente");
await page.GetByLabel("Busca").PressAsync("Enter");
```

Isso e util em campos de pesquisa.

Outros exemplos:

```csharp
await page.Keyboard.PressAsync("Tab");
await page.Keyboard.PressAsync("Enter");
await page.Keyboard.PressAsync("Escape");
```

Use com cuidado.

Automacoes baseadas em `Tab` podem ficar frageis se a ordem dos campos mudar.

## 6. SelectOptionAsync

Para campos `select`, use `SelectOptionAsync`.

Exemplo:

```csharp
await page.GetByLabel("Estado").SelectOptionAsync("SP");
```

Tambem e possivel selecionar pelo texto visivel ou por outras opcoes, dependendo do HTML.

Exemplo:

```csharp
await page.Locator("select[name='estado']").SelectOptionAsync(new[] { "SP" });
```

Em sistemas legados, muitos campos de selecao ainda usam `select` tradicional.

Nesse caso, esse metodo costuma funcionar bem.

## 7. Checkbox

Para marcar uma checkbox, use `CheckAsync`.

Exemplo:

```csharp
await page.GetByLabel("Aceito os termos").CheckAsync();
```

Para desmarcar:

```csharp
await page.GetByLabel("Aceito os termos").UncheckAsync();
```

Tambem e possivel verificar se esta marcada:

```csharp
var estaMarcado = await page.GetByLabel("Aceito os termos").IsCheckedAsync();
```

Isso ajuda quando o estado inicial do campo pode variar.

## 8. Radio button

Radio buttons tambem podem ser marcados com `CheckAsync`.

Exemplo:

```csharp
await page.GetByLabel("Pessoa fisica").CheckAsync();
```

Em formularios, radio buttons normalmente representam escolhas exclusivas.

Exemplo:

```txt
Pessoa fisica
Pessoa juridica
```

Escolher um geralmente desmarca o outro.

## 9. Campos com mascara

Sistemas legados costumam ter campos com mascara.

Exemplos:

- CPF;
- CNPJ;
- telefone;
- CEP;
- data;
- moeda.

Algumas mascaras funcionam bem com `FillAsync`.

Outras precisam de `TypeAsync`.

Exemplo:

```csharp
await page.GetByLabel("CPF").TypeAsync("00000000000");
```

Se a mascara falhar com `FillAsync`, teste `TypeAsync`.

Tambem pode ser necessario limpar o campo antes:

```csharp
var campoCpf = page.GetByLabel("CPF");

await campoCpf.ClickAsync();
await campoCpf.PressAsync("Control+A");
await campoCpf.TypeAsync("00000000000");
```

## 10. Validando depois de preencher

Depois de preencher um formulario, nao confie apenas no clique.

Valide o resultado.

Exemplo:

```csharp
await page.GetByRole(AriaRole.Button, new() { Name = "Salvar" }).ClickAsync();

await page.GetByText("Cadastro realizado com sucesso").WaitForAsync();
```

Esse codigo confirma que a mensagem de sucesso apareceu.

Tambem pode ser necessario validar erro:

```csharp
await page.GetByText("CPF invalido").WaitForAsync();
```

Em automacao de producao, essa validacao define se o item foi processado com sucesso ou falha.

## 11. Exemplo completo

Exemplo de cadastro simples:

```csharp
await page.GotoAsync("https://sistema-legado.com/clientes/novo");

await page.GetByLabel("Nome").FillAsync("Nicolas Silva");
await page.GetByLabel("CPF").TypeAsync("00000000000");
await page.GetByLabel("Email").FillAsync("nicolas@example.com");
await page.GetByLabel("Estado").SelectOptionAsync("SP");
await page.GetByLabel("Ativo").CheckAsync();

await page.GetByRole(AriaRole.Button, new() { Name = "Salvar" }).ClickAsync();

await page.GetByText("Cadastro realizado com sucesso").WaitForAsync();
```

Esse fluxo:

- abre a tela de cadastro;
- preenche campos de texto;
- digita CPF;
- seleciona estado;
- marca checkbox;
- salva;
- espera mensagem de sucesso.

## 12. Boas praticas

Boas praticas para formularios:

- prefira `FillAsync` para campos simples;
- use `TypeAsync` quando a tela tiver mascara ou evento por tecla;
- use `SelectOptionAsync` para `select`;
- use `CheckAsync` e `UncheckAsync` para checkbox;
- valide mensagem de sucesso ou erro;
- limpe campos quando estiver editando registros;
- evite depender de `Tab` para navegar entre campos;
- trate campos obrigatorios;
- registre qual item estava sendo preenchido em caso de erro;
- capture screenshot quando o envio falhar.

## 13. Conclusao

Preencher formularios e uma das bases da automacao com Playwright.

Em sistemas sem API, a tela e o caminho principal para enviar dados.

Por isso, voce precisa dominar:

- campos de texto;
- selects;
- checkboxes;
- radio buttons;
- mascaras;
- validacoes;
- mensagens de sucesso e erro.

O ponto mais importante e nao apenas preencher, mas confirmar que o sistema aceitou os dados.

Fontes para estudo:

- https://playwright.dev/dotnet/docs/input
- https://playwright.dev/dotnet/docs/locators
- https://playwright.dev/dotnet/docs/actionability
