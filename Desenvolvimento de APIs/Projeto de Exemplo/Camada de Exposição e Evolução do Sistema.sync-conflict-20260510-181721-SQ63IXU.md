A camada de Controller é responsável por disponibilizar as funcionalidades do sistema para o mundo externo. Além disso, para que um sistema seja considerado "Enterprise", ele deve evoluir para padrões que protejam os dados e forneçam respostas claras em caso de erros.

## 1. REST Controllers: A Porta de Entrada

Uma Controller mapeia os verbos HTTP para métodos Java. Ela utiliza anotações para identificar o que deve ser feito com cada requisição que chega à porta 8080.

**Verbos HTTP fundamentais:**

- **GET:** Solicita dados (Listagem ou Busca por ID).
    
- **POST:** Envia novos dados para criação.
    
- **PUT:** Envia dados para atualização completa.
    
- **DELETE:** Solicita a remoção (ou desativação) de um registro.
    

**Exemplo de Controller Profissional:**



```java
@RestController
@RequestMapping("/gastos")
public class GastoController {

    @Autowired
    private GastoService service;

    @GetMapping
    public List<Gasto> listar() {
        return service.listarAtivos();
    }

    @PostMapping
    public Gasto criar(@RequestBody Gasto gasto) {
        return service.salvar(gasto);
    }

    @DeleteMapping("/{id}")
    public void excluir(@PathVariable Long id) {
        service.desativar(id);
    }
}
```

- `@RequestBody`: Converte o JSON recebido em um objeto Java.
    
- `@PathVariable`: Captura valores variáveis na URL (como o ID no delete).
    

---

## 2. Padrão DTO (Data Transfer Object)

Em sistemas reais, nunca expomos a `@Entity` do banco de dados diretamente na Controller. Usamos DTOs para filtrar o que o cliente pode ver ou enviar.

**Por que usar DTOs?**

- **Segurança:** Evita que campos sensíveis (como senhas ou flags internas) sejam expostos.
    
- **Performance:** Você pode retornar apenas os 3 campos necessários em vez de uma tabela com 50 colunas.
    
- **Desacoplamento:** O banco de dados pode mudar sem quebrar o contrato da API com o front-end.
    

**Exemplo de DTO Simples:**

Java

```
// Apenas os dados que o usuário precisa ver
public record GastoResponseDTO(Long id, String descricao, Double valor) {}
```

---

## 3. Tratamento Global de Exceções

Um sistema profissional não permite que erros internos (Stacktraces) vazem para o usuário. Utilizamos o `@ControllerAdvice` para capturar exceções e padronizar a resposta.

**Exemplo de Handler de Erros:**

Java

```
@ControllerAdvice
public class ErrorHandler {

    @ExceptionHandler(RuntimeException.class)
    public ResponseEntity<String> lidarComErro(RuntimeException ex) {
        // Retorna status 400 (Bad Request) com a mensagem customizada
        return ResponseEntity.status(400).body(ex.getMessage());
    }
}
```

Dessa forma, se a sua Service lançar um "Gasto não encontrado", o usuário receberá uma mensagem limpa em vez de um erro 500 genérico.

---

## 4. Maturidade e Boas Práticas Finais

Ao concluir este projeto, o sistema atingiu um nível de maturidade que inclui:

1. **Inversão de Controle:** O Spring gerencia as instâncias das classes via `@Autowired`.
    
2. **Persistência Robusta:** MySQL rodando isolado em Docker.
    
3. **Integridade de Dados:** Uso de Soft Delete para preservar o histórico.
    
4. **Código Limpo:** Separação clara entre o que é Banco, o que é Lógica e o que é Web.
    

## 5. Próximos Passos de Estudo

Para dar continuidade à evolução como desenvolvedor Backend Java, os tópicos recomendados para pesquisa após consolidar esta base são:

- **Spring Security + JWT:** Para autenticação e autorização de usuários.
    
- **JUnit 5 & Mockito:** Para criação de testes automatizados na camada de Service.
    
- **Flyway:** Para versionamento de scripts SQL.
    
- **Swagger (SpringDoc):** Para documentação automática dos endpoints da API.