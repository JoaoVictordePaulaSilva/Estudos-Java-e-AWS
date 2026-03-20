
## 1. Conceitos Gerais

O Spring Core funciona baseado em dois pilares:

- **Inversão de Controle (IoC):** O Spring toma as rédeas do ciclo de vida dos objetos.
    
- **Injeção de Dependência (DI):** Em vez de você dar um `new Objeto()`, o Spring "injeta" a instância pronta onde for necessária usando `@Autowired`.

![[Spring Framework Runtime.png]]

---

## 2. Beans vs. Components

Ambos são objetos gerenciados pelo Spring, mas usados em contextos diferentes:

- **`@Component`:** Você anota em cima da sua classe. É a forma automática (o Spring escaneia e cria o objeto).
    
    - _Variações:_ `@Service` (lógica de negócio), `@Repository` (acesso a dados), `@Controller` (web).
        
- **`@Bean`:** Usado dentro de uma classe de `@Configuration`. É a forma manual. Útil quando você precisa configurar um objeto de uma biblioteca de terceiros que você não pode editar o código-fonte.
    

---

## 3. Scopes (Escopos)

Define "quanto tempo" um Bean vive:

- **Singleton (Padrão):** Uma única instância para toda a aplicação.
    
- **Prototype:** Uma nova instância toda vez que for solicitada.
    
- **Request/Session:** Uma instância por requisição HTTP ou sessão de usuário.
    

---

## 4. Application Properties

Localizado em `src/main/resources/application.properties` (ou `.yml`), é onde configuramos o comportamento da aplicação (porta do servidor, conexão com banco, etc).

Properties

```
server.port=8080
spring.datasource.url=jdbc:postgresql://localhost:5432/meu_banco
spring.datasource.username=postgres
spring.datasource.password=123
spring.jpa.hibernate.ddl-auto=update
```

---

## 5. ORM e JPA com PostgreSQL

- **ORM (Object-Relational Mapping):** Técnica para mapear classes Java para tabelas do banco.
    
- **JPA (Java Persistence API):** É a especificação (o "contrato").
    
- **Hibernate:** É a implementação mais famosa da JPA (quem faz o trabalho pesado).
    

### Exemplo de Entidade

Java

```
@Entity
@Table(name = "tb_usuarios")
public class Usuario {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @Column(nullable = false)
    private String nome;
    // getters e setters
}
```

---

## 6. JPA Repository

Interface mágica que já traz os métodos CRUD prontos (`save`, `findAll`, `findById`, `delete`).

Java

```
@Repository
public interface UsuarioRepository extends JpaRepository<Usuario, Long> {
    // O Spring cria a implementação em tempo de execução
    List<Usuario> findByNomeContaining(String nome); // Query Method automático
}
```

---

## 7. Dicas de Produtividade no IntelliJ

- **Spring Initializr:** Você não precisa ir ao site. No IntelliJ, vá em `File > New > Project > Spring Initializr`.
    
- **Database Tool:** No lado direito do IntelliJ, use a aba **Database**. Conecte seu PostgreSQL ali para ver as tabelas criadas pelo Hibernate em tempo real sem sair da IDE.
    
- **Dependency Injection Check:** O IntelliJ coloca um ícone de "folha verde" ao lado de classes gerenciadas pelo Spring. Se a folha não estiver lá, seu `@Autowired` vai falhar (NullPointerException).
    
- **Lombok:** Use a biblioteca Lombok (`@Data`, `@NoArgsConstructor`) para evitar escrever Getters/Setters manuais e manter seu código limpo.