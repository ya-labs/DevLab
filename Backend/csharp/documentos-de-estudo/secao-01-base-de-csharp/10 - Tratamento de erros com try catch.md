# Tratamento de erros com try catch

## 1. O que é tratamento de erros

Tratamento de erros é a forma de lidar com situações inesperadas durante a execução do programa.

Exemplos:

- arquivo não encontrado;
- falha ao conectar no banco;
- valor inválido;
- erro de rede;
- divisão por zero;
- conversão inválida;
- permissão negada.

Sem tratamento, uma exceção pode parar a aplicação.

Com tratamento, o programa pode reagir de forma controlada.

## 2. O que é uma exceção

Exceção é um erro que acontece enquanto o programa está rodando.

Exemplo:

```csharp
int numero = int.Parse("abc");
```

Esse código tenta converter `"abc"` para inteiro.

Como isso não é possível, o C# lança uma exceção.

## 3. try catch

`try catch` serve para tentar executar um código e tratar erro caso ele aconteça.

Sintaxe:

```csharp
try
{
    // Código que pode gerar erro
}
catch (Exception ex)
{
    // Tratamento do erro
}
```

Exemplo:

```csharp
try
{
    int numero = int.Parse("abc");

    Console.WriteLine(numero);
}
catch (FormatException ex)
{
    Console.WriteLine("O texto informado não é um número válido.");
    Console.WriteLine(ex.Message);
}
```

Nesse caso, o erro é tratado e a aplicação não para de forma inesperada.

## 4. Capturando exceções específicas

Prefira capturar exceções específicas quando souber qual erro pode acontecer.

Exemplo:

```csharp
try
{
    string conteudo = File.ReadAllText("dados.txt");

    Console.WriteLine(conteudo);
}
catch (FileNotFoundException)
{
    Console.WriteLine("O arquivo não foi encontrado.");
}
```

Esse código trata especificamente o caso de arquivo inexistente.

Isso deixa o tratamento mais claro.

## 5. Vários catch

Você pode ter mais de um `catch`.

Exemplo:

```csharp
try
{
    string conteudo = File.ReadAllText("dados.txt");
    int numero = int.Parse(conteudo);

    Console.WriteLine(numero);
}
catch (FileNotFoundException)
{
    Console.WriteLine("Arquivo não encontrado.");
}
catch (FormatException)
{
    Console.WriteLine("O conteúdo do arquivo não é um número válido.");
}
catch (Exception ex)
{
    Console.WriteLine("Ocorreu um erro inesperado.");
    Console.WriteLine(ex.Message);
}
```

Ordem importante:

```txt
Exceções específicas primeiro.
Exception genérica por último.
```

Se `catch (Exception)` vier primeiro, ele captura tudo e os outros blocos podem ficar inúteis.

## 6. finally

`finally` é executado sempre, com erro ou sem erro.

Exemplo:

```csharp
try
{
    Console.WriteLine("Executando operação.");
}
catch (Exception)
{
    Console.WriteLine("Erro encontrado.");
}
finally
{
    Console.WriteLine("Finalizando operação.");
}
```

O `finally` é útil para liberar recursos ou registrar finalização.

Mesmo assim, em C# moderno, muitas vezes usamos `using` para liberar recursos automaticamente.

## 7. using para recursos descartáveis

Alguns objetos precisam ser fechados ou descartados depois do uso.

Exemplos:

- arquivos;
- conexões;
- streams;
- navegadores;
- recursos externos.

Exemplo:

```csharp
using StreamReader leitor = new StreamReader("dados.txt");

string conteudo = leitor.ReadToEnd();
```

Quando o escopo terminar, o recurso será liberado automaticamente.

Isso evita esquecer de fechar o arquivo manualmente.

## 8. Não engolir exceções

Um erro comum é capturar a exceção e não fazer nada.

Exemplo ruim:

```csharp
try
{
    int numero = int.Parse("abc");
}
catch
{
}
```

