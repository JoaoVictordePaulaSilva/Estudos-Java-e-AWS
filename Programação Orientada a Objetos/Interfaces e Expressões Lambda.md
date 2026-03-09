## 1. Interfaces

Uma interface é um **contrato** que define quais métodos uma classe deve implementar, mas não necessariamente como. Ela permite que classes de diferentes hierarquias compartilhem comportamentos.

- **Contrato:** Todos os métodos abstratos são implicitamente `public` e `abstract`.
    
- **Múltipla Implementação:** Uma classe pode implementar várias interfaces.
    
- **Default Methods:** Permitem adicionar métodos com corpo nas interfaces sem quebrar as classes que já as implementam.
    


```java
public interface Autenticavel {
    // Método abstrato (sem corpo)
    boolean login(String senha);

    // Método Default (com implementação padrão)
    default void logAcesso() {
        System.out.println("Acesso solicitado.");
    }
}

public class Usuario implements Autenticavel {
    @Override
    public boolean login(String senha) {
        return "123".equals(senha);
    }
}
```

---

## 2. Interfaces Funcionais

Uma interface funcional é aquela que possui **exatamente um método abstrato**. Elas são a base para o uso de Lambdas no Java.

- **Anotação `@FunctionalInterface`:** Opcional, mas boa prática, pois força o compilador a garantir que haja apenas um método abstrato.
    
- **Principais Interfaces nativas (`java.util.function`):**
    
    - `Predicate<T>`: Recebe um valor e retorna um booleano (`test`).
        
    - `Consumer<T>`: Recebe um valor e não retorna nada (`accept`).
        
    - `Function<T, R>`: Recebe um valor e retorna outro (`apply`).
        
    - `Supplier<T>`: Não recebe nada e retorna um valor (`get`).
        

---

## 3. Expressões Lambda

As Lambdas fornecem uma maneira clara e concisa de representar uma instância de uma interface funcional. Elas eliminam a necessidade de criar classes anônimas verbosas.

### Sintaxe

`(parâmetros) -> { corpo_do_codigo }`

### Comparativo: Antes vs Depois


```java
List<String> nomes = Arrays.asList("Java", "Python", "C#");

// Forma antiga: Classe Anônima
nomes.forEach(new Consumer<String>() {
    @Override
    public void accept(String s) {
        System.out.println(s);
    }
});

// Forma nova: Lambda
nomes.forEach(n -> System.out.println(n));

// Evolução: Method Reference (mais conciso ainda)
nomes.forEach(System.out::println);
```

---

## 4. Exemplos Práticos Rápidos

|**Contexto**|**Exemplo com Lambda**|
|---|---|
|**Ordenação**|`lista.sort((a, b) -> a.compareTo(b));`|
|**Filtro**|`lista.removeIf(n -> n.length() < 3);`|
|**Thread**|`new Thread(() -> System.out.println("Rodando...")).start();`|

---

## 5. Dicas de Produtividade no IntelliJ

- **Substituir por Lambda:** Quando você escreve uma classe anônima para uma interface funcional, o IntelliJ sublinha em cinza. Pressione `Alt + Enter` e escolha **"Replace with lambda"**.
    
- **Inspecionar tipo:** Se a Lambda for complexa, coloque o cursor sobre a seta `->` e o IntelliJ mostrará a qual interface funcional ela pertence.
    
- **Method Reference:** Se sua Lambda apenas repassa um parâmetro para outro método (ex: `n -> System.out.println(n)`), use `Alt + Enter` para converter em **Method Reference** (`System.out::println`).



