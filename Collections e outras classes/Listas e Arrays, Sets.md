## 1. Arrays (Vetores)

Estrutura básica, estática e de tamanho fixo. Armazena elementos do mesmo tipo (primitivos ou objetos).

- **Tamanho:** Imutável após a criação.
    
- **Acesso:** Direto via índice (começa em 0).
    
- **Propriedade:** `.length` (não é um método).
    


```java
// Declaração e inicialização
int[] numeros = new int[5];
String[] nomes = {"Java", "Kotlin", "Scala"};

// Acesso e modificação
nomes[0] = "Java 21";
int tamanho = nomes.length; 

// Percorrendo (For clássico)
for (int i = 0; i < nomes.length; i++) {
    System.out.println(nomes[i]);
}
```

---

## 2. List (Interface)

Parte do _Collections Framework_. Representa uma sequência ordenada de elementos que permite duplicatas.

- **Implementação comum:** `ArrayList` (baseada em array dinâmico).
    
- **Vantagem:** Cresce automaticamente conforme a necessidade.
    
- **Métodos chave:** `add()`, `get(index)`, `remove(index)`, `size()`.
    

```java
import java.util.ArrayList;
import java.util.List;

List<String> lista = new ArrayList<>();

lista.add("Elemento A");
lista.add("Elemento B");
lista.add("Elemento A"); // Permite duplicados

String primeiro = lista.get(0); // Acesso por índice
lista.remove(1); // Remove por índice ou objeto

// Iteração Moderna (Lambda)
lista.forEach(System.out::println);
```

---

## 3. Set (Interface)

Uma coleção que **não permite elementos duplicados**. Ideal para garantir unicidade.

- **Implementação comum:** `HashSet` (rápida, mas não garante ordem).
    
- **Implementação ordenada:** `TreeSet` (mantém ordem natural ou definida).
    
- **Método chave:** `add()` (retorna `false` se o elemento já existir).
    


```java
import java.util.HashSet;
import java.util.Set;

Set<Integer> numerosUnicos = new HashSet<>();

numerosUnicos.add(10);
numerosUnicos.add(20);
numerosUnicos.add(10); // Será ignorado, pois já existe

if (numerosUnicos.contains(10)) {
    System.out.println("O número 10 está no conjunto.");
}
```

---

## 4. Comparativo Rápido

|**Característica**|**Array**|**List (ArrayList)**|**Set (HashSet)**|
|---|---|---|---|
|**Tamanho**|Fixo|Dinâmico|Dinâmico|
|**Permite Duplicados**|Sim|Sim|**Não**|
|**Ordenado**|Sim (por índice)|Sim (ordem de inserção)|Não (em geral)|
|**Acesso por Índice**|`array[i]`|`lista.get(i)`|Não possui|
|**Performance**|Alta (memória contígua)|Média/Alta|Alta (para buscas)|

---

## 5. Operações Úteis (Classe Collections)

A classe `java.util.Collections` fornece métodos estáticos para manipular coleções.


```java
import java.util.Collections;

Collections.sort(lista);          // Ordena a lista
Collections.reverse(lista);       // Inverte a ordem
Collections.shuffle(lista);       // Embaralha os elementos
int min = Collections.min(lista); // Encontra o menor valor
```

---

## 6. Dicas de Produtividade no IntelliJ

- **Gerar declaração:** Digite `new ArrayList<String>()` e use `Ctrl + Alt + V` para criar a variável `List<String> list = ...`.
    
- **Iterar rapidamente:** Digite `lista.for` e aperte `Tab` para gerar um loop for-each automaticamente.
    
- **Converter Array para Lista:** Use `Arrays.asList(meuArray)` ou o moderno `List.of(1, 2, 3)` (para listas imutáveis).