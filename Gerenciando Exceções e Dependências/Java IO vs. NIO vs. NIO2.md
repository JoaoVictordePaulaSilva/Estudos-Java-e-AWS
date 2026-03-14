## 1. Java IO (`java.io`)

Baseado no conceito de **Streams** (fluxos de dados). É unidirecional e bloqueante (o programa para e espera a leitura terminar).

- **InputStream / OutputStream:** Para dados binários (imagens, vídeos).
    
- **Reader / Writer:** Para dados de texto (caracteres).
    
- **File:** Representa o caminho do arquivo (mas tem limitações, como não lançar exceções claras).
    



```java
// Exemplo clássico com BufferedReader (mais rápido que ler caractere por caractere)
try (BufferedReader br = new BufferedReader(new FileReader("arquivo.txt"))) {
    String linha;
    while ((linha = br.readLine()) != null) {
        System.out.println(linha);
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

---

## 2. Java NIO (`java.nio`)

Introduzido para melhorar a performance. Baseado em **Buffers** e **Channels**.

- **Canais (Channels):** Diferente das Streams, são bidirecionais (pode ler e escrever no mesmo canal).
    
- **Seletores (Selectors):** Permitem que uma única Thread gerencie múltiplos canais (essencial para servidores de alta performance).
    

---

## 3. Java NIO2 (`java.nio.file`)

Uma evolução completa que facilitou absurdamente a manipulação de arquivos no Java 7+. É a recomendação atual para quase tudo.

### Classes Principais:

- **Path:** Interface que substitui a classe `File`. Representa o caminho no sistema.
    
- **Paths:** Classe utilitária para criar instâncias de `Path`.
    
- **Files:** Classe utilitária com métodos estáticos poderosos para mover, copiar, ler e deletar.
    


```java
import java.nio.file.*;
import java.util.List;

// Criando um Path
Path path = Paths.get("documentos/notas.txt");

// Lendo todas as linhas de forma simples
try {
    List<String> linhas = Files.readAllLines(path);
    
    // Escrevendo em um arquivo (Cria se não existir, sobrescreve se existir)
    Files.write(Paths.get("copia.txt"), linhas);
    
    // Verificando existência
    if (Files.exists(path)) {
        System.out.println("Arquivo encontrado!");
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

---

## 4. Comparativo Rápido

|**Característica**|**Java IO**|**Java NIO / NIO2**|
|---|---|---|
|**Abordagem**|Orientada a Fluxo (Stream)|Orientada a Buffer|
|**Bloqueante**|Sim|Não (Configurável)|
|**Performance**|Menor para grandes volumes|Alta performance|
|**Manipulação**|Limitada (Classe `File`)|Completa (`Path` e `Files`)|
|**Facilidade**|Simples para textos pequenos|Muito intuitiva no NIO2|

---

## 5. Dicas de Produtividade no IntelliJ

- **Importação:** Ao digitar `Files.`, certifique-se de importar o `java.nio.file.Files` e não o do Google ou outras bibliotecas.
    
- **Caminhos Relativos:** No IntelliJ, o caminho relativo (ex: `"arquivo.txt"`) começa na **raiz do seu projeto**. Se o arquivo estiver dentro de `src`, o caminho deve ser `"src/arquivo.txt"`.
    
- **Try-with-resources:** Sempre use o `try(...)` para abrir Streams ou Readers. O IntelliJ avisará se você esquecer de fechar um recurso que pode causar vazamento de memória.
    
- **Novidades (Java 11+):** Você pode ler uma String inteira de um arquivo com um único comando: `Files.readString(path)`.