Esse código esconde o erro.

Quem estiver investigando não saberá o que aconteceu.

Melhor:

```csharp
try
{
    int numero = int.Parse("abc");
}
catch (FormatException ex)
{
    Console.WriteLine("Valor inválido.");
    Console.WriteLine(ex.Message);
}
```

Em sistemas reais, normalmente você registraria isso em log.

## 9. Quando usar try catch

Use `try catch` quando existe uma situação que pode falhar fora do controle direto do código.

Exemplos:

- ler arquivo;
- acessar banco;
- chamar API externa;
- converter entrada do usuário;
- processar dados de fonte externa;
- abrir conexão;
- executar automação em sistema instável.

Evite usar exceção para controlar fluxo normal.

Exemplo melhor para conversão:

```csharp
bool conseguiuConverter = int.TryParse("123", out int numero);

if (conseguiuConverter)
{
    Console.WriteLine(numero);
}
else
{
    Console.WriteLine("Número inválido.");
}
```

Quando existe um método seguro como `TryParse`, ele costuma ser melhor do que usar `try catch`.

## 10. throw

`throw` é usado para lançar uma exceção.

Exemplo:

```csharp
static void ValidarIdade(int idade)
{
    if (idade < 0)
    {
        throw new ArgumentException("A idade não pode ser negativa.");
    }
}
```

Uso:

```csharp
try
{
    ValidarIdade(-1);
}
catch (ArgumentException ex)
{
    Console.WriteLine(ex.Message);
}
```

Lançar exceção faz sentido quando o programa encontrou uma situação inválida que não deveria continuar normalmente.

## 11. Exemplo prático com arquivo

```csharp
try
{
    string caminho = "dados.txt";
    string conteudo = File.ReadAllText(caminho);

    Console.WriteLine(conteudo);
}
catch (FileNotFoundException)
{
    Console.WriteLine("Arquivo não encontrado.");
}
catch (UnauthorizedAccessException)
{
    Console.WriteLine("Sem permissão para acessar o arquivo.");
}
catch (IOException ex)
{
    Console.WriteLine("Erro de entrada ou saída.");
    Console.WriteLine(ex.Message);
}
```

Esse exemplo trata erros comuns de leitura de arquivo.

## 12. Exemplo em contexto backend

Em backend, tratamento de erro aparece em:

- leitura de configuração;
- conexão com banco;
- chamada de API externa;
- validação de dados;
- gravação de arquivo;
- envio de email;
- automações externas.

Exemplo simples:

```csharp
try
{
    Console.WriteLine("Enviando dados para sistema externo.");

    // Chamada para API, banco ou automação externa
}
catch (Exception ex)
{
    Console.WriteLine("Falha ao enviar dados.");
    Console.WriteLine(ex.Message);
}
```

Esse exemplo é genérico. Em código real, prefira capturar exceções mais específicas quando possível.

## 13. Boas práticas

Boas práticas:

- capture exceções específicas primeiro;
- deixe `catch (Exception)` por último;
- não esconda erros silenciosamente;
- registre informações úteis para investigação;
- não exponha detalhes sensíveis para o usuário final;
- use `finally` quando precisar garantir uma ação final;
- use `using` para recursos descartáveis;
- prefira métodos seguros, como `TryParse`, quando existirem;
- não use exceção para fluxo normal do programa.

## 14. Conclusão

`try catch` permite lidar com erros de forma controlada.

Ele não deve ser usado para esconder problemas.

Ele deve ajudar o sistema a reagir melhor quando algo inesperado acontece.

O ponto principal é:

```txt
Trate erros esperados de forma clara e registre informações suficientes para investigar problemas reais.
```

Antes de avançar, entenda bem:

- `try`;
- `catch`;
- múltiplos `catch`;
- `finally`;
- `throw`;
- `Exception`;
- exceções específicas;
- `using` para liberar recursos.
