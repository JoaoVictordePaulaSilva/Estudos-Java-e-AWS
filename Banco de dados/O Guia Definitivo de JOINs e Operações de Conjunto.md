## 1. Tipos de JOIN (A Teoria dos Conjuntos)

O JOIN serve para combinar linhas de duas ou mais tabelas baseando-se em uma coluna comum entre elas (Geralmente `PK` e `FK`).

|**Tipo de JOIN**|**Descrição**|**Resultado**|
|---|---|---|
|**INNER JOIN**|O mais comum.|Retorna apenas registros que possuem correspondência em **ambas** as tabelas.|
|**LEFT JOIN**|Focado na tabela da esquerda.|Retorna todos da tabela A, e os correspondentes da B. Se não houver em B, traz `NULL`.|
|**RIGHT JOIN**|Focado na tabela da direita.|Retorna todos da tabela B, e os da A se existirem. (Menos usado que o Left).|
|**FULL JOIN**|União total.|Retorna todos os registros de ambas, preenchendo com `NULL` onde não há par.|

### Exemplo Prático (Produtos e Categorias):


```SQL
-- Queremos todos os produtos e o nome de sua categoria
SELECT p.nome, c.descricao 
FROM tb_produtos p
INNER JOIN tb_categorias c ON p.categoria_id = c.id;

-- Queremos TODOS os clientes, mesmo aqueles que nunca fizeram um pedido
SELECT c.nome, p.id_pedido
FROM tb_clientes c
LEFT JOIN tb_pedidos p ON c.id = p.cliente_id;
```

---

## 2. O que ficou faltando: Operadores de Conjunto (Set Operators)

Enquanto o JOIN junta colunas (lado a lado), os operadores de conjunto juntam **linhas** (uma em cima da outra).

- **UNION / UNION ALL:** Combina o resultado de dois `SELECT`. O `UNION` remove duplicados, o `UNION ALL` mantém tudo (é mais rápido).
    
- **INTERSECT:** Retorna apenas as linhas que aparecem em ambos os `SELECT`.
    
- **EXCEPT (ou MINUS):** Retorna as linhas do primeiro `SELECT` que **não** estão no segundo.
    

---

## 3. Subqueries vs. Joins

Muitos iniciantes usam subqueries (um SELECT dentro de outro), mas o JOIN costuma ser muito mais performático porque o otimizador do MySQL consegue ler os índices melhor.

- **Subquery (Lento):** `SELECT nome FROM tb_produtos WHERE categoria_id IN (SELECT id FROM tb_categorias WHERE st_ativo = 1);`
    
- **JOIN (Rápido):** `SELECT p.nome FROM tb_produtos p JOIN tb_categorias c ON p.categoria_id = c.id WHERE c.st_ativo = 1;`
    

---

## 4. Agregações Avançadas: `HAVING`

Você já conhece o `GROUP BY`, mas e se precisar filtrar o resultado de uma contagem? O `WHERE` não funciona para funções de agregação (como `COUNT`, `SUM`). Usamos o **HAVING**.

```SQL
-- Buscar categorias que possuem mais de 5 produtos cadastrados
SELECT categoria_id, COUNT(*) as total
FROM tb_produtos
GROUP BY categoria_id
HAVING total > 5;
```

---

## 5. Dicas de "Mestre" para a Integração Java

No **Java 21** com Spring Data JPA:

- **Fetch Join:** Quando você faz um JOIN no JPA, use a palavra-chave `FETCH` (`JOIN FETCH p.categoria`) para carregar os dados em uma única consulta ao banco. Isso evita que o Hibernate faça 100 consultas extras para buscar 100 categorias (Problema N+1).
    
- **Projeções:** Se você só precisa do _Nome do Produto_ e _Nome da Categoria_, não traga a entidade inteira. Use um **Record** no Java para receber apenas essas duas colunas.
    

---

## 6. Dicas de Produtividade no IntelliJ

- **Visual Join:** Ao escrever um JOIN, o IntelliJ sugere automaticamente a cláusula `ON` baseada nas chaves estrangeiras que ele detectou no seu banco de dados. Basta apertar `Enter`.
    
- **Injeção de Parâmetros:** Se você testar uma query no console do IntelliJ que tenha parâmetros (`:id` ou `?`), ele abrirá uma janelinha para você digitar os valores e testar a query sem precisar "hardcodar" números no SQL.