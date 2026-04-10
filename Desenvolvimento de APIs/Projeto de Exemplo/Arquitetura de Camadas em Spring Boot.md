A arquitetura de camadas (ou Multitier Architecture) é o padrão utilizado para organizar o código de forma que cada parte do sistema tenha uma responsabilidade única e bem definida. Em vez de escrever todo o código em um único arquivo, dividimos a aplicação para facilitar a manutenção, os testes e a escalabilidade.

## 1. O Fluxo de uma Requisição

Para entender as camadas, imagine o caminho que os dados percorrem quando você solicita a lista de gastos no navegador:

1. O **Cliente** (Navegador/Postman) faz uma requisição para a **Controller**.
    
2. A **Controller** recebe o pedido e o encaminha para a **Service**.
    
3. A **Service** aplica as regras necessárias e pede os dados para o **Repository**.
    
4. O **Repository** busca a informação no Banco de Dados através do **Model**.
    
5. A resposta faz o caminho inverso até chegar ao usuário.
    

---

## 2. Detalhamento das Camadas

### Camada de Controller (Exposição)

A Controller é a "fronteira" da sua aplicação. Sua única responsabilidade é receber dados externos e devolver uma resposta. Ela não deve saber como salvar no banco ou como calcular um imposto.

- **Analogia:** O garçom de um restaurante. Ele anota o pedido e entrega o prato, mas não cozinha.
    
- **Responsabilidades:** Mapear URLs, validar se o corpo da requisição (JSON) está correto e definir o status HTTP (200 OK, 404 Not Found, etc).
    

### Camada de Service (Negócio)

Esta é a camada mais importante do sistema. É aqui que o software "pensa". Toda a inteligência do seu projeto de Controle de Gastos deve morar aqui.

- **Analogia:** O chef de cozinha. Ele decide como preparar o prato, verifica se os ingredientes estão estragados e segue a receita.
    
- **Responsabilidades:** Validar se o valor é maior que zero, verificar se o usuário tem permissão para excluir um dado e realizar cálculos de conversão.
    

### Camada de Repository (Persistência)

O Repository é especializado em comunicação com o banco de dados. No Spring Boot, utilizamos o Spring Data JPA para que esta camada seja composta principalmente por interfaces.

- **Analogia:** O almoxarife ou estoquista. Ele sabe exatamente em qual prateleira (tabela) o produto (dado) está e como pegá-lo.
    
- **Responsabilidades:** Executar comandos SQL (Select, Insert, Update, Delete) através de métodos Java.
    

### Camada de Model/Entity (Domínio)

O Model é a representação fiel da sua tabela do banco de dados em formato de classe Java.

- **Analogia:** A ficha técnica ou a planta baixa. Define quais informações um objeto deve ter (id, valor, data, descrição).
    
- **Responsabilidades:** Mapear colunas do banco de dados para atributos da classe usando anotações JPA.
    

---

## 3. Exemplo Prático: O processo de "Salvar Gasto"

Imagine o código distribuído nestas camadas:

1. **Controller:** Recebe o JSON com os dados do gasto e chama o método `service.salvar(gasto)`.
    
2. **Service:** Verifica: `if (gasto.getValor() > 0)`. Se estiver correto, chama `repository.save(gasto)`.
    
3. **Repository:** Transforma o objeto `Gasto` em um comando SQL `INSERT INTO gastos...` e envia para o MySQL.
    
4. **Model:** Serve como o mapa para que o Hibernate saiba que o atributo `descricao` deve ir para a coluna `txt_descricao` no banco.
    

---

## 4. Por que utilizar essa divisão?

- **Substituibilidade:** Se você decidir trocar o banco de dados MySQL pelo PostgreSQL, você altera apenas a configuração e, no máximo, a camada de Repository. O restante do sistema nem percebe a mudança.
    
- **Facilidade de Testes:** Você consegue testar as regras de negócio na Service sem precisar abrir um navegador ou ligar o banco de dados.
    
- **Trabalho em Equipe:** Em projetos reais, um desenvolvedor pode focar em criar novos Endpoints na Controller enquanto outro foca nas regras complexas da Service.