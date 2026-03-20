## 1. Conceitos Fundamentais

Segurança se resume a dois pilares:

- **Autenticação:** Você é quem diz ser? (Login/Senha).
    
- **Autorização:** Você tem permissão para fazer isso? (Perfil de ADMIN, USER, etc).
    

---

## 2. O Fluxo JWT (JSON Web Token)

Como APIs REST devem ser _stateless_ (sem sessão no servidor), usamos o JWT:

1. O cliente envia **Login/Senha**.
    
2. O servidor valida e devolve um **Token** assinado (uma String criptografada).
    
3. O cliente guarda esse token e o envia no **Header** (`Authorization: Bearer <token>`) em todas as próximas requisições.
    
4. O servidor apenas valida a assinatura do token, sem precisar consultar o banco o tempo todo.
    

---

## 3. Componentes Principais do Spring Security

|**Componente**|**Função**|
|---|---|
|**`SecurityFilterChain`**|O "porteiro". Define quais rotas são públicas (ex: `/login`) e quais são protegidas.|
|**`UserDetailsService`**|Interface que você implementa para buscar o usuário no banco de dados.|
|**`PasswordEncoder`**|Define o algoritmo de hash (geralmente `BCrypt`) para não salvar senhas em texto puro.|
|**`OncePerRequestFilter`**|Filtro personalizado que intercepta a requisição, lê o JWT e autentica o usuário.|

---

## 4. Exemplo de Configuração (SecurityChain)

No Spring Boot 3, a configuração é feita de forma funcional:


```Java
@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        return http
            .csrf(csrf -> csrf.disable()) // Desativado para APIs Stateless
            .sessionManagement(sm -> sm.sessionCreationPolicy(SessionCreationPolicy.STATELESS))
            .authorizeHttpRequests(req -> {
                req.requestMatchers(HttpMethod.POST, "/login").permitAll();
                req.requestMatchers("/admin/**").hasRole("ADMIN");
                req.anyRequest().authenticated();
            })
            .addFilterBefore(securityFilter, UsernamePasswordAuthenticationFilter.class)
            .build();
    }
}
```

---

## 5. Controle de Acesso por Anotações

Você pode restringir métodos específicos diretamente no Controller usando `@PreAuthorize`:

```Java

@DeleteMapping("/{id}")
@PreAuthorize("hasRole('ADMIN')")
public ResponseEntity deletar(@PathVariable Long id) {
    service.excluir(id);
    return ResponseEntity.noContent().build();
}
```

---

## 6. Integrando com Swagger

Para testar rotas protegidas no Swagger, você precisa configurar o "Cadeado" (Security Scheme) no seu Bean do OpenAPI:

```Java

@Bean
public OpenAPI customOpenAPI() {
    return new OpenAPI()
        .components(new Components()
            .addSecuritySchemes("bearer-key",
                new SecurityScheme().type(SecurityScheme.Type.HTTP).scheme("bearer").bearerFormat("JWT")));
}
```

---

## 7. Dicas de Produtividade no IntelliJ

- **BCrypt Generator:** Não invente sua criptografia. O IntelliJ ajuda a identificar se você está comparando senhas de forma insegura (usando `==` em vez do `passwordEncoder.matches()`).
    
- **Debug de Filtros:** Se você levar um **403 Forbidden** inesperado, coloque um breakpoint dentro do seu `OncePerRequestFilter`. É ali que a maioria dos erros de "token inválido" acontece.
    
- **Environment Variables:** Nunca deixe sua `JWT_SECRET` exposta no `application.properties`. Use variáveis de ambiente no IntelliJ (`Run > Edit Configurations > Environment Variables`).