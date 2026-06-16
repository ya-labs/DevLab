# Encapsulamento

## 1. O que é encapsulamento

Encapsulamento é um princípio da programação orientada a objetos usado para proteger os dados de uma classe.

A ideia é simples:

```txt
Nem tudo que existe dentro de uma classe deve ser alterado diretamente por fora.
```

Em vez de expor todos os dados livremente, a classe controla como esses dados podem ser lidos e modificados.

Isso ajuda a manter regras importantes em um único lugar.

## 2. O problema de expor dados diretamente

Exemplo ruim:

```csharp
class ContaBancaria
{
    public decimal Saldo;
}
```

Uso:

```csharp
ContaBancaria conta = new ContaBancaria();

conta.Saldo = -100;
```

Esse código permite colocar saldo negativo diretamente.

O problema não é apenas técnico. O problema é de regra de negócio.

Uma conta não deveria aceitar qualquer alteração direta no saldo.

## 3. Protegendo dados com private

Podemos esconder o campo usando `private`.

Exemplo:

```csharp
class ContaBancaria
{
    private decimal saldo;
}
```

Agora `saldo` só pode ser acessado dentro da própria classe.

Isso impede que outro código faça:

```csharp
conta.saldo = -100;
```

O campo está protegido.

## 4. Expondo comportamento controlado

Depois de proteger o campo, criamos métodos para controlar as alterações.

Exemplo:

```csharp
class ContaBancaria
{
    private decimal saldo;

    public decimal Saldo
    {
        get { return saldo; }
    }

    public void Depositar(decimal valor)
    {
        if (valor <= 0)
        {
            Console.WriteLine("O valor do depósito deve ser maior que zero.");
            return;
        }

        saldo += valor;
    }
}
```

Agora o saldo pode ser lido, mas não pode ser alterado diretamente por fora.

Uso:

```csharp
ContaBancaria conta = new ContaBancaria();

conta.Depositar(200);

Console.WriteLine(conta.Saldo);
```

Esse formato protege a regra:

```txt
Só é possível aumentar o saldo usando Depositar.
```

## 5. get e set

Propriedades em C# podem ter `get` e `set`.

Exemplo:

```csharp
class Produto
{
    public string Nome { get; set; } = "";
}
```

`get` permite ler o valor.

`set` permite alterar o valor.

Uso:

```csharp
Produto produto = new Produto();

produto.Nome = "Teclado";

Console.WriteLine(produto.Nome);
```

Esse formato é comum quando a propriedade pode ser lida e alterada sem regra especial.

## 6. set privado

Às vezes, queremos permitir leitura pública, mas alteração apenas dentro da classe.

Exemplo:

```csharp
class Pedido
{
    public string Status { get; private set; } = "Pendente";

    public void Aprovar()
    {
        Status = "Aprovado";
    }
}
```

Uso:

```csharp
Pedido pedido = new Pedido();

pedido.Aprovar();

Console.WriteLine(pedido.Status);
```

O código de fora consegue ler `Status`, mas não consegue alterar diretamente.

Isso evita algo assim:

```csharp
pedido.Status = "Qualquer coisa";
```

## 7. Encapsulamento com validação

Também podemos validar valores dentro da propriedade.

Exemplo:

```csharp
class Produto
{
    private decimal preco;

    public decimal Preco
    {
        get { return preco; }
        set
        {
            if (value <= 0)
            {
                Console.WriteLine("O preço deve ser maior que zero.");
                return;
            }

            preco = value;
        }
    }
}
```

Uso:

```csharp
Produto produto = new Produto();

produto.Preco = -10;
produto.Preco = 100;

Console.WriteLine(produto.Preco);
```

O `set` controla o que pode entrar na propriedade.

## 8. Quando usar métodos em vez de set

Nem toda alteração deve ser feita com `set`.

Algumas ações representam comportamentos de negócio.

Exemplo:

```csharp
class ContaBancaria
{
    public decimal Saldo { get; private set; }

    public void Depositar(decimal valor)
    {
        if (valor <= 0)
        {
            return;
        }

        Saldo += valor;
    }

    public void Sacar(decimal valor)
    {
        if (valor <= 0 || valor > Saldo)
        {
            return;
        }

        Saldo -= valor;
    }
}
```

Esse modelo é melhor do que permitir:

```csharp
conta.Saldo = 999999;
```

Porque depósito e saque são ações com regras.

## 9. Modificadores de acesso

Encapsulamento usa bastante modificadores de acesso.

Os principais:

- `public`: acessível por fora;
- `private`: acessível apenas dentro da própria classe;
- `protected`: acessível pela classe e por classes derivadas;
- `internal`: acessível dentro do mesmo projeto.

No começo, foque principalmente em:

```txt
public -> aquilo que outras partes do código podem usar.
private -> detalhe interno da classe.
```

## 10. Boas práticas

Boas práticas de encapsulamento:

- evite campos públicos;
- exponha propriedades apenas quando fizer sentido;
- use `private set` quando o valor não deve ser alterado livremente;
- use métodos para ações com regra de negócio;
- mantenha validações próximas dos dados que elas protegem;
- não deixe qualquer parte do sistema alterar estados importantes sem controle.

## 11. Conclusão

Encapsulamento serve para proteger os dados e organizar regras dentro da classe correta.

O objetivo não é esconder por esconder.

O objetivo é evitar alterações indevidas e manter o objeto em um estado válido.

Na prática:

- dados internos ficam privados;
- acesso externo acontece por propriedades ou métodos;
- regras importantes ficam dentro da classe;
- o código fica mais seguro e mais fácil de manter.
