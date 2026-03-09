## 1. BigDecimal

Diferente de `double` ou `float`, o `BigDecimal` é usado para cálculos que exigem precisão absoluta (como valores monetários), pois não sofre com arredondamentos binários.

- **Imutabilidade:** Operações não alteram o valor original, retornam um novo objeto.
    
- **Comparação:** **Nunca** use `==` ou `.equals()`, use `compareTo()`.
    


```java
import java.math.BigDecimal;
import java.math.RoundingMode;

BigDecimal valor = new BigDecimal("100.50"); // Use String no construtor para evitar imprecisão
BigDecimal taxa = new BigDecimal("0.10");

// Operações
BigDecimal soma = valor.add(taxa);
BigDecimal sub  = valor.subtract(taxa);
BigDecimal mult = valor.multiply(taxa);
BigDecimal div  = valor.divide(taxa, 2, RoundingMode.HALF_UP); // Sempre defina escala e arredondamento

// Comparação
if (valor.compareTo(BigDecimal.ZERO) > 0) {
    System.out.println("Valor é maior que zero");
}
```

---

## 2. Enums (Enumerações)

Tipo especial que define um conjunto de constantes fixas. É muito mais poderoso que simples `Strings` ou `Integers` porque permite adicionar métodos e atributos.


```java
public enum StatusPedido {
    AGUARDANDO_PAGAMENTO(1),
    PROCESSANDO(2),
    ENVIADO(3),
    ENTREGUE(4);

    private final int codigo;

    // Construtor de Enum é sempre privado
    StatusPedido(int codigo) {
        this.codigo = codigo;
    }

    public int getCodigo() {
        return codigo;
    }
}
```

_Uso no Switch:_


```java
StatusPedido status = StatusPedido.ENVIADO;
switch (status) {
    case ENVIADO -> System.out.println("O produto saiu!");
    case ENTREGUE -> System.out.println("Chegou!");
}
```

---

## 3. Classe Optional (Java 8+)

Um container que pode ou não conter um valor não nulo. Serve para indicar explicitamente que um método pode retornar "nada", evitando o erro de `null`.

|**Método**|**Descrição**|
|---|---|
|`Optional.of(obj)`|Cria com valor (lança erro se o obj for null).|
|`Optional.ofNullable(obj)`|Cria com valor ou vazio (aceita null).|
|`isPresent()`|Retorna true se houver valor.|
|`ifPresent(lambda)`|Executa a lambda se houver valor.|
|`orElse(padrão)`|Retorna o valor ou um padrão se estiver vazio.|
|`orElseThrow()`|Retorna o valor ou lança uma exceção.|


```java
public Optional<String> buscarNome(int id) {
    // Lógica que pode retornar nulo
    return Optional.ofNullable(nomeDoBanco);
}

// Uso seguro
buscarNome(10)
    .map(String::toUpperCase)
    .ifPresent(n -> System.out.println("Nome: " + n));

String resultado = buscarNome(5).orElse("Desconhecido");
```

---

## 4. Resumo Comparativo Rápido

|**Recurso**|**Quando usar?**|**Principal benefício**|
|---|---|---|
|**BigDecimal**|Dinheiro, taxas, medidas exatas.|Precisão decimal sem erros de bit.|
|**Enum**|Categorias, dias da semana, status.|Segurança de tipos (Type Safety).|
|**Optional**|Retornos de métodos que podem ser nulos.|Código limpo sem `if (x != null)`.|

---

## 5. Dicas de Produtividade no IntelliJ

- **BigDecimal:** Ao digitar `valor.add(taxa)`, se você não atribuir a uma variável, o IntelliJ avisará que o resultado está sendo ignorado (lembre-se: ele é imutável).
    
- **Extract Enum:** Se você tem muitas constantes `String` ou `int` em uma classe, use `Refactor > Extract > Delegate to Enum`.
    
- **Optional Chain:** O IntelliJ ajuda a converter blocos de `if (obj != null)` para encadeamentos de `.map()` e `.filter()` do Optional com `Alt + Enter`.