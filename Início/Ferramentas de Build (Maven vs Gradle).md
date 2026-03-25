## 1. Apache Maven (O Padrão de Mercado)

Baseado em **XML**, o Maven segue o princípio de _"Convenção sobre Configuração"_. Ele possui uma estrutura de pastas rígida que, se seguida, exige quase zero configuração.

- **Arquivo Principal:** `pom.xml` (Project Object Model).
    
- **Vantagem:** Muito estável, fácil de entender o que está acontecendo e padrão na maioria das empresas.
    
- **Desvantagem:** O XML pode ficar muito grande e verboso; difícil de criar lógicas personalizadas no build.
    

XML

```
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-core</artifactId>
    <version>6.1.0</version>
</dependency>
```

---

## 2. Gradle (A Evolução Flexível)

Baseado em **DSL** (Domain Specific Language) usando **Groovy** ou **Kotlin**. É a ferramenta padrão para desenvolvimento Android e projetos modernos de alta performance.

- **Arquivo Principal:** `build.gradle` ou `build.gradle.kts`.
    
- **Vantagem:** Muito mais rápido (usa cache e builds incrementais); permite escrever código real para customizar o processo de build.
    
- **Desvantagem:** Curva de aprendizado maior; a flexibilidade pode gerar scripts de build confusos se não houver cuidado.
    

Groovy

```
// Exemplo de dependência no build.gradle
dependencies {
    implementation 'org.springframework:spring-core:6.1.0'
}
```

---

## 3. Comparativo Rápido

|**Característica**|**Maven**|**Gradle**|
|---|---|---|
|**Linguagem**|XML (Declarativo)|Groovy/Kotlin (Programável)|
|**Performance**|Boa (linear)|Excelente (incremental/cache)|
|**Flexibilidade**|Rígida (focada em plugins)|Alta (focada em scripts)|
|**Gerenciamento de Dependências**|Estrito (conflitos são chatos)|Inteligente (resolve conflitos melhor)|
|**Popularidade**|Dominante no Backend/Legado|Dominante em Android/Spring moderno|

---

## 4. Dicas para Migração

### Do Maven para o Gradle

O Gradle possui um comando nativo que tenta converter o projeto automaticamente:

1. Abra o terminal na pasta do projeto Maven (onde está o `pom.xml`).
    
2. Digite: `gradle init`.
    
3. Selecione a opção para converter o projeto Maven encontrado.
    
4. **Dica:** Verifique se os nomes das dependências e as versões foram mapeados corretamente no novo `build.gradle`.
    

### Do Gradle para o Maven

Não existe um comando nativo "gradle to maven". Você precisará:

1. Criar um `pom.xml` manualmente.
    
2. Copiar as `dependencies` do Gradle para o formato XML do Maven.
    
3. Ajustar os plugins (ex: plugin de compilação, plugin do Spring Boot).
    

---

## 5. Dicas de Produtividade no IntelliJ

- **Janela de Ferramentas:** No lado direito do IntelliJ, existem as abas **Maven** e **Gradle**. Use-as para rodar comandos como `clean`, `install` ou `build` sem precisar digitar no terminal.
    
- **Auto-reload:** Sempre que alterar o `pom.xml` ou `build.gradle`, clique no ícone do "Elefantinho" (Gradle) ou do "M" (Maven) que aparece no canto superior direito para sincronizar as dependências.
    
- **Dependency Analyzer:** O IntelliJ tem uma ferramenta visual para mostrar se você tem bibliotecas duplicadas ou em conflito. No `pom.xml`, clique com o botão direito > **Maven** > **Show Dependencies**.