## Operadores

Os operadores em C# são símbolos especiais usados para manipular variáveis, realizar cálculos e avaliar condições. Eles são divididos em categorias essenciais, como aritméticos, de atribuição, relacionais, lógicos e operadores de nulos.

# Operadores Aritméticos

Usados para realizar cálculos matemáticos

+ = Adição
- = Subtração
* = Multiplicação
/ = Divisão
% = Módulo (Resto)

# Operadores de Atribuição

= Exemplo: x = 5;

+= = Exemplo x += 5; Equivalente a: x = x + 5;

-= = Exemplo x -= 5; Equivalente a: x = x - 5;

++ = Exemplo x++; Equivalente a x = x + 1;

-- = Exemplo x--; Equivalente a x = x - 1;

## Operadores Relacionais (Comparação)

Usados para comparar dois valores, sempre retornando um valor booleano (true ou false).

x = 5;

y = 6;

== Igual a / Exemplo: x == y // False

!= Diferente de / Exemplo: x != y // True

> Maior que / Exemplo = x > y // False

< Menor que / Exemplo = x < y // True

>= Maior ou igual / Exemplo = x >= y // False

<= Menor ou igual / Exemplo = x <= y // True

## Operadores Lógicos

Usados para combinar múltiplas condições booleanas.

x = 5;
y = 9;

&& = E ou AND - Retorna true se ambas as condições forem verdadeiras // Exemplo: (x > 5) && (y < 10) // False

|| = Ou - Retorna true se pelo menos uma das condições for verdadeira // Exemplo: (x > 5) || (y < 10) // True, pois y é menor que 10

! = Não/NOT - Inverte o valor lógico // Exemplo = !(x > 5) // True pois x não(NOT) é maior que 5

## Operadores Especiais de Nulos

Extremamente úteis para lidar com valores nulos (null) em C#.

?? = Coalescência Nula: Retorna o operando esquerdo se não for nulo; caso contrário, retorna o direito. // Exemplo: string nome = usuario ?? "Anônimo";

?. = Propagação Nula: Só acessa o membro ou método se o objeto não for nulo. // Exemplo: int? comprimento = texto?.Length;