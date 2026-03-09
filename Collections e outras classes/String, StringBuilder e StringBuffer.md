## 1. Classe String

A `String` no Java é **imutável**. Isso significa que, toda vez que você "altera" uma String, o Java não modifica a original; ele cria uma **nova** String na memória (no String Pool).

- **Uso:** Ideal para textos que não mudam frequentemente.
    
- **Segurança:** Segura para multi-threads (por ser imutável).
    
- **Performance:** Ruim para concatenações em loops (gera muito lixo na memória).
    

```java
String nome = "Java";
nome = nome + " 21"; // Criou uma nova String na memória, a antiga "Java" será descartada.
```

---

## 2. StringBuilder e StringBuffer

Ambas são classes **mutáveis**, ou seja, você pode modificar o conteúdo do mesmo objeto sem criar novos objetos na memória.

- **StringBuilder:** * Mais rápida.
    
    - **Não é Thread-Safe** (não deve ser usada se várias threads acessarem o mesmo objeto simultaneamente).
        
    - Recomendada para a maioria dos casos (uso geral).
        
- **StringBuffer:** * Um pouco mais lenta que o StringBuilder.
    
    - **Thread-Safe** (métodos sincronizados).
        
    - Recomendada apenas em ambientes concorrentes (multi-thread).
        

### Exemplo de Uso (StringBuilder)


```java
StringBuilder sb = new StringBuilder("Curso");

sb.append(" de");    // Adiciona ao final
sb.append(" Java");  // Adiciona ao final
sb.insert(0, "> "); // Insere no início ou posição específica
sb.reverse();        // Inverte o texto
sb.delete(0, 2);     // Remove caracteres por índice

String resultado = sb.toString(); // Converte de volta para String
```

---

## 3. Comparativo Rápido

|**Característica**|**String**|**StringBuilder**|**StringBuffer**|
|---|---|---|---|
|**Mutável**|Não|Sim|Sim|
|**Thread-Safe**|Sim (por ser imutável)|Não|Sim|
|**Performance**|Lenta (se houver muitas mudanças)|Muito Rápida|Rápida|
|**Uso Principal**|Literais, chaves de Map, nomes|Construção de strings pesada|Multi-threading|

---

## 4. Métodos Úteis de String (Pesquisa Rápida)

|**Método**|**Descrição**|
|---|---|
|`length()`|Retorna o tamanho da string.|
|`contains("xyz")`|Verifica se contém a sequência.|
|`toUpperCase()` / `toLowerCase()`|Altera a caixa das letras.|
|`trim()`|Remove espaços em branco nas extremidades.|
|`replace("a", "b")`|Substitui caracteres ou sequências.|
|`substring(inicio, fim)`|Corta a string entre dois índices.|
|`equals()` / `equalsIgnoreCase()`|Compara conteúdo (NUNCA use `==` para Strings).|

---

## 5. Dicas de Produtividade no IntelliJ

- **Concatenação em Loops:** Se você escrever um loop que faz `string += "texto"`, o IntelliJ mostrará um aviso amarelo sugerindo trocar para `StringBuilder.append()`. Pressione `Alt + Enter` para ele refatorar sozinho.
    
- **Visualização de Memória:** Strings muito grandes podem ser visualizadas por completo no debugger do IntelliJ clicando em "View" ao lado do valor da variável.
    
- **Sintaxe Multilinha (Text Blocks):** No Java 15+, para strings grandes (como HTML ou SQL), use três aspas:
    
    Java
    
    ```java
    String sql = """
                 SELECT * FROM usuarios
                 WHERE ativo = true
                 """;
    ```