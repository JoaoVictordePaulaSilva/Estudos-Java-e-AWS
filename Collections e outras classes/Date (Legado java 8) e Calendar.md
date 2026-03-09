## 1. Classe Date

Foi a primeira tentativa do Java de lidar com tempo. Representa um ponto específico no tempo com precisão de milissegundos.

- **Problema:** A maioria dos seus métodos está **depreciada** (obsoleta).
    
- **Armazenamento:** Guarda o número de milissegundos desde "A Época" (1º de janeiro de 1970).
    


```java
import java.util.Date;

Date agora = new Date(); 
System.out.println(agora); // Exibe: Mon Mar 09 11:38:16 BRT 2026

long milissegundos = agora.getTime(); // Retorna o tempo em ms desde 1970
```

---

## 2. Classe Calendar

Surgiu para resolver os problemas da `Date`, permitindo manipulação de campos específicos (dia, mês, ano). É uma classe **abstrata**, então usamos `getInstance()`.

- **Atenção:** No `Calendar`, os meses são indexados em **0** (Janeiro = 0, Dezembro = 11).
    


```java
import java.util.Calendar;

Calendar cal = Calendar.getInstance();

// Acessando informações
int ano = cal.get(Calendar.YEAR);
int mes = cal.get(Calendar.MONTH); // Lembre-se: Jan é 0
int dia = cal.get(Calendar.DAY_OF_MONTH);

// Manipulando datas
cal.add(Calendar.DAY_OF_MONTH, 5);  // Adiciona 5 dias
cal.add(Calendar.MONTH, -1);        // Remove 1 mês
cal.set(Calendar.HOUR_OF_DAY, 10);  // Define hora específica

Date dataConvertida = cal.getTime(); // Converte Calendar para Date
```

---

## 3. Formatação: SimpleDateFormat

Como `Date` e `Calendar` não imprimem bonito por padrão, usamos esta classe para formatar a saída.

|**Símbolo**|**Descrição**|**Exemplo**|
|---|---|---|
|**dd**|Dia do mês|09|
|**MM**|Mês numérico|03|
|**yyyy**|Ano completo|2026|
|**HH**|Hora (0-23)|14|
|**mm**|Minutos|45|
|**ss**|Segundos|30|


```java
import java.text.SimpleDateFormat;

SimpleDateFormat formatador = new SimpleDateFormat("dd/MM/yyyy HH:mm:ss");
String dataFormatada = formatador.format(new Date());

// Convertendo String para Date (Parse)
Date dataParseada = formatador.parse("25/12/2026 20:00:00");
```

---

## 4. Comparativo e Cuidados

|**Recurso**|**Característica**|**Recomendação**|
|---|---|---|
|**Date**|Simples, mas obsoleta.|Use apenas se bibliotecas antigas exigirem.|
|**Calendar**|Complexa e mutável.|Evite em novos projetos; difícil de testar.|
|**SimpleDateFormat**|**Não é Thread-Safe.**|Nunca declare como variável estática em Servlets/Web.|

---

## 5. Dicas de Produtividade no IntelliJ

- **Substituição por Java Time:** Se você começar a usar `Date` ou `Calendar`, o IntelliJ pode sugerir que você migre para `java.time.LocalDate` ou `java.time.ZonedDateTime`.
    
- **Inspeção de Constantes:** Ao usar `cal.get()`, o IntelliJ autocompleta as constantes de `Calendar`. Sempre prefira usar as constantes (`Calendar.MONTH`) em vez de números mágicos (`2`).
    
- **Tratamento de Exceções:** Lembre-se que o método `parse()` do `SimpleDateFormat` lança uma `ParseException`. O IntelliJ vai te obrigar a usar um bloco `try-catch` ou adicionar `throws` na assinatura do método.