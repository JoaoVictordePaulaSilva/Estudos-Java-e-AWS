## 1. O que é uma Thread?

Uma Thread é um "fio" de execução independente dentro de um processo. Por padrão, todo programa Java tem pelo menos uma: a **Main Thread**.

### Estados de uma Thread

|**Estado**|**Descrição**|
|---|---|
|**New**|A thread foi criada, mas ainda não iniciada.|
|**Runnable**|A thread está pronta para rodar (aguardando o processador).|
|**Running**|O processador está executando o código da thread.|
|**Blocked/Waiting**|A thread está esperando por um recurso ou outra thread.|
|**Terminated**|A execução do método `run()` foi finalizada.|

---

## 2. Criando Threads: Duas Formas

### Opção A: Herdando de `Thread`

Você cria uma nova classe que estende `Thread` e sobrescreve o método `run()`.


```java
class MeuProcesso extends Thread {
    @Override
    public void run() {
        System.out.println("Rodando em uma thread separada: " + getName());
    }
}

// Uso:
MeuProcesso t1 = new MeuProcesso();
t1.start(); // IMPORTANTE: Use start(), não run(), para criar a nova thread.
```

### Opção B: Implementando `Runnable` (Recomendado)

Como Java não permite herança múltipla, implementar a interface `Runnable` é a melhor prática, pois sua classe ainda pode herdar de outra.


``` java
class MinhaTarefa implements Runnable {
    @Override
    public void run() {
        System.out.println("Executando tarefa via Runnable.");
    }
}

// Uso:
Thread t2 = new Thread(new MinhaTarefa());
t2.start();
```

---

## 3. Uso com Expressões Lambda (Java 8+)

Como `Runnable` é uma **Interface Funcional**, podemos criar threads de forma muito mais rápida:


```java
new Thread(() -> {
    System.out.println("Thread rodando com Lambda!");
}).start();
```

---

## 4. Métodos Essenciais de Controle

|**Método**|**Descrição**|
|---|---|
|**`start()`**|Inicia a thread e chama o método `run()`.|
|**`sleep(ms)`**|Pausa a thread atual por um tempo determinado (estático).|
|**`join()`**|Faz a thread atual esperar até que a thread alvo termine.|
|**`yield()`**|Sugere ao processador dar prioridade a outras threads.|
|**`isAlive()`**|Verifica se a thread ainda está em execução.|

---

## 5. Cuidados Importantes

- **`start()` vs `run()`:** Chamar `.run()` diretamente executa o código na mesma thread (como um método comum). Apenas `.start()` cria uma nova trilha de execução.
    
- **Race Condition:** Quando duas threads tentam alterar a mesma variável ao mesmo tempo. Para evitar isso, usa-se a palavra-chave `synchronized`.
    

---

## 6. Dicas de Produtividade no IntelliJ

- **Nomear Threads:** Sempre que criar uma thread, use `t.setName("ProcessoX")`. No **Debugger** do IntelliJ, na aba "Threads", você verá os nomes que definiu, facilitando muito encontrar onde está o erro.
    
- **Monitor de Threads:** Durante o debug, use a aba **"Threads & Variables"** para pausar ou inspecionar threads individuais.
    
- **Thread.sleep:** O IntelliJ vai te avisar que o `sleep()` lança uma `InterruptedException`. Use `Alt + Enter` para envolver rapidamente em um `try-catch`.