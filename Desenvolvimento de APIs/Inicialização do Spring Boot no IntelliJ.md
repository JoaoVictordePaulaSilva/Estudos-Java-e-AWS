## 1. O Passo a Passo (New Project)

1. Abra o IntelliJ e vá em **File > New > Project**.
    
2. No menu à esquerda, selecione **Spring Initializr**.
    
    - _Nota: Se estiver na versão Community e não ver essa opção, use o site [start.spring.io](https://start.spring.io/) e importe o projeto._
        
3. **Configurações iniciais:**
    
    - **Name:** `nome-do-seu-projeto` (use kebab-case).
        
    - **Language:** Java.
        
    - **Type:** Maven (ou Gradle, conforme sua preferência).
        
    - **Group:** `com.seuusuario` (ex: `com.dev.projeto`).
        
    - **Artifact:** `nome-do-projeto`.
        
    - **Java Version:** 17 ou 21 (LTS - Long Term Support).
        
4. **Seleção de Dependências (As essenciais):**
    
    - **Spring Web:** Para criar APIs REST.
        
    - **Spring Data JPA:** Para persistência no banco.
        
    - **PostgreSQL Driver:** Para conexão com o banco.
        
    - **Lombok:** Para reduzir código boilerplate (Getters/Setters).
        
    - **Spring Boot DevTools:** Para restart automático ao salvar.
        

---

## 2. Estrutura de Pastas (Boas Práticas)

O Spring Boot segue uma arquitetura em camadas. Organize seu pacote principal (`src/main/java/com/exemplo`) assim:

- `model` ou `entity`: Classes que representam as tabelas do banco.
    
- `repository`: Interfaces que herdam de `JpaRepository`.
    
- `service`: Onde fica a "inteligência" do sistema (regras de negócio).
    
- `controller`: Onde ficam os Endpoints (Porta de entrada da API).
    
- `dto`: (Data Transfer Object) Para trafegar dados entre camadas sem expor a entidade do banco.
    
- `config`: Classes de configuração (Beans, Security, etc).
    

---

## 3. O "Checklist" Pós-Criação

Assim que o projeto abrir:

1. **Habilite o Annotation Processing:** Vá em `Settings > Build, Execution, Deployment > Compiler > Annotation Processors` e marque **Enable annotation processing** (necessário para o Lombok funcionar).
    
2. **Configure o `application.properties`:** Sem isso, o projeto não sobe se você adicionou a dependência de banco de dados.
    
3. **Verifique o ícone do Maven/Gradle:** No canto superior direito, clique no ícone de "refresh" para baixar todas as dependências.
    

---

## 4. Dicas de Ouro (Pro Tips)

### Injeção de Dependência

**Evite** o uso de `@Autowired` diretamente em atributos (Field Injection). A boa prática atual é usar **Constructor Injection**.

- _Dica no IntelliJ:_ Use a anotação do Lombok `@RequiredArgsConstructor` na classe e declare seus atributos como `private final`. O Spring injetará automaticamente.
    

### Live Reload

No IntelliJ, para o **DevTools** funcionar 100% ao salvar:

1. Vá em `Settings > Advanced Settings`.
    
2. Marque a opção: **Allow auto-make to start even if developed application is currently running**.
    

### Profiles

Nunca coloque senhas de produção no arquivo principal. Use o `application-dev.properties` para desenvolvimento local e `application-prod.properties` para o servidor real.

---

## 5. Atalhos Úteis no IntelliJ para Spring

|**Atalho**|**Ação**|
|---|---|
|`Ctrl + F9`|Recompila o projeto (ativa o DevTools).|
|`Alt + Insert`|Gera construtores, métodos ou novas classes rapidamente.|
|`Shift + Shift`|Busca qualquer arquivo, classe ou configuração no projeto.|
|`Ctrl + Alt + V`|Extrai uma expressão para uma variável local.|