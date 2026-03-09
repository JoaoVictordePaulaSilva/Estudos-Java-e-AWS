## 1. Abstração e Classes

A abstração consiste em isolar propriedades essenciais de um objeto, ignorando detalhes irrelevantes para o contexto.

- **Classe:** O molde/projeto (blueprint).
    
- **Objeto:** A instância real criada a partir do molde.
    
- **Atributos:** Características (variáveis).
    
- **Métodos:** Comportamentos (funções).
    


```java
public class ContaBancaria {
    // Atributos
    String titular;
    double saldo;

    // Método
    void depositar(double valor) {
        saldo += valor;
    }
}
```

_No IntelliJ: Digite `new ContaBancaria()` e use `Ctrl + Alt + V` para gerar a variável de referência automaticamente._

---

## 2. Encapsulamento e Modificadores de Acesso

Protege os dados internos de uma classe, controlando quem pode visualizá-los ou alterá-los.

### Tabela de Visibilidade

|**Modificador**|**Classe**|**Pacote**|**Subclasse**|**Global**|
|---|---|---|---|---|
|**private**|Sim|Não|Não|Não|
|**(default)**|Sim|Sim|Não|Não|
|**protected**|Sim|Sim|Sim|Não|
|**public**|Sim|Sim|Sim|Sim|

### Getters e Setters

Usados para ler e modificar atributos `private` de forma controlada.

Java

```java
public class Usuario {
    private String senha; // Ninguém acessa diretamente

    // Getter: Para ler
    public String getSenha() {
        return senha;
    }

    // Setter: Para alterar com validação
    public void setSenha(String novaSenha) {
        if (novaSenha.length() >= 8) {
            this.senha = novaSenha;
        }
    }
}
```

_Dica IntelliJ: Pressione `Alt + Insert` e selecione "Getter and Setter" para gerar tudo automaticamente._

---

## 3. Construtores e Palavra-chave `this`

O construtor define como o objeto deve "nascer". O `this` referencia o atributo da própria classe, evitando confusão com parâmetros.

Java

```java
public class Produto {
    private String nome;

    // Construtor
    public Produto(String nome) {
        this.nome = nome; 
    }
}
```

---

## 4. Java Records (Java 14+)

Ideal para classes que servem apenas como "transportadoras de dados" (DTOs). São imutáveis por padrão.

- Já cria automaticamente: Construtor, Getters, `equals`, `hashCode` e `toString`.
    
- Os campos são `final` (não podem ser alterados após a criação).
    

Java

```java
// Declaração em uma única linha
public record Cliente(String nome, String cpf) {}

// Uso:
Cliente c1 = new Cliente("Fulano", "123.456.789-00");
System.out.println(c1.nome()); // No record não usa "get", apenas o nome do campo
```

---

## 5. Boas Práticas

- **Tell, Don't Ask:** Em vez de pedir o saldo, validar e depois alterar, peça para a classe realizar a operação (ex: `conta.sacar(valor)`).
    
- **Atributos Privados:** Sempre inicie com atributos `private` e só dê acesso conforme a necessidade.
    
- **Nomenclatura:** Classes em `PascalCase`, métodos e variáveis em `camelCase`.