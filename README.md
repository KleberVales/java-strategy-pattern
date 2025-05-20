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
