## 1. Generics

Permitem que classes, interfaces e métodos operem sobre tipos especificados pelo usuário, garantindo que o compilador verifique se você está usando o tipo correto.

- **Vantagem:** Elimina a necessidade de _casting_ manual e evita o `ClassCastException`.
    
- **Convenção de Letras:** * `<T>`: Type (Tipo geral)
    
    - `<E>`: Element (Usado em coleções)
        
    - `<K, V>`: Key e Value (Usado em Maps)
        



```java
// Classe Genérica
public class Caixa<T> {
    private T conteudo;

    public void guardar(T objeto) { this.conteudo = objeto; }
    public T pegar() { return conteudo; }
}

// Uso
Caixa<String> caixaDeTexto = new Caixa<>();
caixaDeTexto.guardar("Java 21");
String texto = caixaDeTexto.pegar(); // Não precisa de cast
```

---

## 2. Stream API (Java 8+)

Uma Stream é uma sequência de elementos que suporta diferentes tipos de operações para processar coleções de forma **declarativa** (você diz _o que_ quer, não _como_ fazer).

### Estrutura de uma Stream

1. **Fonte:** `lista.stream()`
    
2. **Operações Intermediárias:** Retornam uma nova Stream (são "preguiçosas", só executam no final).
    
3. **Operação Terminal:** Fecha a Stream e produz um resultado ou efeito colateral.
    

### Principais Operações

|**Tipo**|**Método**|**Descrição**|
|---|---|---|
|**Intermediária**|`filter(predicate)`|Filtra elementos com base em uma condição.|
|**Intermediária**|`map(function)`|Transforma cada elemento em outra coisa.|
|**Intermediária**|`sorted()`|Ordena os elementos.|
|**Intermediária**|`distinct()`|Remove duplicatas (usa o `.equals()`).|
|**Terminal**|`forEach(consumer)`|Executa uma ação para cada elemento.|
|**Terminal**|`collect(Collectors.toList())`|Converte a Stream de volta para uma Lista.|
|**Terminal**|`count()`|Retorna a quantidade de elementos.|

---

## 3. Exemplo Prático: O "Poder" das Streams

Imagine filtrar uma lista de nomes, transformar para maiúsculo e ordenar:

Java

```java
List<String> nomes = Arrays.asList("Felipe", "Ana", "Beto", "Amélia");

List<String> resultado = nomes.stream()
    .filter(n -> n.startsWith("A"))    // Filtra quem começa com 'A'
    .map(String::toUpperCase)          // Transforma em MAIÚSCULO
    .sorted()                          // Ordena (Amélia, Ana)
    .collect(Collectors.toList());     // Agrupa em uma nova lista

System.out.println(resultado); // [AMÉLIA, ANA]
```

---

## 4. Diferença Crucial: Stream vs Collection

- **Collection:** É sobre o armazenamento de dados (foco na estrutura).
    
- **Stream:** É sobre o processamento de dados (foco na computação). Uma Stream não altera a coleção original.
    

---

## 5. Dicas de Produtividade no IntelliJ

- **Debugger de Stream:** Durante o debug, o IntelliJ tem um botão chamado **"Trace Current Stream Chain"**. Ele abre uma janela visual que mostra exatamente o que aconteceu com cada elemento em cada etapa da Stream (`filter`, `map`, etc). É a melhor ferramenta para aprender Streams.
    
- **Refatoração para Stream:** Se você escrever um loop `for` com um `if` dentro, o IntelliJ sugerirá converter para Stream automaticamente. Use `Alt + Enter` sobre o `for`.
    
- **Wildcards em Generics:** Se encontrar `<? extends T>` ou `<? super T>`, lembre-se do princípio **PECS** (Producer Extends, Consumer Super). O IntelliJ ajuda a corrigir erros de tipo nesses casos complexos.