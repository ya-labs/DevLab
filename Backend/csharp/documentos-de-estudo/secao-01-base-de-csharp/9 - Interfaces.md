# Interfaces

## 1. O que é uma interface

Uma interface é um contrato.

Ela define o que uma classe deve fazer, mas não precisa definir exatamente como essa classe vai fazer.

Exemplo:

```csharp
public interface INotificador
{
    void Enviar(string mensagem);
}
```

Essa interface diz:

```txt
Quem implementar INotificador precisa ter um método Enviar.
```

Ela não diz se a mensagem será enviada por email, SMS, WhatsApp ou outro meio.

## 2. Implementando uma interface

Uma classe implementa uma interface usando `:`.

Exemplo:

```csharp
public class NotificadorEmail : INotificador
{
    public void Enviar(string mensagem)
    {
        Console.WriteLine($"Enviando email: {mensagem}");
    }
}
```

Essa classe cumpre o contrato porque possui o método:

```csharp
public void Enviar(string mensagem)
```

O nome, retorno e parâmetros precisam combinar com o que a interface exige.

## 3. Exemplo com mais de uma implementação

Interfaces são úteis quando diferentes classes compartilham o mesmo comportamento, mas cada uma executa de um jeito.

Exemplo:

```csharp
public interface INotificador
{
    void Enviar(string mensagem);
}

public class NotificadorEmail : INotificador
{
    public void Enviar(string mensagem)
    {
        Console.WriteLine($"Email enviado: {mensagem}");
    }
}

public class NotificadorSms : INotificador
{
    public void Enviar(string mensagem)
    {
        Console.WriteLine($"SMS enviado: {mensagem}");
    }
}
```

As duas classes implementam `INotificador`.

Mas cada uma envia a mensagem de um jeito.

## 4. Usando a interface como tipo

Uma vantagem importante é poder usar a interface como tipo.

Exemplo:

```csharp
INotificador notificador = new NotificadorEmail();

notificador.Enviar("Pedido aprovado.");
```

Também poderíamos trocar a implementação:

```csharp
INotificador notificador = new NotificadorSms();

notificador.Enviar("Pedido aprovado.");
```

O código continua chamando `Enviar`.

O que muda é a classe concreta usada por trás.

## 5. Por que interfaces existem

Interfaces ajudam a reduzir acoplamento.

Acoplamento é quando uma parte do código depende demais de uma implementação específica.

Exemplo mais acoplado:

```csharp
public class PedidoService
{
    private readonly NotificadorEmail notificador = new NotificadorEmail();

    public void AprovarPedido()
    {
        notificador.Enviar("Pedido aprovado.");
    }
}
```

Aqui `PedidoService` depende diretamente de `NotificadorEmail`.

Se quiser trocar para SMS, precisa alterar a classe.

Com interface:

```csharp
public class PedidoService
{
    private readonly INotificador notificador;

    public PedidoService(INotificador notificador)
    {
        this.notificador = notificador;
    }

    public void AprovarPedido()
    {
        notificador.Enviar("Pedido aprovado.");
    }
}
```

Agora `PedidoService` depende do contrato, não da implementação.

## 6. Exemplo completo

```csharp
public interface IForma
{
    double CalcularArea();
}

public class Circulo : IForma
{
    public double Raio { get; set; }

    public double CalcularArea()
    {
        return Math.PI * Raio * Raio;
    }
}

public class Quadrado : IForma
{
    public double Lado { get; set; }

    public double CalcularArea()
    {
        return Lado * Lado;
    }
}
```

Uso:

```csharp
IForma forma = new Circulo();

forma.CalcularArea();
```

O código sabe que `forma` tem o método `CalcularArea`, porque isso está no contrato da interface.

## 7. Convenção de nome

Em C#, interfaces normalmente começam com a letra `I`.

Exemplos:

```csharp
INotificador
IRepositorio
IForma
IClienteService
```

Essa é uma convenção muito comum no ecossistema .NET.

## 8. Interface não é classe base

Uma classe pode herdar de apenas uma classe base, mas pode implementar várias interfaces.

Exemplo:

```csharp
public interface IImprimivel
{
    void Imprimir();
}

public interface IExportavel
{
    void Exportar();
}

public class Relatorio : IImprimivel, IExportavel
{
    public void Imprimir()
    {
        Console.WriteLine("Imprimindo relatório.");
    }

    public void Exportar()
    {
        Console.WriteLine("Exportando relatório.");
    }
}
```

Isso permite combinar contratos diferentes em uma mesma classe.

## 9. Interfaces no backend

Em backend com C#, interfaces aparecem bastante em:

- services;
- repositories;
- validações;
- notificadores;
- integrações externas;
- envio de email;
- logs;
- testes automatizados.

Exemplo:

```csharp
public interface IClienteRepository
{
    Cliente? BuscarPorId(int id);
    void Salvar(Cliente cliente);
}
```

Essa interface define o que um repositório de clientes precisa fazer.

A implementação pode usar banco de dados, arquivo, memória ou outra fonte.

## 10. Boas práticas

Boas práticas com interfaces:

- use interface quando existir mais de uma implementação possível;
- use interface para separar contrato de implementação;
- não crie interface para tudo sem necessidade;
- nomeie interfaces com `I` no começo;
- mantenha contratos simples;
- evite interfaces grandes demais;
- use nomes que representem comportamento.

Exemplo ruim:

```csharp
public interface IClasseCliente
{
}
```

Exemplo melhor:

```csharp
public interface IClienteRepository
{
    Cliente? BuscarPorId(int id);
}
```

## 11. Conclusão

Interface é um contrato.

Ela define quais membros uma classe precisa implementar.

O principal benefício é permitir que o código dependa de uma abstração, não de uma classe concreta.

Isso deixa o sistema mais flexível, mais fácil de testar e mais fácil de modificar.

Antes de avançar, entenda bem:

- interface define contrato;
- classe implementa contrato;
- o nome da implementação precisa bater com o contrato;
- interfaces ajudam a reduzir acoplamento;
- uma classe pode implementar várias interfaces.
