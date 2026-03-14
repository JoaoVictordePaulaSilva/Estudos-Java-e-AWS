
## 1. Estruturas Condicionais

Decidem qual bloco de código será executado com base em uma condição booleana.

### If / Else If / Else

Utilizado para desvios lógicos baseados em condições verdadeiras ou falsas.

Java

```java
int idade = 18;

if (idade < 16) {
    System.out.println("Não vota");
} else if (idade >= 18) {
    System.out.println("Voto obrigatório");
} else {
    System.out.println("Voto facultativo");
}
```

### Switch Case

Ideal para múltiplas escolhas baseadas em uma única variável (Inteiros, Strings ou Enums).

|**Componente**|**Função**|
|---|---|
|**switch(var)**|Variável a ser testada.|
|**case valor:**|Executa se a variável for igual ao valor.|
|**break;**|Interrompe a execução (evita o "fall-through").|
|**default:**|Executa se nenhum caso for atendido.|

Java

```java
int dia = 2;
switch (dia) {
    case 1 -> System.out.println("Segunda"); // Sintaxe moderna (Java 14+)
    case 2 -> System.out.println("Terça");
    default -> System.out.println("Dia inválido");
}
```

---

## 2. Estruturas de Repetição (Loops)

Repetem um bloco de código enquanto uma condição for atendida.

### While

Verifica a condição **antes** de executar o bloco. Se for falsa de início, nunca executa.

Java

```java
int contador = 0;
while (contador < 5) {
    System.out.println("Valor: " + contador);
    contador++; // Crucial para evitar loop infinito
}
```

### Do While

Executa o bloco **ao menos uma vez**, pois a verificação ocorre no final.

Java

```java
int opcao;
do {
    System.out.println("Executando menu...");
    opcao = 0; 
} while (opcao != 0);
```

---

## 3. Estrutura For

Ideal quando você sabe exatamente quantas vezes o código deve ser repetido.

### For Tradicional

Dividido em: **Inicialização**; **Condição**; **Incremento**.

Java

```java
// (inicio; condição; passo)
for (int i = 0; i < 10; i++) {
    System.out.println("Índice: " + i);
}
```

### Enhanced For (For-Each)

Utilizado para percorrer arrays ou coleções de forma simplificada.

Java

```java
String[] nomes = {"Java", "Python", "C#"};

for (String nome : nomes) {
    System.out.println(nome);
}
```

---

## 4. Comandos de Interrupção

|**Comando**|**Efeito**|
|---|---|
|**break**|Sai imediatamente do loop ou switch atual.|
|**continue**|Pula a iteração atual e vai para a próxima validação do loop.|

### Dica de IntelliJ

No IntelliJ, você pode digitar `fori` e apertar `Tab` para gerar automaticamente a estrutura de um loop `for` indexado. Para o `System.out.println()`, use o atalho `sout` + `Tab`.