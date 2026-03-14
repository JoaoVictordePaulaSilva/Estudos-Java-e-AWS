## 1. O que são Exceções?

Exceções são eventos que interrompem o fluxo normal do programa. No Java, elas são objetos que herdam da classe `Throwable`.

### Hierarquia das Exceções

- **Error:** Problemas graves que o programa não consegue recuperar (ex: `OutOfMemoryError`).
    
- **Checked Exception (Verificada):** O compilador obriga você a tratar (ex: `IOException`, `SQLException`).
    
- **Unchecked Exception (Não verificada):** Erros de lógica que ocorrem em tempo de execução (ex: `NullPointerException`, `ArrayIndexOutOfBoundsException`). Herdam de `RuntimeException`.
    

---

## 2. Tratamento de Exceções (`try-catch-finally`)

|**Bloco**|**Função**|
|---|---|
|**`try`**|Contém o código que "pode" lançar um erro.|
|**`catch`**|Captura a exceção e executa o tratamento (erro).|
|**`finally`**|Bloco opcional que **sempre** executa (útil para fechar arquivos ou conexões).|


```java
try {
    int resultado = 10 / 0;
} catch (ArithmeticException e) {
    System.err.println("Erro: Não é possível dividir por zero!");
} finally {
    System.out.println("Fim da operação (sempre executa).");
}
```

### Try-with-resources (Java 7+)

Forma moderna de fechar recursos automaticamente (como o `Scanner` ou arquivos) sem precisar do `finally`. O recurso deve implementar `AutoCloseable`.


```java
try (Scanner leitor = new Scanner(System.in)) {
    int n = leitor.nextInt();
} catch (Exception e) {
    System.out.println("Erro na leitura.");
} // O leitor será fechado automaticamente aqui
```

---

## 3. Lançando Exceções (`throw` e `throws`)

- **`throw`:** Lança uma exceção manualmente.
    
- **`throws`:** Avisa na assinatura do método que ele pode lançar aquela exceção (obriga quem chama a tratar).
    


```java
public void validarIdade(int idade) throws Exception {
    if (idade < 18) {
        throw new Exception("Menor de idade não permitido.");
    }
}
```

---

## 4. Debugging no IntelliJ IDEA

O Debugger é sua ferramenta de "raio-x" para ver o que acontece linha por linha.

### Atalhos e Funções de Debug

- **Breakpoint:** Clique na lateral da linha (bolinha vermelha) para o código parar ali.
    
- **F8 (Step Over):** Vai para a próxima linha sem entrar em métodos.
    
- **F7 (Step Into):** Entra dentro do método da linha atual para ver o que ocorre lá.
    
- **Shift + F8 (Step Out):** Sai do método atual e volta para quem o chamou.
    
- **Evaluate Expression (`Alt + F8`):** Permite testar códigos e ver valores de variáveis em tempo real enquanto o programa está pausado.
    

---

## 5. Boas Práticas

- **Não use Exception genérica:** Evite `catch (Exception e)`. Capture a exceção específica para saber exatamente o que falhou.
    
- **Fail Fast:** Valide as condições no início do método e lance a exceção o quanto antes.
    
- **Mensagens Claras:** Ao lançar exceções, forneça mensagens que ajudem a identificar o erro.