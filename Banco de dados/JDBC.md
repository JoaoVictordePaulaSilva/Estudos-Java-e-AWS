## 1. Conexão Base: O JDBC moderno

O JDBC é a API de baixo nível. No Java 21, usamos o **Try-with-resources** (que aprendemos na aula de Exceções) para garantir que a conexão feche sozinha, evitando vazamentos de memória (_memory leaks_).

### Estrutura de Conexão (Caminho "Raiz")

```java
String url = "jdbc:mysql://localhost:3306/meu_banco";
String user = "root";
String password = "password";

String sql = "SELECT id, nome FROM tb_produtos WHERE st_ativo = ?";

try (Connection conn = DriverManager.getConnection(url, user, password);
     PreparedStatement pstmt = conn.prepareStatement(sql)) {
    
    pstmt.setBoolean(1, true); // Define o parâmetro st_ativo
    
    try (ResultSet rs = pstmt.executeQuery()) {
        while (rs.next()) {
            System.out.println(rs.getLong("id") + " - " + rs.getString("nome"));
        }
    }
} catch (SQLException e) {
    e.printStackTrace();
}
```

> **Dica de Segurança:** Nunca concatene strings no SQL. Use sempre `PreparedStatement` com `?` para evitar **SQL Injection**.

---

## 2. A Integração Moderna: Spring Data JPA

Em projetos reais com Spring Boot, você não escreve o JDBC na mão. Você usa o **JPA (Java Persistence API)**, que mapeia sua classe Java diretamente para a tabela.

### O Fluxo de Integração:

1. **Entidade:** Uma classe Java com `@Entity`.
    
2. **Repository:** Uma interface que faz a ponte com o SQL.
    
3. **Service:** Onde a lógica de Java e SQL se encontram.
    

---

## 3. Mapeando Relacionamentos no Java

Aqui é onde o Java 21 e o SQL se interligam de forma avançada.

```java
@Entity
public class Produto {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String nome;

    @ManyToOne // Relacionamento Muitos para Um (N:1)
    @JoinColumn(name = "categoria_id") // A Chave Estrangeira no SQL
    private Categoria categoria;

    private boolean stAtivo = true;
}
```

---

## 4. Consultas Customizadas (JPQL e Native Query)

Às vezes, o método padrão do JPA não é suficiente. Você pode escrever SQL puro dentro do seu código Java:


```java
public interface ProdutoRepository extends JpaRepository<Produto, Long> {

    // JPQL (Linguagem de consulta baseada em Objetos)
    @Query("SELECT p FROM Produto p WHERE p.preco > :limite AND p.stAtivo = true")
    List<Produto> buscarProdutosCaros(BigDecimal limite);

    // Native Query (SQL Puro do MySQL)
    @Query(value = "SELECT * FROM tb_produtos WHERE st_ativo = 1 ORDER BY RAND() LIMIT 5", nativeQuery = true)
    List<Produto> buscarCincoAleatorios();
}
```

---

## 5. Boas Práticas na Integração (Checklist)

- **Connection Pool:** Em produção, nunca abra uma conexão do zero para cada usuário. Use o **HikariCP** (padrão do Spring Boot), que mantém um "pool" de conexões abertas e prontas.
    
- **Transactions (`@Transactional`):** Use esta anotação nos métodos do seu _Service_. Se o método der erro no meio do caminho, o Spring faz o **Rollback** no banco automaticamente.
    
- **DTOs:** Nunca retorne a sua `@Entity` (que representa o SQL) direto para o Frontend. Converta para um **Record** (recurso moderno do Java) para trafegar apenas o necessário.
    

```java
// Java 21 Record: Simples, imutável e performático para DTOs
public record ProdutoDTO(Long id, String nome, BigDecimal preco) {}
```

---

## 6. Dicas de Produtividade no IntelliJ

- **Inspeção de Query:** O IntelliJ tem uma inteligência chamada _Language Injection_. Se você digitar um SQL dentro de uma String no Java, ele colore o código e valida se as tabelas existem no seu banco real.
    
- **Geração de Entidades:** No painel **Database**, clique com o botão direito em uma tabela > **Scripted Extensions > Generate POJOs**. O IntelliJ cria a classe `@Entity` do Java baseada na sua tabela MySQL automaticamente.
    
- **Logs do SQL:** Para ver o que o Java está mandando para o banco no console, adicione no seu `application.properties`: `spring.jpa.show-sql=true` `spring.jpa.properties.hibernate.format_sql=true`