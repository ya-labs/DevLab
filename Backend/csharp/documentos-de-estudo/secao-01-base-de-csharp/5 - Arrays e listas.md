# Arrays e listas

## 1. O que são coleções

Coleções são estruturas usadas para guardar vários valores em uma única variável.

Em vez de criar várias variáveis separadas:

```csharp
string nome1 = "Ana";
string nome2 = "Bruno";
string nome3 = "Carla";
```

Você pode guardar os valores em uma coleção:

```csharp
string[] nomes = { "Ana", "Bruno", "Carla" };
```

Isso facilita quando você precisa trabalhar com listas de dados, como:

- nomes de usuários;
- produtos;
- pedidos;
- notas;
- mensagens;
- registros vindos de um banco de dados.

Em C#, duas coleções muito comuns no começo são:

- array;
- `List<T>`.

## 2. O que é um array

Um array é uma coleção de elementos do mesmo tipo com tamanho fixo.

Exemplo:

```csharp
int[] numeros = new int[3];

numeros[0] = 10;
numeros[1] = 20;
numeros[2] = 30;
```

Esse array possui 3 posições.

Os índices começam em `0`, não em `1`.

```txt
Índice 0 -> 10
Índice 1 -> 20
Índice 2 -> 30
```

Para acessar um valor:

```csharp
Console.WriteLine(numeros[1]);
```

Saída:

```txt
20
```

## 3. Criando array com valores

Você também pode criar um array já preenchido:

```csharp
string[] nomes = { "Ana", "Bruno", "Carla" };

Console.WriteLine(nomes[0]);
```

Saída:

```txt
Ana
```

Nesse caso, o C# entende que o array possui 3 elementos.

## 4. Length

Para saber o tamanho de um array, use `Length`.

Exemplo:

```csharp
string[] nomes = { "Ana", "Bruno", "Carla" };

Console.WriteLine(nomes.Length);
```

Saída:

```txt
3
```

`Length` mostra quantos elementos cabem no array.

Como o array tem tamanho fixo, esse tamanho não aumenta automaticamente.

## 5. Erro comum com índice

Um erro comum é tentar acessar uma posição que não existe.

Exemplo:

```csharp
string[] nomes = { "Ana", "Bruno", "Carla" };

Console.WriteLine(nomes[3]);
```

Esse código gera erro, porque o array tem os índices:

```txt
0, 1, 2
```

O índice `3` não existe.

Esse erro é conhecido como acesso fora do limite da coleção.

## 6. Percorrendo array com foreach

Para percorrer todos os valores de um array, use `foreach`.

Exemplo:

```csharp
string[] nomes = { "Ana", "Bruno", "Carla" };

foreach (string nome in nomes)
{
    Console.WriteLine(nome);
}
```

Saída:

```txt
Ana
Bruno
Carla
```

O `foreach` passa por cada item da coleção.

Use esse formato quando você não precisa controlar o índice manualmente.

## 7. O que é uma lista

`List<T>` é uma coleção que pode crescer ou diminuir durante a execução do programa.

Diferente do array, você não precisa definir o tamanho final logo no começo.

Exemplo:

```csharp
List<string> nomes = new List<string>();

nomes.Add("Ana");
nomes.Add("Bruno");
nomes.Add("Carla");
```

Nesse exemplo, `List<string>` significa:

```txt
Uma lista de strings.
```

O `T` em `List<T>` representa o tipo dos elementos da lista.

Exemplos:

```csharp
List<int> numeros = new List<int>();
List<string> nomes = new List<string>();
List<double> precos = new List<double>();
```

## 8. Count

Para saber quantos elementos existem em uma lista, use `Count`.

Exemplo:

```csharp
List<string> nomes = new List<string>();

nomes.Add("Ana");
nomes.Add("Bruno");

Console.WriteLine(nomes.Count);
```

Saída:

```txt
2
```

Em arrays, usamos `Length`.

Em listas, usamos `Count`.

## 9. Métodos comuns de List

Alguns métodos comuns:

- `Add`: adiciona um item;
- `Remove`: remove um item pelo valor;
- `RemoveAt`: remove um item pelo índice;
- `Contains`: verifica se um valor existe;
- `Clear`: remove todos os itens;
- `IndexOf`: retorna o índice de um valor.

Exemplo:

```csharp
List<string> nomes = new List<string>();

nomes.Add("Ana");
nomes.Add("Bruno");
nomes.Add("Carla");

nomes.Remove("Bruno");

Console.WriteLine(nomes.Count);
```

Saída:

```txt
2
```

Depois da remoção, a lista fica com:

```txt
Ana
Carla
```

## 10. Percorrendo lista

Também podemos usar `foreach` em listas.

Exemplo:

```csharp
List<string> nomes = new List<string>();

nomes.Add("Ana");
nomes.Add("Bruno");
nomes.Add("Carla");

foreach (string nome in nomes)
{
    Console.WriteLine(nome);
}
```

O funcionamento é parecido com o array.

## 11. Quando usar array

Use array quando:

- a quantidade de itens é fixa;
- o tamanho já é conhecido;
- você não precisa adicionar ou remover itens depois;
- quer uma estrutura simples.

Exemplo:

```csharp
string[] diasDaSemana =
{
    "Domingo",
    "Segunda",
    "Terça",
    "Quarta",
    "Quinta",
    "Sexta",
    "Sábado"
};
```

Os dias da semana não mudam durante a execução do programa.

Nesse caso, array faz sentido.

## 12. Quando usar List

Use `List<T>` quando:

- a quantidade de itens pode mudar;
- você precisa adicionar elementos;
- você precisa remover elementos;
- os dados vêm de entrada do usuário, API ou banco;
- precisa manipular a coleção com mais flexibilidade.

Exemplo:

```csharp
List<string> tarefas = new List<string>();

tarefas.Add("Estudar C#");
tarefas.Add("Praticar loops");
tarefas.Add("Revisar listas");
```

Nesse caso, uma lista é melhor porque novas tarefas podem ser adicionadas depois.

## 13. Comparação rápida

```txt
Array:
- tamanho fixo;
- usa Length;
- bom quando a quantidade não muda.

List:
- tamanho dinâmico;
- usa Count;
- boa quando precisa adicionar ou remover itens.
```

## 14. Conclusão

Arrays e listas servem para armazenar vários valores.

O array é mais simples e tem tamanho fixo.

A lista é mais flexível e pode crescer ou diminuir.

Na prática, em aplicações C#, `List<T>` aparece com muita frequência porque sistemas reais trabalham com dados que mudam: usuários, produtos, pedidos, tarefas e resultados de consultas.

Antes de avançar, é importante dominar:

- índices;
- `Length`;
- `Count`;
- `foreach`;
- `Add`;
- `Remove`;
- diferença entre array e lista.
