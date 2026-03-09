## 1. Tipos de Data e Hora

A API separa as preocupações: data pura, hora pura, ou ambos, com ou sem fuso horário.

|**Classe**|**O que representa?**|**Exemplo de Saída**|
|---|---|---|
|**`LocalDate`**|Apenas data (ano, mês, dia).|`2026-03-09`|
|**`LocalTime`**|Apenas hora (hora, min, seg, nano).|`14:30:15`|
|**`LocalDateTime`**|Data e hora sem fuso horário.|`2026-03-09T14:30:15`|
|**`OffsetTime`**|Hora com deslocamento UTC (fuso).|`14:30:15-03:00`|
|**`OffsetDateTime`**|Data e hora com deslocamento UTC.|`2026-03-09T14:30:15-03:00`|

---

## 2. Exemplos de Uso Prático

### Criando Instâncias

Diferente do `Calendar`, aqui os meses são ENUMS ou números de **1 a 12**.


```java
// Data e Hora atual
LocalDate hoje = LocalDate.now();
LocalTime agora = LocalTime.now();
LocalDateTime dataHoraAgora = LocalDateTime.now();

// Datas específicas
LocalDate natal = LocalDate.of(2026, 12, 25);
LocalTime almoco = LocalTime.of(12, 30, 0);

// Offset (Fuso Horário)
OffsetDateTime dataComFuso = OffsetDateTime.now(); // Pega o fuso do sistema
```

### Manipulação (Imutabilidade)

Lembre-se: como são imutáveis, você deve **atribuir o resultado** a uma variável.


```java
LocalDate amanha = hoje.plusDays(1);
LocalDate mesPassado = hoje.minusMonths(1);
LocalDateTime daquiDuasHoras = dataHoraAgora.plusHours(2);
```

---

## 3. Formatação Moderna: `DateTimeFormatter`

Esqueça o `SimpleDateFormat`. O novo formatador é mais rápido e seguro.


```java
import java.time.format.DateTimeFormatter;

LocalDateTime agora = LocalDateTime.now();

// Formatação para String
DateTimeFormatter fmt = DateTimeFormatter.ofPattern("dd/MM/yyyy HH:mm");
System.out.println(agora.format(fmt));

// Parse de String para Objeto
LocalDate dataParse = LocalDate.parse("09/03/2026", DateTimeFormatter.ofPattern("dd/MM/yyyy"));
```

---

## 4. Comparação entre Datas

Para saber se uma data é antes ou depois de outra, usamos métodos semânticos.


```java
if (hoje.isBefore(natal)) {
    System.out.println("Ainda não é natal!");
}

if (hoje.isAfter(natal)) {
    System.out.println("O natal já passou.");
}
```

---

## 5. Resumo de Diferenças (Dica para Provas/Entrevistas)

|**Característica**|**Local (Date/Time)**|**Offset (Date/Time)**|
|---|---|---|
|**Fuso Horário**|Não possui.|Possui (ex: -03:00).|
|**Uso**|Contexto local (ex: validade de produto).|Sistemas distribuídos, Logs, transações bancárias.|
|**Referência**|Onde o usuário está.|Referência absoluta em relação ao UTC.|

---

## 6. Dicas de Produtividade no IntelliJ

- **Atalhos de Criação:** Digite `.now` após o nome da classe (ex: `LocalDate.now`) e use `Ctrl + Alt + V` para gerar a variável.
    
- **Inspeção de Formato:** Ao criar um `DateTimeFormatter.ofPattern("")`, o IntelliJ ajuda a validar se os símbolos (y, M, d, H) são válidos.
    
- **Migração:** Se você colar um código antigo com `java.util.Date`, o IntelliJ frequentemente oferece uma "Light Bulb" (lâmpada) sugerindo converter para `java.time`.