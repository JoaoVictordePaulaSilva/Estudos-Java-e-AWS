## 1. O que é uma API?

**API** (_Application Programming Interface_) é um conjunto de regras que permite que um software "converse" com outro.

- **Analogia do Garçom:** * Você (Cliente) faz um pedido.
    
    - O Garçom (API) leva o pedido à Cozinha (Servidor).
        
    - A Cozinha prepara e o Garçom traz a comida (Resposta) de volta.
        
- **Função:** Abstrair a complexidade. Você não precisa saber como o banco de dados funciona, apenas como "pedir" os dados à API.
    

---

## 2. O que é REST?

**REST** (_Representational State Transfer_) é um **estilo de arquitetura** para sistemas distribuídos. Ele define um conjunto de restrições para que a comunicação via HTTP seja eficiente e escalável.

### Os 6 Princípios (Constraints) do REST:

1. **Client-Server:** Separação clara entre quem pede (Front/Mobile) e quem processa (Back).
    
2. **Stateless (Sem estado):** Cada requisição é independente. O servidor não guarda memória de requisições anteriores.
    
3. **Cacheable:** As respostas devem dizer se podem ou não ser cacheadas para melhorar a performance.
    
4. **Interface Uniforme:** Uso padronizado de recursos (URIs) e métodos HTTP.
    
5. **Sistema em Camadas:** O cliente não precisa saber se está falando com o servidor final ou com um intermediário (Load Balancer).
    
6. **Código sob Demanda (Opcional):** Capacidade de enviar código executável (como Scripts) para o cliente.
    

![REST Architecture Client-Server model, gerada com IA](https://encrypted-tbn0.gstatic.com/licensed-image?q=tbn:ANd9GcQ6KoU3ApEJC2ysb-VuRSVETB3zqOJ3wm0WeuSaPQF6jj9wsSIKSjP7WU-RkpwkO2gvjLrgNGYPCcWSgPa9VvPIdXgMNcBm8Kb47hjdpeTzje4xiGk)

---

## 3. REST vs. RESTful: Qual a diferença?

Embora usados como sinônimos no dia a dia, existe uma diferença técnica:

- **REST:** É o conceito, o conjunto de regras e princípios de design.
    
- **RESTful:** É o sistema que **aplica** rigorosamente os princípios do REST. Se a sua API segue as regras, ela é uma "API RESTful".
    

---

## 4. Métodos HTTP e Status Codes

No REST, usamos os métodos do protocolo HTTP para indicar a ação que queremos realizar no **Recurso** (Ex: `/usuarios`).

|**Método**|**Ação (CRUD)**|**Descrição**|
|---|---|---|
|**GET**|Read|Recupera dados de um recurso.|
|**POST**|Create|Cria um novo recurso no servidor.|
|**PUT**|Update|Atualiza um recurso inteiro (substituição).|
|**PATCH**|Update|Atualiza apenas uma parte do recurso.|
|**DELETE**|Delete|Remove um recurso.|

### Famílias de Status Codes (Respostas)

- **2xx (Sucesso):** `200 OK`, `201 Created`.
    
- **3xx (Redirecionamento):** `301 Moved Permanently`.
    
- **4xx (Erro do Cliente):** `400 Bad Request`, `401 Unauthorized`, `404 Not Found`.
    
- **5xx (Erro do Servidor):** `500 Internal Server Error`.
    

---

## 5. Anatomia de uma Requisição REST

Para uma pesquisa rápida, lembre-se que uma requisição é composta por:

1. **Endpoint (URL):** `https://api.exemplo.com/v1/produtos`
    
2. **Método:** `GET`, `POST`, etc.
    
3. **Headers (Cabeçalhos):** Metadados (Tipo de conteúdo, Tokens de segurança).
    
4. **Body (Corpo):** Os dados em si, geralmente em formato **JSON**.
    


```json
{
  "nome": "Teclado Mecânico",
  "preco": 350.00
}
```

---

## 6. Dicas de Produtividade no IntelliJ

- **HTTP Client:** O IntelliJ tem um cliente HTTP embutido fantástico. Em vez de usar o Postman, você pode criar um arquivo com extensão `.http` e escrever suas requisições lá para testar sua API direto no IDE.
    
- **JSON Viewer:** Ao receber respostas em JSON, o IntelliJ formata e permite que você navegue pelos campos facilmente no console.
    
- **Spring Web Sugestões:** Se você estiver usando o framework Spring, o IntelliJ sugere os endpoints e métodos baseados nas suas anotações `@RestController`.