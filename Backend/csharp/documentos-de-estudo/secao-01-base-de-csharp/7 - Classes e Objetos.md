# Classes e objetos

## 1. O que é uma classe

Uma classe é um molde usado para criar objetos.

Ela define quais dados e comportamentos um objeto pode ter.

Exemplo simples:

```csharp
class Carro
{
    public string Cor { get; set; } = "";

    public void Buzinar()
    {
        Console.WriteLine("Bip!");
    }
}
```

Nesse exemplo, `Carro` é uma classe.

Ela define:

- uma propriedade chamada `Cor`;
- um método chamado `Buzinar`.

## 2. O que é um objeto

Um objeto é uma instância criada a partir de uma classe.

Se a classe é o molde, o objeto é algo criado com base nesse molde.

Exemplo:

```csharp
Carro meuCarro = new Carro();

meuCarro.Cor = "Vermelho";
meuCarro.Buzinar();
```

Aqui:

```txt
Carro -> classe
meuCarro -> objeto
new Carro() -> criação da instância
```

## 3. Por que classes existem

Classes existem para organizar dados e comportamentos relacionados.

Sem classe, o código pode ficar solto e difícil de manter.

Exemplo com dados soltos:

```csharp
string nomeCliente = "Ana";
string emailCliente = "ana@example.com";
bool clienteAtivo = true;
```

Com classe:

```csharp
class Cliente
{
    public string Nome { get; set; } = "";
    public string Email { get; set; } = "";
    public bool Ativo { get; set; }
}
```

Agora esses dados fazem parte de um mesmo conceito: `Cliente`.

## 4. Criando objetos

Exemplo:

```csharp
Cliente cliente = new Cliente();

cliente.Nome = "Ana";
cliente.Email = "ana@example.com";
cliente.Ativo = true;
```

Esse código cria um objeto `Cliente` e preenche suas propriedades.

Depois, você pode usar os dados:

```csharp
Console.WriteLine(cliente.Nome);
Console.WriteLine(cliente.Email);
```

## 5. Vários objetos da mesma classe

Uma classe pode gerar vários objetos.

Exemplo:

```csharp
Cliente cliente1 = new Cliente();
cliente1.Nome = "Ana";

Cliente cliente2 = new Cliente();
cliente2.Nome = "Bruno";

Console.WriteLine(cliente1.Nome);
Console.WriteLine(cliente2.Nome);
```

Saída:

```txt
Ana
Bruno
```

Os dois objetos foram criados a partir da mesma classe, mas cada um possui seus próprios dados.

## 6. Propriedades

Propriedades representam dados de uma classe.

Exemplo:

```csharp
class Produto
{
    public string Nome { get; set; } = "";
    public decimal Preco { get; set; }
}
```

Uso:

```csharp
Produto produto = new Produto();

produto.Nome = "Teclado";
produto.Preco = 150.00m;
```

`Nome` e `Preco` são propriedades.

Elas guardam o estado do objeto.

## 7. Métodos

Métodos representam ações ou comportamentos.

Exemplo:

```csharp
class Produto
{
    public string Nome { get; set; } = "";
    public decimal Preco { get; set; }

    public void ExibirResumo()
    {
        Console.WriteLine($"{Nome} - {Preco}");
    }
}
```

Uso:

```csharp
Produto produto = new Produto();

produto.Nome = "Mouse";
produto.Preco = 80.00m;

produto.ExibirResumo();
```

O método usa os dados do próprio objeto.

## 8. Construtor

Construtor é um método especial executado quando o objeto é criado.

Exemplo:

```csharp
class Cliente
{
    public string Nome { get; set; }
    public string Email { get; set; }

    public Cliente(string nome, string email)
    {
        Nome = nome;
        Email = email;
    }
}
```

Uso:

```csharp
Cliente cliente = new Cliente("Ana", "ana@example.com");
```

O construtor obriga a criação do cliente com nome e email.

Isso evita criar objetos incompletos.

## 9. Classe Program e outras classes

Em projetos C#, é comum ter uma classe principal que inicia a aplicação e outras classes que representam conceitos do sistema.

Exemplo:

```csharp
class Program
{
    static void Main()
    {
        Cliente cliente = new Cliente("Ana", "ana@example.com");

        Console.WriteLine(cliente.Nome);
    }
}

class Cliente
{
    public string Nome { get; set; }
    public string Email { get; set; }

    public Cliente(string nome, string email)
    {
        Nome = nome;
        Email = email;
    }
}
```

Em projetos maiores, cada classe costuma ficar em seu próprio arquivo.

Exemplo:

```txt
Program.cs
Cliente.cs
Produto.cs
Pedido.cs
```

## 10. Classes no uso real

Em sistemas backend, classes aparecem para representar:

- entidades;
- serviços;
- configurações;
- requisições;
- respostas;
- regras de negócio.

Exemplo:

```csharp
class Pedido
{
    public int Id { get; set; }
    public string Cliente { get; set; } = "";
    public decimal Total { get; set; }
}
```

Essa classe poderia representar um pedido dentro do sistema.

## 11. Boas práticas

Boas práticas para classes:

- use nomes no singular, como `Cliente`, `Produto`, `Pedido`;
- use nomes claros para propriedades;
- coloque comportamentos relacionados dentro da classe;
- evite classes que fazem coisas demais;
- crie construtores quando o objeto precisa nascer com dados obrigatórios;
- evite deixar regra de negócio espalhada pelo programa.

## 12. Conclusão

Classes e objetos são a base da programação orientada a objetos em C#.

A classe define o molde.

O objeto é a instância criada a partir desse molde.

Propriedades guardam dados.

Métodos executam ações.

Construtores ajudam a criar objetos de forma correta.

Entender classes é essencial para estudar encapsulamento, interfaces, serviços, entidades e APIs em C#.
