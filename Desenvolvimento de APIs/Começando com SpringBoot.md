Este guia resume os conceitos fundamentais e a configuração inicial para projetos Java Backend modernos, utilizando o ecossistema Spring.

## 1. O que é o Spring Boot?

O Spring Boot é um **framework** que facilita a criação de aplicações Java "prontas para rodar". Ele elimina a necessidade de configurações manuais complexas (o famoso XML gigante de antigamente) através da **Convenção sobre Configuração**.

- **Servidor Embutido:** Ele já vem com um servidor (Tomcat) dentro do arquivo final.
    
- **Starters:** Conjuntos de dependências pré-configuradas (ex: `spring-boot-starter-web`).
    
- **Auto-Configuration:** O Spring "adivinha" o que você precisa com base nas bibliotecas que você adicionou ao projeto.
    

---

## 2. Gerenciadores de Build: Maven vs Gradle

Para projetos Java profissionais, usamos ferramentas que gerenciam as bibliotecas (dependências) e o ciclo de vida do software.

|**Característica**|**Maven (Recomendado)**|**Gradle**|
|---|---|---|
|**Configuração**|Arquivo `pom.xml` (Baseado em XML)|Arquivo `build.gradle` (Groovy/Kotlin)|
|**Padrão de Mercado**|Altamente utilizado em Java corporativo.|Muito comum em apps Android e projetos Kotlin.|
|**Curva de Aprendizado**|Mais rígido, porém mais fácil de entender a estrutura.|Mais flexível e performático, porém mais complexo.|

---

## 3. Conceitos de Empacotamento (Packaging)

Ao finalizar seu código, você precisa "gerar" o programa para rodar na nuvem (AWS):

- **JAR (Java ARchive):** O padrão ouro do Spring Boot. Contém o código + servidor web. Roda de forma independente.
    
- **WAR (Web ARchive):** Usado em servidores legados. Requer um servidor externo (como Tomcat ou Glassfish) pré-instalado.
    

---

## 4. Passo a Passo: Criando o Projeto no IntelliJ IDEA

1. **Menu New Project:** Selecione **Spring Boot** (Spring Initializr) no menu lateral.
    
2. **Project Metadata:**
    
    - **Type:** Escolha `Maven`.
        
    - **JDK:** Use a versão mais recente (ex: 21) para aproveitar as melhorias de performance.
        
    - **Packaging:** Selecione `JAR`.
        
3. **Dependências Essenciais para o Desafio (Starters):**
    
    - `Spring Web`: Para criar APIs REST e usar o protocolo HTTP.
        
    - `OpenFeign`: Cliente HTTP declarativo (facilita consumir APIs como a PokeAPI).
        
    - `Lombok`: Anotações que reduzem código repetitivo (gera Getters/Setters sozinho).
        
    - `H2 Database`: Banco de dados em memória para testes rápidos sem instalação externa.
        
    - `Spring Data JPA`: Facilita a comunicação com o banco de dados usando Objetos Java.
        

---

## 5. Estrutura de Pastas Padrão

Após a criação, o Spring organiza seu projeto assim:

- `src/main/java`: Onde fica seu código `.java` (Controllers, Services, Models).
    
- `src/main/resources`: Arquivos de configuração (`application.properties`) e arquivos estáticos.
    
- `src/test/java`: Onde você escreve os testes automatizados da sua aplicação.
    
- `pom.xml`: O "cérebro" do Maven onde todas as dependências são listadas.
    

---

> **Dica de Ouro:** Sempre que adicionar uma dependência nova no `pom.xml`, lembre-se de clicar no ícone do Maven (o "M" com setinhas) para que o IntelliJ baixe as bibliotecas e o código compile corretamente.