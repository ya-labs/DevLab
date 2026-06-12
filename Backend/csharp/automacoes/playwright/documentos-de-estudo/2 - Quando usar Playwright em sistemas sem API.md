# Quando usar Playwright em sistemas sem API

## 1. O problema

Em um sistema ideal, a integracao entre aplicacoes acontece por API.

Uma API permite que um sistema envie e receba dados de forma estruturada, sem depender da tela.

Exemplo:

```txt
Sistema A envia dados para uma API
API valida os dados
Sistema B salva as informacoes
API devolve uma resposta
```

Mas em muitos cenarios reais isso nao existe.

Alguns sistemas antigos foram criados apenas para uso manual. Eles possuem telas, menus e formularios, mas nao oferecem endpoints para integracao.

Nesse caso, uma pessoa precisa abrir o navegador, fazer login, preencher campos e repetir o processo varias vezes.

Quando essa tarefa e repetitiva, lenta ou sujeita a erro humano, o Playwright pode ajudar.

## 2. O que significa sistema sem API

Um sistema sem API e um sistema que nao oferece uma forma oficial de integracao por codigo.

Ele pode ate usar HTTP internamente, mas isso nao significa que ele tenha uma API publica, documentada e segura para consumo.

Na pratica, voce so consegue operar o sistema pela interface.

Exemplo:

```txt
Nao existe endpoint para cadastrar pedido.
Nao existe documentacao de integracao.
Nao existe token de API.
Nao existe contrato de request e response.
Existe apenas uma tela com formulario.
```

Nesse tipo de cenario, a automacao precisa interagir com a tela como um usuario faria.

## 3. Quando Playwright faz sentido

Playwright faz sentido quando:

- o sistema nao possui API;
- criar uma API nao e possivel no momento;
- a tarefa manual e repetitiva;
- o volume de dados e alto;
- o processo precisa ser executado com frequencia;
- o erro humano gera custo;
- a automacao pode reduzir tempo operacional;
- a empresa precisa integrar com um sistema legado;
- o sistema so aceita entrada de dados pela interface web.

Exemplo:

```txt
Todo dia uma planilha chega com 300 registros.
Um usuario precisa copiar os dados da planilha.
Depois precisa colar cada registro em um sistema antigo.
O sistema antigo nao tem API.
```

Nesse caso, uma automacao pode ler os dados e preencher o sistema pela tela.

## 4. Quando Playwright nao e a melhor opcao

Playwright nao deve ser a primeira escolha quando existe uma API confiavel.

Se o sistema oferece API, normalmente e melhor integrar pela API.

API costuma ser melhor porque:

- e mais estavel;
- e mais rapida;
- depende menos da interface visual;
- possui contrato mais claro;
- e mais facil de versionar;
- permite melhor tratamento de erros;
- reduz risco de quebra por mudanca visual.

Comparacao simples:

```txt
Com API:
Sistema envia dados diretamente.

Com Playwright:
Sistema abre tela, encontra campos, preenche e clica.
```

O segundo caminho e util quando nao ha alternativa melhor.

## 5. Exemplo de uso real

Imagine um sistema legado de cadastro de clientes.

Ele possui:

- tela de login;
- menu lateral;
- formulario de cliente;
- botao salvar;
- mensagem de sucesso.

Mas nao possui API.

Fluxo manual:

```txt
1. Abrir navegador
2. Acessar sistema
3. Fazer login
4. Ir para cadastro de cliente
5. Preencher nome
6. Preencher CPF
7. Preencher telefone
8. Clicar em salvar
9. Conferir mensagem de sucesso
10. Repetir para o proximo cliente
```

Fluxo automatizado:

```txt
1. Aplicacao C# le os dados
2. Playwright abre o navegador
3. Playwright faz login
4. Playwright abre a tela de cadastro
5. Playwright preenche os campos
6. Playwright salva
7. Aplicacao registra resultado
8. Fluxo repete para o proximo item
```

