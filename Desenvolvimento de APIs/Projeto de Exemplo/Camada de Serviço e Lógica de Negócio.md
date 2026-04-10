A camada de serviço (Service Layer) atua como um intermediário entre a Controller e o Repository. Sua função principal é isolar as regras de negócio da infraestrutura de rede e de banco de dados. Em sistemas profissionais, nenhuma lógica de decisão deve estar na Controller.

## 1. Por que isolar a Lógica de Negócio?

Se você colocar a lógica na Controller, seu código fica "acoplado". Isso significa que se você precisar criar uma nova forma de entrada (como um comando via terminal ou uma tarefa agendada), você terá que repetir toda a lógica de validação.

**Vantagens do Service:**

- **Reutilização:** O mesmo método de salvar pode ser chamado por diferentes partes do sistema.
    
- **Testabilidade:** É muito mais simples criar testes unitários para uma classe de serviço.
    
- **Organização:** A Controller foca em HTTP, enquanto a Service foca no Negócio.
    

---

## 2. Injeção de Dependência (@Service e @Autowired)

Para que o Spring gerencie a Service, utilizamos a anotação `@Service`. Para que a Service consiga utilizar o banco de dados, "injetamos" o Repository dentro dela.

**Exemplo de Injeção:**

Java

```
@Service
public class GastoService {

    @Autowired
    private GastoRepository repository;

    // Métodos da classe...
}
```

---

## 3. Implementação de Regras de Negócio

Regras de negócio são restrições ou cálculos que definem como o sistema deve se comportar.

**Exemplo: Validação de valor positivo**

Antes de enviar o objeto para o Repository, a Service deve garantir que os dados são válidos.

Java

```
public Gasto salvar(Gasto gasto) {
    if (gasto.getValor() <= 0) {
        throw new RuntimeException("O valor do gasto deve ser positivo.");
    }
    return repository.save(gasto);
}
```

---

## 4. Soft Delete na Prática (Exclusão Lógica)

Como discutido, uma das melhores práticas em banco de dados é evitar a exclusão física (`DELETE`). Em vez disso, alteramos o status do registro.

**Passo a passo da lógica:**

1. Buscamos o objeto no banco pelo ID.
    
2. Verificamos se ele existe.
    
3. Alteramos o atributo `ativo` para `false`.
    
4. Salvamos a alteração.
    

**Exemplo de código:**

Java

```
public void excluirLogico(Long id) {
    // Busca o gasto ou lança erro se não encontrar
    Gasto gasto = repository.findById(id)
            .orElseThrow(() -> new RuntimeException("Gasto não encontrado"));

    // Define como inativo em vez de apagar
    gasto.setAtivo(false);

    // Persiste a alteração no banco
    repository.save(gasto);
}
```

---

## 5. Filtragem de Dados

Ao utilizar o Soft Delete, a Service também se torna responsável por garantir que o usuário só veja os dados ativos nas buscas comuns.

**Exemplo de listagem filtrada:**

Java

```
public List<Gasto> listarSomenteAtivos() {
    return repository.findAll().stream()
            .filter(gasto -> gasto.isAtivo())
            .toList();
}
```

---

## 6. Boas Práticas na Camada de Serviço

1. **Tratamento de Erros:** Não retorne `null` se algo der errado; lance exceções descritivas.
    
2. **Transacionalidade:** Use `@Transactional` (do Spring) em métodos que fazem mais de uma alteração no banco. Isso garante que, se um passo falhar, todas as alterações anteriores sejam canceladas (rollback).
    
3. **Métodos Atômicos:** Cada método da Service deve realizar apenas uma tarefa lógica bem definida.