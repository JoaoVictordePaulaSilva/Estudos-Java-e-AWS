## 1. Herança (`extends`)

Permite que uma classe (filha/subclasse) herde atributos e métodos de outra classe (pai/superclasse), promovendo o reuso de código.

- **Regra:** Java não suporta herança múltipla de classes (uma classe filha tem apenas um pai).
    
- **Palavra-chave `super`:** Referencia membros da superclasse (construtores ou métodos).
    

Java

```java
public class Funcionario {
    protected String nome;
    protected double salario;

    public double getBonus() {
        return this.salario * 0.1;
    }
}

// Subclasse herda de Funcionario
public class Gerente extends Funcionario {
    @Override
    public double getBonus() {
        return super.getBonus() + 1000; // Usa o cálculo original + adicional
    }
}
```

---

## 2. Polimorfismo

A capacidade de um objeto ser referenciado de várias formas. Uma variável do tipo da superclasse pode apontar para um objeto de qualquer subclasse.

Java

```java
Funcionario f1 = new Gerente(); // Referência genérica, objeto específico
System.out.println(f1.getBonus()); // Executa a versão do Gerente (Sobrescrita)
```

### O Operador `instanceof`

Verifica se um objeto é de um determinado tipo antes de realizar um cast (conversão).

Java

```java
if (f1 instanceof Gerente) {
    Gerente g = (Gerente) f1; // Downcast seguro
    System.out.println("É um gerente");
}

// Versão moderna (Java 16+): Pattern Matching for instanceof
if (f1 instanceof Gerente g) {
    System.out.println(g.getBonus()); // Variável 'g' já está pronta para uso
}
```

---

## 3. Sobrecarga vs. Sobrescrita

Dois conceitos frequentemente confundidos, mas com propósitos distintos.

|**Característica**|**Sobrecarga (Overload)**|**Sobrescrita (Override)**|
|---|---|---|
|**Onde ocorre**|Na mesma classe.|Em classes diferentes (Herança).|
|**Nomes**|Devem ser iguais.|Devem ser iguais.|
|**Parâmetros**|**Devem ser diferentes.**|Devem ser idênticos.|
|**Anotação**|Nenhuma.|`@Override` (opcional, mas recomendada).|

### Exemplo de Sobrecarga (Mesma Classe)

Útil para criar diferentes formas de inicializar um objeto ou executar uma ação.

Java

```java
public class Calculadora {
    // Sobrecarga de método
    public int somar(int a, int b) { return a + b; }
    public int somar(int a, int b, int c) { return a + b + c; }
    
    // Sobrecarga de construtor
    public Calculadora() { }
    public Calculadora(int valorInicial) { /* ... */ }
}
```

---

## 4. Dicas de Produtividade no IntelliJ

- **Ver Hierarquia:** Pressione `Ctrl + H` sobre o nome de uma classe para ver toda a sua árvore de herança.
    
- **Sobrescrever Métodos:** Pressione `Ctrl + O` dentro da classe filha para listar métodos da superclasse que podem ser sobrescritos.
    
- **Implementar Métodos:** Pressione `Ctrl + I` se estiver lidando com métodos abstratos ou interfaces.
    
- **Casting Automático:** Ao usar `instanceof` (versão moderna), o IntelliJ sugere a refatoração automática para simplificar o código.