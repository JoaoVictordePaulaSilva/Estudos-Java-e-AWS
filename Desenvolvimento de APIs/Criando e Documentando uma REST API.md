## 1. Estrutura de um Controller REST

O Controller é a porta de entrada. Ele traduz requisições HTTP para chamadas de métodos Java.

- **`@RestController`**: Combina `@Controller` e `@ResponseBody`. Diz que a classe retornará JSON.
    
- **`@RequestMapping`**: Define a rota base (ex: `/api/produtos`).
    


```java
@RestController
@RequestMapping("/produtos")
@RequiredArgsConstructor // Injeção via construtor (Lombok)
public class ProdutoController {

    private final ProdutoService service;

    @GetMapping
    public List<ProdutoDTO> listarTodos() {
        return service.buscarTodos();
    }

    @PostMapping
    public ResponseEntity<ProdutoDTO> criar(@RequestBody ProdutoDTO dto) {
        ProdutoDTO novo = service.salvar(dto);
        return ResponseEntity.status(HttpStatus.CREATED).body(novo);
    }
}
```

---

## 2. Documentação com Swagger (SpringDoc OpenAPI)

Para o Spring Boot 3, a biblioteca padrão é o **SpringDoc OpenAPI**.

### Adicionando a Dependência (Maven)


```XML
<dependency>
    <groupId>org.springdoc</groupId>
    <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
    <version>2.3.0</version>
</dependency>
```

### Acessando a Interface

Após rodar o projeto, o Swagger estará disponível em:

`http://localhost:8080/swagger-ui/index.html`

---

## 3. Anotações Principais do Swagger

Você pode "enfeitar" sua documentação para torná-la legível para humanos.

|**Anotação**|**Onde usar**|**Descrição**|
|---|---|---|
|**`@Tag`**|Na classe Controller|Define um nome e descrição para o grupo de endpoints.|
|**`@Operation`**|No método|Resume o que o endpoint faz (ex: "Busca usuário por ID").|
|**`@ApiResponse`**|No método|Explica o que significa cada Status Code retornado.|
|**`@Schema`**|No DTO/Entidade|Dá nomes amigáveis e exemplos para os campos do JSON.|


```Java
@Operation(summary = "Lista todos os produtos", description = "Retorna uma lista paginada de produtos ativos")
@GetMapping
public List<ProdutoDTO> listar() { ... }
```

---

## 4. O Fluxo Completo da Requisição

Para uma pesquisa rápida, lembre-se da ordem de "passagem de bastão":

1. **Client (Postman/Browser):** Faz o `GET /produtos`.
    
2. **Controller:** Recebe a requisição e valida os dados de entrada.
    
3. **Service:** Aplica a regra de negócio (ex: "só listar se tiver estoque").
    
4. **Repository:** Busca os dados no PostgreSQL via JPA.
    
5. **Controller:** Transforma a Entidade em DTO e envia o JSON + `200 OK`.
    

---

## 5. Dicas de Produtividade no IntelliJ

- **Endpoints Tool Window:** No IntelliJ Ultimate, existe uma aba chamada **Endpoints** que lista todas as URLs do seu projeto de forma visual, permitindo testá-las ali mesmo.
    
- **Refatoração de Path:** Se você mudar o nome de um `@RequestMapping`, use o `Shift + F6` para garantir que todas as referências no projeto sejam atualizadas.
    
- **Testes Rápidos:** Use o arquivo `.http` do IntelliJ para salvar testes de requisições POST complexas e não precisar preencher o Swagger toda vez.
    

---

### Boas Práticas de API

- **Versionamento:** Use `/api/v1/recurso`. Isso evita quebrar apps antigos quando você mudar a API.
    
- **Substantivos, não verbos:** Use `/produtos` (correto) em vez de `/getProdutos` (errado). O método HTTP (`GET`) já diz que você quer "pegar".