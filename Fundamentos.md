## 1. Padrões de Desenvolvimento e Estrutura

O Java organiza o código de forma hierárquica para facilitar a manutenção e evitar conflitos de nomenclatura.

### Packages e Imports

- **Package:** Define o "endereço" da classe. Deve ser a primeira linha do arquivo.
    
- **Import:** Traz classes de outros pacotes para o seu arquivo.
    
- **Documentação (IntelliJ):** Posicione o cursor sobre uma classe/método e pressione `Ctrl + Q` para ver a documentação oficial (Javadoc).
    

### Classe Main e Entrada de Dados

A porta de entrada de qualquer aplicação Java.

Java

```java
package com.projeto.aula; // Definição do pacote

import java.util.Scanner; // Import da classe Scanner

public class Main {
    public static void main(String[] args) {
        // Instanciação do Scanner para leitura do teclado
        Scanner leitor = new Scanner(System.in);

        System.out.print("Digite um valor: ");
        int valor = leitor.nextInt(); 

        System.out.println("O valor digitado foi: " + valor);

        leitor.close(); // Boa prática: fechar o recurso
    }
}
```

---

## 2. Keywords e Tipos Primitivos

Java possui 8 tipos primitivos. É fundamental usar os sufixos corretos para evitar erros de compilação ou perda de precisão.

### Tabela de Tipos Primitivos

|**Tipo**|**Tamanho**|**Descrição**|**Exemplo / Sufixo**|
|---|---|---|---|
|**boolean**|1 bit|true ou false|`boolean ativo = true;`|
|**char**|16 bits|Um caractere Unicode|`char letra = 'A';`|
|**byte**|8 bits|-128 a 127|`byte n = 10;`|
|**short**|16 bits|-32.768 a 32.767|`short n = 1000;`|
|**int**|32 bits|Padrão para inteiros|`int n = 50000;`|
|**long**|64 bits|Inteiros grandes|`long n = 900L;` (Obrigatório **L**)|
|**float**|32 bits|Precisão simples|`float n = 10.5f;` (Obrigatório **f**)|
|**double**|64 bits|Precisão dupla (padrão)|`double n = 10.5d;` (Opcional **d**)|

### Métodos de Saída (Print)

- `System.out.print()`: Imprime e mantém o cursor na mesma linha.
    
- `System.out.println()`: Imprime e pula para a próxima linha.
    
- `System.out.printf()`: Saída formatada.
    
    - `%s` -> String
        
    - `%d` -> Inteiro
        
    - `%.2f` -> Decimal com 2 casas
        

---

## 3. Operadores

### Aritméticos

Usados para cálculos matemáticos básicos.

- `+` : Soma
    
- `-` : Subtração
    
- `*` : Multiplicação
    
- `/` : Divisão
    
- `%` : Resto da divisão (Módulo)
    

### Lógicos

Retornam valores booleanos baseados em proposições.

- `&&` : **AND** (E) - Verdadeiro se ambos forem true.
    
- `||` : **OR** (OU) - Verdadeiro se ao menos um for true.
    
- `!` : **NOT** (NÃO) - Inverte o estado booleano.
    

### Bitwise (Bit a Bit)

Operam diretamente nos bits individuais dos números.

|**Operador**|**Nome**|**Descrição**|
|---|---|---|
|`&`|AND|Compara cada bit; resulta 1 se ambos forem 1.|
|`\|`|OR|Resulta 1 se ao menos um bit for 1.|
|`^`|XOR|Resulta 1 se os bits forem diferentes.|
|`~`|NOT|Inverte todos os bits (complemento).|
|`<<`|Left Shift|Desloca bits para a esquerda (multiplica por 2).|
|`>>`|Right Shift|Desloca bits para a direita (divide por 2).|

**Exemplo Rápido:**

Java

```java
int a = 5;  // 0101 em binário
int b = 3;  // 0011 em binário

int and = a & b; // Resulta 1 (0001)
int or  = a | b; // Resulta 7 (0111)
```