Esse tipo de automacao nao e apenas teste. E automacao operacional.

## 6. Exemplo pequeno em CSharp

Exemplo simplificado:

```csharp
using Microsoft.Playwright;

using var playwright = await Playwright.CreateAsync();

await using var browser = await playwright.Chromium.LaunchAsync(new()
{
    Headless = false
});

var page = await browser.NewPageAsync();

await page.GotoAsync("https://sistema-legado.com/clientes/novo");

await page.GetByLabel("Nome").FillAsync("Nicolas Silva");
await page.GetByLabel("CPF").FillAsync("00000000000");
await page.GetByLabel("Telefone").FillAsync("11999999999");

await page.GetByRole(AriaRole.Button, new() { Name = "Salvar" }).ClickAsync();
```

Esse codigo representa um fluxo comum:

- abrir a tela;
- preencher campos;
- clicar em salvar.

Em producao, esse codigo precisaria de mais cuidados.

Por exemplo:

- validar se o login esta ativo;
- esperar a tela carregar;
- tratar erro de campo obrigatorio;
- registrar log;
- capturar screenshot se falhar;
- evitar dados sensiveis no codigo.

## 7. Cuidados importantes

Automatizar tela e diferente de integrar com API.

Uma automacao de tela depende de detalhes visuais e estruturais da pagina.

Ela pode quebrar se:

- o nome do botao mudar;
- o campo mudar de lugar;
- o sistema alterar o HTML;
- a pagina ficar mais lenta;
- aparecer um modal inesperado;
- a sessao expirar;
- o usuario perder permissao;
- o sistema exibir captcha;
- houver instabilidade de rede.

Por isso, uma automacao com Playwright precisa ser escrita com cuidado.

Nao basta fazer o fluxo funcionar uma vez. Ela precisa ser observavel e facil de corrigir.

## 8. O que registrar em uma automacao real

Uma automacao de producao precisa deixar rastros.

Registros importantes:

- horario de inicio;
- horario de fim;
- quantidade de itens processados;
- dados principais do item processado;
- status de sucesso ou falha;
- mensagem de erro;
- screenshot em caso de falha;
- etapa onde o erro aconteceu;
- usuario usado na execucao, quando fizer sentido.

Exemplo de log:

```txt
Inicio da automacao de cadastro de clientes.
Cliente 123 iniciado.
Cliente 123 salvo com sucesso.
Cliente 124 iniciado.
Erro ao salvar cliente 124: campo CPF invalido.
Screenshot salvo em evidencias/cliente-124.png.
Fim da automacao.
```

Esse tipo de registro ajuda a investigar problemas sem precisar adivinhar o que aconteceu.

## 9. Boas praticas

Boas praticas para usar Playwright em sistemas sem API:

- use Playwright quando API nao existir;
- documente por que a automacao pela tela foi escolhida;
- mantenha os seletores organizados;
- evite repetir codigo de tela em varios lugares;
- trate cada etapa importante;
- registre logs;
- capture evidencias em erro;
- proteja credenciais;
- valide mensagens de sucesso;
- nao confie apenas no clique final;
- acompanhe mudancas no sistema legado.

Se a empresa criar uma API oficial no futuro, vale reavaliar a automacao.

## 10. Conclusao

Playwright faz sentido em sistemas sem API quando a unica forma de executar o processo e pela interface web.

Ele permite transformar tarefas manuais e repetitivas em fluxos automatizados com C#.

Mesmo assim, automacao de tela deve ser vista como uma solucao cuidadosa, porque depende da estabilidade da interface.

Quando existir API, prefira API. Quando nao existir API e o processo precisar ser automatizado, Playwright pode ser uma ferramenta muito util.

Fontes para estudo:

- https://playwright.dev/dotnet/
- https://playwright.dev/dotnet/docs/library
- https://playwright.dev/dotnet/docs/locators
