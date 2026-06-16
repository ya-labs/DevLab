## Loops

Em C#, os loops (ou estruturas de repetição) executam um bloco de código repetidamente enquanto uma condição específica é atendida. Os quatro tipos principais são for, foreach, while e do-while.

# Loop "for"

Utilizado quando você sabe exatamente quantas vezes o loop deve rodar. Combina a inicialização, a condição e a atualização em uma única linha.

```csharp
for (int i = 0; i < 5; i++)
{
    Console.WriteLine($"Número: {i}");
}
```

# Loop "foreach"

A melhor opção para percorrer coleções (como listas e arrays), pois o C# gerencia a iteração automaticamente para cada item.

```csharp
string[] nomes = { "Ana", "Bruno", "Carlos" };
foreach (string nome in nomes)
{
    Console.WriteLine($"Olá, {nome}!");
}
```

# Loop "while"

Executa o bloco de código continuamente enquanto uma condição booleana for verdadeira. É ideal quando o número de repetições é imprevisível e depende de fatores dinâmicos.

```csharp
int contador = 0;
while (contador < 3)
{
    Console.WriteLine($"Contador: {contador}");
    contador++;
}
```

# Loop "do-while"

Semelhante ao while, mas garante que o bloco de código seja executado pelo menos uma vez, já que a condição é verificada apenas no final do ciclo.

```csharp
int numero = 5;
do
{
    Console.WriteLine($"Executando ao menos uma vez. Número: {numero}");
    numero--;
} while (numero > 0);
```

# Controle de Fluxo

Você também pode alterar o comportamento padrão dos loops usando duas palavras-chave:

break: Encerra o loop imediatamente.

continue: Pula a repetição atual e vai para a próxima.
