## Condicionais

Estruturas condicionais em C# permitem que o código tome decisões e altere seu fluxo com base em valores ou expressões. Os principais comandos são if/else, switch e o operador ternário, que avaliam resultados booleanos (verdadeiro ou falso).

# If

A estrutura if é uma das mais básicas e importantes. Ela é usada para executar um bloco de código se uma condição for verdadeira.

```csharp
bool estaInscrito = true;

if (estaInscrito)
{
    Console.WriteLine("Bem-vindo ao evento! Prepare-se para um aprendizado incrível.");
}
```

Neste exemplo, o código verifica se a variável estaInscrito é verdadeira. Se for, a mensagem “Bem-vindo ao evento! Prepare-se para um aprendizado intenso.” será exibida

# If-Else

Agora, e se quisermos executar algo quando a condição não for verdadeira? É aqui que entra o else.

```csharp
int horasDeEstudo = 5;

if (horasDeEstudo >= 7)
{
    Console.WriteLine("Parabéns! Você atingiu sua meta de estudos semanal.");
}
else
{
    Console.WriteLine("Continue se dedicando! Sua jornada de aprendizado está apenas começando.");
}
```

Se horasDeEstudo for menor que 7, a mensagem “Continue se dedicando! Sua jornada de aprendizado está apenas começando.” será exibida. Caso contrário, a mensagem “Parabéns! Você atingiu um ótimo nível de dedicação.” aparecerá.

# Else If

O else if permite verificar múltiplas condições em sequência, tornando-se ideal para avaliar diferentes cenários, como a escolha de uma trilha de aprendizado.

```csharp
string interesseDev = "C#";

if (interesseDev == "React Native")
{
    Console.WriteLine("Show de bola! A trilha de React Native é perfeita para quem quer desenvolver aplicativos móveis.");
}
else if (interesseDev == "C#")
{
    Console.WriteLine("C# é uma escolha poderosa para quem quer se aprofundar no back-end. Bora codar!");
}
else if (interesseDev == "React")
{
    Console.WriteLine("React é uma excelente opção para criar interfaces incríveis no front-end. Vamos juntos nessa jornada!");
}
else
{
    Console.WriteLine("Ainda não decidiu sua trilha? Sem problemas.");
}
```

Aqui, o código verifica o interesseDev e exibe uma mensagem de acordo com a escolha do desenvolvedor. Se o interesse for "React Native", a mensagem “Show de bola! A trilha de React Native é perfeita para quem quer desenvolver aplicativos móveis.” será exibida. Para "C#", incentivamos o aprendizado no back-end, e para "React", destacamos a importância de criar interfaces incríveis no front-end. Se o dev ainda estiver indeciso, informamos que não tem problema.

# Switch

O switch avalia uma variável ou expressão contra múltiplos valores possíveis (os cases). É ideal para substituir uma longa lista de if/else if quando se lida com opções fixas.

```csharp
string cargo = "Gerente";

switch (cargo) {
    case "Diretor":
        Console.WriteLine("Acesso total.");
        break;
    case "Gerente":
        Console.WriteLine("Acesso gerencial.");
        break;
    default:
        Console.WriteLine("Acesso padrão.");
        break;
}
```

# Operador Ternário

Uma forma simplificada e em uma única linha para escrever um if/else simples.

```csharp
int idade = 18;
string status = (idade >= 18) ? "Maior de idade" : "Menor de idade"; // Se for Maior ou igual a 18 retorna "Maior de idade", caso contrário retorna "Menor de idade"
Console.WriteLine(status);
```

# Quando usar qual estrutura condicional?

Use if-else: quando há uma ou algumas condições específicas a serem verificadas.

Use switch-case: quando você precisa verificar várias possibilidades de um mesmo valor.

Use o operador ternário ?:: para decisões simples e que não impactam na legibilidade do código.

# Desempenho e eficiência

Quando se trata de desempenho e eficiência no C#, é importante entender que o uso adequado de estruturas condicionais pode impactar significativamente a velocidade e a eficiência do seu código.
if-else vs switch-case: qual é mais eficiente?

    Múltiplos else if: Quando você usa uma sequência de múltiplos else if, o C# avalia as condições uma por uma até encontrar uma verdadeira. Se você tiver muitas condições a serem verificadas, especialmente se a condição verdadeira estiver no final da cadeia, o desempenho pode ser afetado, já que o programa precisa verificar cada condição até encontrar a certa.

    switch-case: Por outro lado, o switch-case é geralmente mais eficiente para lidar com múltiplas opções. Isso ocorre porque o C# utiliza internamente uma técnica de otimização, como a criação de tabelas de salto (jump tables) ou pesquisa binária, que permite encontrar o caso correspondente de maneira muito mais rápida, especialmente quando o número de casos é grande e os valores são constantes.

# Quando o switch-case é mais vantajoso?

O switch-case se torna mais vantajoso quando você está lidando com várias possibilidades de uma única variável e cada caso é um valor constante ou discreto. Por exemplo, se você estiver criando um menu de seleção para diferentes trilhas de aprendizado e precisar avaliar mais de 5 ou 6 opções, o switch-case será muito mais eficiente do que uma cadeia de else if.

# Limitações do switch-case

No entanto, vale lembrar que o switch-case não é adequado para todas as situações. Se você precisa avaliar expressões complexas ou condições que não são baseadas em valores constantes, a estrutura if-else ainda é a melhor opção. Além disso, se o número de casos for pequeno (por exemplo, 2 ou 3), a diferença de desempenho entre if-else e switch-case é praticamente insignificante.

# Conclusão

As estruturas condicionais são essenciais para qualquer desenvolvedor que deseja dominar a linguagem C#. Elas permitem que seu código tome decisões e execute ações diferentes dependendo das condições que você define, tornando suas aplicações muito mais dinâmicas e adaptáveis.