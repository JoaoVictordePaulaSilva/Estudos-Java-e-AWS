A infraestrutura de um projeto Spring Boot moderno baseia-se em três pilares: o gerenciamento de dependências, a conteinerização do banco de dados e as propriedades de configuração do sistema. Sem essa base bem ajustada, o código das camadas superiores não consegue ser executado.

## 1. Gerenciamento de Dependências (pom.xml)

O Maven utiliza o arquivo `pom.xml` para baixar e organizar as bibliotecas necessárias. Em um projeto inicial de API, as dependências fundamentais são:

- **Spring Boot Starter Web:** Para criar os endpoints REST e rodar o servidor Tomcat.
    
- **Spring Data JPA:** Para a comunicação com o banco de dados.
    
- **MySQL Connector:** O driver que permite ao Java "falar" com o MySQL.
    
- **Lombok:** Para reduzir a escrita de código repetitivo.
    

**Exemplo de estrutura de dependência:**

```XML
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>

<dependency>
    <groupId>com.mysql</groupId>
    <artifactId>mysql-connector-j</artifactId>
    <scope>runtime</scope>
</dependency>
```

---

## 2. Banco de Dados em Container (Docker)

Em vez de instalar o MySQL diretamente no Windows, utilizamos o Docker. Isso garante que o ambiente de banco de dados seja idêntico para qualquer desenvolvedor que baixar o projeto.

**Vantagens:**

- Evita conflitos de portas no sistema operacional.
    
- Permite destruir e recriar o banco em segundos.
    
- Isola as configurações do banco do restante da máquina.
    

**Comando básico para subir o banco:**


```Bash
docker run --name mysql-gastos -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=controle_gastos -p 3306:3306 -d mysql:8.0
```

- `--name`: Nome do container.
    
- `-e`: Variáveis de ambiente (senha do root e nome do banco inicial).
    
- `-p`: Mapeamento da porta 3306 do container para a 3306 da sua máquina.
    

---

## 3. Configurações da Aplicação (application.properties)

Este arquivo, localizado em `src/main/resources`, funciona como o painel de controle da aplicação. É nele que o Spring busca as credenciais para se conectar ao banco que está rodando no Docker.

**Exemplo de configuração essencial:**


```Properties
# Conexão com o Banco de Dados
spring.datasource.url=jdbc:mysql://localhost:3306/controle_gastos
spring.datasource.username=root
spring.datasource.password=root

# Estratégia de geração das tabelas (Hibernate)
spring.jpa.hibernate.ddl-auto=update

# Mostrar no console o SQL que o Java está gerando
spring.jpa.show-sql=true
```

### O que significa o ddl-auto?

- **none:** O Spring não mexe na estrutura do banco.
    
- **update:** O Spring verifica suas classes Java e cria/altera as tabelas no banco automaticamente. Ideal para desenvolvimento.
    
- **create-drop:** Cria as tabelas quando o projeto inicia e apaga tudo quando ele desliga.
    

---

## 4. Ordem de Inicialização

Para que o projeto funcione sem erros de conexão, a ordem sempre deve ser:

1. **Docker Desktop:** Deve estar aberto.
    
2. **Container MySQL:** Deve estar em execução (Status: Running).
    
3. **IntelliJ/Aplicação:** O Play só deve ser dado após o banco estar pronto para receber conexões.