A camada de persistência é responsável por transformar objetos Java em registos nas tabelas do banco de dados (e vice-versa). No ecossistema Spring Boot, isto é feito através da **JPA (Jakarta Persistence API)** e do **Hibernate**.

## 1. O Conceito de ORM (Object-Relational Mapping)

O mapeamento objeto-relacional elimina a necessidade de escrever comandos SQL manuais para operações básicas. O Hibernate (que é a implementação da JPA) funciona como um tradutor:

- **Lado Java:** Você lida com Classes e Objetos.
    
- **Lado SQL:** O Hibernate gera as Tabelas e Linhas.
    

---

## 2. Estrutura de uma Entidade (Model)

Uma Entidade é uma classe Java que representa uma tabela. Para que o Spring a reconheça, utilizamos anotações específicas.

**Anotações de Identidade:**

- `@Entity`: Define que a classe é uma tabela.
    
- `@Table`: Opcional, usada para definir o nome exato da tabela no banco (ex: `tb_gastos`).
    
- `@Id`: Indica qual o atributo é a Chave Primária (Primary Key).
    
- `@GeneratedValue`: Define como o ID será gerado. O padrão `IDENTITY` utiliza o auto-incremento do banco de dados.
    

**Exemplo de Mapeamento:**


```java
@Entity
@Table(name = "tb_gasto")
@Data // Lombok: gera getters/setters automaticamente
public class Gasto {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "txt_descricao", nullable = false)
    private String descricao;

    private Double valor;

    @Column(length = 50)
    private String categoria;
}
```

- `@Column`: Usada quando o nome da coluna no banco deve ser diferente do nome da variável ou para definir restrições como `nullable = false`.
    

---

## 3. O Papel do Lombok na Persistência

Em sistemas Java antigos, metade do ficheiro da entidade era preenchido com Getters e Setters. O Lombok limpa o código:


```java
@Data // Inclui @Getter, @Setter, @EqualsAndHashCode e @ToString
@NoArgsConstructor // Construtor vazio (obrigatório para a JPA)
@AllArgsConstructor // Construtor com todos os campos
public class Exemplo {
    private Long id;
}
```

---

## 4. Repositórios: A Abstração do Acesso a Dados

O **Spring Data JPA** introduz o conceito de `JpaRepository`. Em vez de criar classes que implementam o acesso ao banco, criamos apenas interfaces.

**Estrutura do Repository:**


```java
@Repository
public interface GastoRepository extends JpaRepository<Gasto, Long> {
    // Métodos herdados automaticamente:
    // save(S entity) - Salva ou atualiza
    // findAll() - Retorna todos os registos
    // findById(ID id) - Busca por chave primária
    // deleteById(ID id) - Remove por chave primária
}
```

Ao estender `JpaRepository<Gasto, Long>`, você informa ao Spring que este repositório lida com a entidade `Gasto` e que o tipo do ID dela é `Long`.

---

## 5. Derived Queries (Consultas por Nome de Método)

Uma funcionalidade poderosa da JPA é criar consultas SQL complexas apenas nomeando o método na interface do repositório:


```java
public interface GastoRepository extends JpaRepository<Gasto, Long> {
    
    // Gera automaticamente: SELECT * FROM tb_gasto WHERE categoria = ?
    List<Gasto> findByCategoria(String categoria);

    // Gera automaticamente: SELECT * FROM tb_gasto WHERE valor > ?
    List<Gasto> findByValorGreaterThan(Double valor);
}
```

---

## 6. Boas Práticas na Persistência

1. **Sempre utilize Classes Wrapper:** Use `Long` e `Double` em vez de `long` e `double`. Tipos primitivos não podem ser nulos, o que pode causar erros ao ler dados do banco.
    
2. **Naming Strategy:** Por padrão, o Hibernate converte `camelCase` (Java) para `snake_case` (SQL). Exemplo: `dataPagamento` vira `data_pagamento`.
    
3. **Construtor Vazio:** Toda entidade JPA deve ter um construtor sem argumentos para que o Hibernate consiga instanciá-la.