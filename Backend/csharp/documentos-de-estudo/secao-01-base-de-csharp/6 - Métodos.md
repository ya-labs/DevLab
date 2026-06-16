# Funções e métodos

## 1. O que são funções

Funções são blocos de código criados para executar uma tarefa específica.

Elas ajudam a organizar o programa e evitam repetição.

Exemplo sem função:

```csharp
Console.WriteLine("Olá, Nicolas!");
Console.WriteLine("Bem-vindo ao sistema.");

Console.WriteLine("Olá, Ana!");
Console.WriteLine("Bem-vinda ao sistema.");
```

Existe repetição.

Podemos criar um método para resolver isso.

```csharp
static void MostrarMensagem(string nome)
{
    Console.WriteLine($"Olá, {nome}!");
    Console.WriteLine("Bem-vindo ao sistema.");
}
```

Agora podemos reutilizar:

```csharp
MostrarMensagem("Nicolas");
MostrarMensagem("Ana");
```

## 2. Função ou método

No C#, o termo mais comum é método.

Um método é uma função que pertence a uma classe.

Exemplo:

```csharp
class Program
{
    static void MostrarMensagem()
    {
        Console.WriteLine("Olá!");
    }
}
```

`MostrarMensagem` é um método da classe `Program`.

Em estudos iniciantes, é comum usar os dois termos, mas tecnicamente em C# quase sempre falamos em métodos.

## 3. Estrutura de um método

Um método pode ter:

- modificador de acesso;
- tipo de retorno;
- nome;
- parâmetros;
- bloco de código.

Exemplo:

```csharp
public int Somar(int numero1, int numero2)
{
    return numero1 + numero2;
}
```

Partes:

```txt
public -> quem pode acessar
int -> tipo de retorno
Somar -> nome do método
int numero1, int numero2 -> parâmetros
return numero1 + numero2 -> valor devolvido
```

## 4. Método sem retorno

Quando um método não devolve valor, usamos `void`.

Exemplo:

```csharp
static void MostrarNome(string nome)
{
    Console.WriteLine(nome);
}
```

Esse método apenas executa uma ação.

Ele não retorna um valor para quem chamou.

Uso:

```csharp
MostrarNome("Nicolas");
```

## 5. Método com retorno

Quando um método devolve um valor, informamos o tipo antes do nome.

Exemplo:

```csharp
static int Somar(int numero1, int numero2)
{
    return numero1 + numero2;
}
```

Uso:

```csharp
int resultado = Somar(10, 5);

Console.WriteLine(resultado);
```

Saída:

```txt
15
```

O tipo do valor retornado precisa combinar com o tipo declarado.

Se o método diz que retorna `int`, ele precisa retornar um `int`.

## 6. Parâmetros

Parâmetros são valores que o método recebe para trabalhar.

Exemplo:

```csharp
static void ExibirProduto(string nome, decimal preco)
{
    Console.WriteLine($"Produto: {nome}");
    Console.WriteLine($"Preço: {preco}");
}
```

Uso:

```csharp
ExibirProduto("Teclado", 150.00m);
```

Nesse caso:

```txt
nome recebe "Teclado"
preco recebe 150.00
```

## 7. Argumentos nomeados

Ao chamar um método, você pode informar o nome dos parâmetros.

Exemplo:

```csharp
ExibirProduto(nome: "Mouse", preco: 80.00m);
```

Isso melhora a leitura quando o método tem vários parâmetros.

Também ajuda a evitar confusão com valores parecidos.

## 8. Parâmetro opcional

Um parâmetro pode ter valor padrão.

Exemplo:

```csharp
static void CriarUsuario(string nome, bool ativo = true)
{
    Console.WriteLine($"Nome: {nome}");
    Console.WriteLine($"Ativo: {ativo}");
}
```

Uso omitindo o parâmetro opcional:

```csharp
CriarUsuario("Nicolas");
```

Nesse caso, `ativo` será `true`.

Uso informando o valor:

```csharp
CriarUsuario("Nicolas", false);
```

## 9. return em método void

Mesmo em um método `void`, você pode usar `return` para encerrar a execução mais cedo.

Exemplo:

```csharp
static void EnviarEmail(string email)
{
    if (string.IsNullOrWhiteSpace(email))
    {
        Console.WriteLine("Email inválido.");
        return;
    }

    Console.WriteLine("Email enviado.");
}
```

Nesse caso, se o email estiver vazio, o método termina antes de tentar enviar.

## 10. Métodos static

Um método `static` pertence à classe, não a um objeto específico.

Exemplo:

```csharp
class Calculadora
{
    public static int Somar(int numero1, int numero2)
    {
        return numero1 + numero2;
    }
}
```

Uso:

```csharp
int resultado = Calculadora.Somar(2, 3);
```

Você não precisa criar um objeto `Calculadora`.

Métodos `static` são úteis quando a ação não depende do estado de um objeto.

## 11. Métodos de instância

Métodos de instância pertencem a um objeto.

Exemplo:

```csharp
class Pessoa
{
    public string Nome { get; set; } = "";

    public void Apresentar()
    {
        Console.WriteLine($"Olá, meu nome é {Nome}.");
    }
}
```

Uso:

```csharp
Pessoa pessoa = new Pessoa();
pessoa.Nome = "Nicolas";
pessoa.Apresentar();
```

Nesse caso, o método usa o estado do objeto.

O valor de `Nome` pertence à instância `pessoa`.

## 12. Modificadores de acesso

Modificadores de acesso controlam quem pode usar um método.

Os mais comuns no começo são:

- `public`: pode ser acessado de fora da classe;
- `private`: só pode ser acessado dentro da própria classe;
- `protected`: pode ser acessado pela classe e por classes filhas;
- `internal`: pode ser acessado dentro do mesmo projeto.

Exemplo:

```csharp
class Conta
{
    public void Depositar(decimal valor)
    {
        RegistrarMovimentacao(valor);
    }

    private void RegistrarMovimentacao(decimal valor)
    {
        Console.WriteLine($"Movimentação registrada: {valor}");
    }
}
```

`Depositar` é público.

`RegistrarMovimentacao` é privado, porque é um detalhe interno da classe.

## 13. Boas práticas

Boas práticas para métodos:

- use nomes claros;
- crie métodos pequenos;
- evite métodos que fazem muitas coisas;
- use parâmetros apenas quando necessário;
- retorne valor quando quem chama precisa do resultado;
- use `void` quando o método apenas executa uma ação;
- prefira `private` para detalhes internos;
- evite repetir código.

Exemplo de nome ruim:

```csharp
void Fazer()
{
}
```

Exemplo melhor:

```csharp
void EnviarEmailDeConfirmacao()
{
}
```

## 14. Sobre delegates, Action e Func

`Action`, `Func` e delegates são recursos importantes do C#, mas não precisam ser aprofundados neste documento.

Eles são formas de guardar ou passar funções como valores.

Esse assunto é mais avançado e combina melhor com um documento próprio depois de classes, interfaces e LINQ.

Aqui, o mais importante é entender bem:

- método com retorno;
- método sem retorno;
- parâmetros;
- `return`;
- `static`;
- método de instância;
- modificadores de acesso.

## 15. Conclusão

Métodos existem para organizar o código em blocos reutilizáveis.

Eles ajudam a deixar o programa mais claro, reduzem repetição e separam responsabilidades.

Na prática, você usa métodos quando quer nomear uma ação do sistema.

Exemplos:

```csharp
CalcularTotal();
SalvarCliente();
ValidarEmail();
EnviarMensagem();
```

Um bom método deve deixar claro o que faz.
