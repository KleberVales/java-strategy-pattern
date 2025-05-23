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
```
// PayPalPayment.java
public class PayPalPayment implements PaymentStrategy {
    private String email;
    private String password;
    
    public PayPalPayment(String email, String password) {
        this.email = email;
        this.password = password;
    }
    
    @Override
    public void pay(double amount) {
        System.out.println(amount + " pago via PayPal usando o email " + email);
    }
}
```
```
// BankTransferPayment.java
public class BankTransferPayment implements PaymentStrategy {
    private String accountNumber;
    private String bankCode;
    
    public BankTransferPayment(String accountNumber, String bankCode) {
        this.accountNumber = accountNumber;
        this.bankCode = bankCode;
    }
    
    @Override
    public void pay(double amount) {
        System.out.println(amount + " pago via transferência bancária para conta " + accountNumber);
    }
}
```
3. Contexto que usa a Strategy3
```
// ShoppingCart.java
public class ShoppingCart {
    private List<Item> items;
    private PaymentStrategy paymentStrategy;
    
    public ShoppingCart() {
        this.items = new ArrayList<>();
    }
    
    public void addItem(Item item) {
        items.add(item);
    }
    
    public void removeItem(Item item) {
        items.remove(item);
    }
    
    public double calculateTotal() {
        return items.stream().mapToDouble(Item::getPrice).sum();
    }
    
    public void setPaymentStrategy(PaymentStrategy paymentStrategy) {
        this.paymentStrategy = paymentStrategy;
    }
    
    public void checkout() {
        double total = calculateTotal();
        paymentStrategy.pay(total);
        items.clear();
    }
}
```
4. Classe auxiliar Item
```
// Item.java
public class Item {
    private String upcCode;
    private double price;
    
    public Item(String upcCode, double price) {
        this.upcCode = upcCode;
        this.price = price;
    }
    
    public String getUpcCode() {
        return upcCode;
    }
    
    public double getPrice() {
        return price;
    }
}
```
5. Classe Main para demonstrar o padrão
```
// Main.java
public class Main {
    public static void main(String[] args) {
        ShoppingCart cart = new ShoppingCart();
        
        Item item1 = new Item("1234", 100.50);
        Item item2 = new Item("5678", 50.25);
        
        cart.addItem(item1);
        cart.addItem(item2);
        
        // Pagamento com cartão de crédito
        cart.setPaymentStrategy(new CreditCardPayment("João Silva", "1234567890123456", "123", "12/25"));
        cart.checkout();
        
        // Adiciona itens novamente para demonstrar outra estratégia
        cart.addItem(new Item("9012", 75.99));
        
        // Pagamento com PayPal
        cart.setPaymentStrategy(new PayPalPayment("joao@example.com", "mypwd"));
        cart.checkout();
        
        // Adiciona itens novamente para demonstrar outra estratégia
        cart.addItem(new Item("3456", 120.00));
        
        // Pagamento com transferência bancária
        cart.setPaymentStrategy(new BankTransferPayment("987654321", "001"));
        cart.checkout();
    }
}
```
