## 1. Wrapper Classes

As classes Wrapper permitem que tipos primitivos sejam tratados como objetos. Isso é obrigatório ao trabalhar com Collections (List, Set, Map), que não aceitam primitivos.

### Tabela de Correspondência

|**Primitivo**|**Wrapper**|**Exemplo de Inicialização**|
|---|---|---|
|**int**|`Integer`|`Integer n = 10;`|
|**double**|`Double`|`Double d = 10.5d;`|
|**float**|`Float`|`Float f = 10.5f;`|
|**long**|`Long`|`Long l = 100L;`|
|**boolean**|`Boolean`|`Boolean b = true;`|
|**char**|`Character`|`Character c = 'A';`|
|**byte**|`Byte`|`Byte by = 1;`|
|**short**|`Short`|`Short sh = 1;`|

### Autoboxing e Unboxing

O Java faz a conversão automática entre o tipo primitivo e seu Wrapper correspondente.

- **Autoboxing:** Primitivo -> Wrapper.
    
- **Unboxing:** Wrapper -> Primitivo.
    



```Java
Integer wrapperInt = 50; // Autoboxing
int primitivoInt = wrapperInt; // Unboxing

// Vantagem: Wrappers podem ser nulos (útil em bancos de dados)
Integer valorOpcional = null; 
```

---

## 2. Map (Interface)

Diferente das outras coleções, o `Map` armazena pares de **Chave** e **Valor**. Cada chave é única e aponta para um único valor.

### Implementações Comuns

- **HashMap:** Mais rápido. Não garante ordem dos elementos.
    
- **LinkedHashMap:** Mantém a ordem de inserção.
    
- **TreeMap:** Mantém as chaves em ordem natural (ex: alfabética ou numérica).
    

### Exemplo de Uso



```Java
import java.util.HashMap;
import java.util.Map;

Map<String, Double> produtos = new HashMap<>();

// Inserir dados (Chave, Valor)
produtos.put("Notebook", 3500.0);
produtos.put("Mouse", 150.0);
produtos.put("Teclado", 250.0);

// Substituir valor (Chaves são únicas)
produtos.put("Notebook", 3200.0); 

// Acessar valor pela chave
Double precoMouse = produtos.get("Mouse");

// Verificar existência
boolean temTeclado = produtos.containsKey("Teclado");
```

---

## 3. Métodos Essenciais de Consulta

|**Método**|**Função**|
|---|---|
|`put(K, V)`|Adiciona ou substitui um par.|
|`get(K)`|Retorna o valor da chave ou `null`.|
|`remove(K)`|Remove o par baseado na chave.|
|`containsKey(K)`|Retorna true se a chave existir.|
|`keySet()`|Retorna um `Set` com todas as chaves.|
|`values()`|Retorna uma `Collection` com todos os valores.|
|`entrySet()`|Retorna o conjunto de pares (chave + valor).|

### Percorrendo um Map (Lambda)



```Java
produtos.forEach((chave, valor) -> {
    System.out.println("Produto: " + chave + " | Preço: " + valor);
});
```

---

## 4. Dicas de Produtividade no IntelliJ

- **Mapas Imutáveis:** Se precisar de um mapa fixo, use `Map.of("Chave", "Valor", "Chave2", "Valor2")`. O IntelliJ sugerirá isso caso você tente adicionar itens manualmente um a um após a criação.
    
- **Visualização no Debugger:** Ao debugar um Map, o IntelliJ mostra a visão "Value" de forma clara, facilitando ver qual chave está ligada a qual valor.
    
- **Verificação de Nulo:** Ao fazer Unboxing de um Wrapper que pode ser nulo, o IntelliJ emitirá um aviso de **NullPointerException** em potencial. Sempre verifique se o valor não é `null` antes de converter para primitivo.