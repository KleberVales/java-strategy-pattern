# Padrão de Projeto: Strategy em Java
Vou implementar o padrão Strategy para demonstrar como encapsular diferentes algoritmos e torná-los intercambiáveis. Este padrão é útil quando você precisa variar o comportamento de um objeto em tempo de execução.

## Implementação do Padrão Strategy

1.  Interface Strategy (Comportamento)
```
// StrategyInterface.java
public interface PaymentStrategy {
    void pay(double amount);
}
```
2. Implementações Concretas (Estratégias)
```
// CreditCardPayment.java
public class CreditCardPayment implements PaymentStrategy {
    private String name;
    private String cardNumber;
    private String cvv;
    private String expirationDate;
    
    public CreditCardPayment(String name, String cardNumber, String cvv, String expirationDate) {
        this.name = name;
        this.cardNumber = cardNumber;
        this.cvv = cvv;
        this.expirationDate = expirationDate;
    }
    
    @Override
    public void pay(double amount) {
        System.out.println(amount + " pago com cartão de crédito (" + cardNumber.substring(cardNumber.length() - 4) + ")");
    }
}
```
