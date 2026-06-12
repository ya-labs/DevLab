## O que são váriaveis?

Em C#, as váriaveis são posições na memória reservadas para armazenar, pense nelas como caixas rotuladas onde você guarda informações (como textos, números ou valores lógicos) para usar e alterar quando precisar.

Toda váriavel em C# possui três caracteristicas essenciais:

Tipo: Define que tipo de dado ela pode guardar (ex: int para números inteiros, string para textos).

Nome: O identificador usado para referenciar e manipular o dado.

Valor: A informação real armazenada dentro da variável.

## Como declarar e usar as váriaveis?

No C#, você declara uma variável definindo primeiro o tipo, seguido pelo nome e atribuindo um valor usando o sinal de igual (=).

Exemplos práticos:

int idade = 25; (armazena um número inteiro)

string nome = "Carlos"; (armazena um texto)

double preco = 19.99; (armazena um número com casas decimais)

## Regras de nomeação

Para criar os nomes das suas variáveis, o C# exige que você siga algumas regras:

Não podem conter espaços ou começar com números.

Não use caracteres especiais (com exceção do underline \_).

O C# é sensível a maiúsculas e minúsculas (Case-sensitive), ou seja, idade e Idade são tratadas como variáveis diferentes.

## Tipos de váriavel

C# é uma linguagem de tipagem forte. Cada váriavel, constante e expressão tem um tipo. O compilador impõe a segurança do tipo verificando se cada operação em seu código é válida para os tipos envolvidos. Por exemplo, você pode adicionar dois int valores, mas não pode adicionar um int e um bool:

```csharp
int a = 5;
int b = a + 2; // OK

bool test = true;
```

## Tipos númericos

O C# tem tipos internos para inteiros, números de ponto flutuante e números decimais. Os tipos mais usados sãoint: doubledecimal

```csharp
int population = 67_000_000;
long distance = 384_400_000L;
short temperature = -40;
byte red = 255;

double pi = 3.141592653589793;
float gravity = 9.81f;
decimal price = 19.99m;
```

Cada tipo numérico tem um tamanho e um intervalo fixos. int armazena inteiros de 32 bits (cerca de ±2,1 bilhões), long armazena inteiros de 64 bits e short armazena byte valores menores.

Use double para matemática de ponto flutuante geral, float quando a memória é restrita e decimal quando você precisa de precisão decimal exata (como cálculos financeiros). Adicione o sufixo f para literais float e o sufixo m para literais decimal. Sem um sufixo, o compilador trata um número com um ponto decimal como double.

## Bool, char e string

Além dos números, o C# fornece outros três tipos internos usados com frequência:

```csharp
bool isValid = true;
char grade = 'A';
string greeting = "Hello, world!";
```

bool — Armazena true ou false. Use-o em condições, loops e expressões lógicas.
char — Armazena um único caractere Unicode (unidade de código UTF-16), entre aspas simples.
string — Armazena uma sequência de caracteres, entre aspas duplas. Cadeias de caracteres são imutáveis. Depois de criar uma cadeia de caracteres, você não poderá alterar seu conteúdo. As operações que parecem modificar uma cadeia de caracteres realmente criam uma nova.


## Var

A var palavra-chave instrui o compilador a inferir o tipo de uma variável local a partir de seu inicializador.

```csharp
bool isValid = true;
char grade = 'A';
string greeting = "Hello, world!";
```

A variável ainda é fortemente tipada; var não a torna dinâmica. O compilador determina o tipo em tempo de compilação e impõe a segurança do tipo como de costume. Use var quando o tipo for óbvio do lado direito para reduzir o ruído visual. Explicite o tipo quando ele torna o código mais claro.