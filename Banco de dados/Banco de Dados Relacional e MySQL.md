## 1. Conceitos Fundamentais

Um banco **Relacional** organiza dados em tabelas que se conectam através de chaves.

- **Chave Primária (PK):** O identificador único da linha (ex: `id`).
    
- **Chave Estrangeira (FK):** Um campo que aponta para a PK de outra tabela, criando o relacionamento.
    

---

## 2. Boas Práticas: O Padrão `st_ativo` (Soft Delete)

Em sistemas profissionais, raramente apagamos um dado do disco (comando `DELETE`). Usamos o **Soft Delete**:

- Em vez de excluir, alteramos um campo booleano (ex: `st_ativo`, `is_active` ou `deleted_at`).
    
- **Vantagens:** Auditoria, recuperação rápida de dados e integridade referencial (evita erros ao deletar algo que outras tabelas usam).
    

---

## 3. CRUD Completo no MySQL (Exemplo Prático)

Vamos criar uma tabela de `produtos` seguindo padrões de mercado:

### CREATE (Criação da Tabela)

```SQL
CREATE TABLE tb_produtos (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    preco DECIMAL(10, 2) NOT NULL,
    data_cadastro DATETIME DEFAULT CURRENT_TIMESTAMP,
    st_ativo BOOLEAN DEFAULT TRUE -- Boas práticas: Ativo por padrão
);
```

### INSERT (Inserção)


```SQL
INSERT INTO tb_produtos (nome, preco) VALUES ('Teclado Mecânico', 350.00);
INSERT INTO tb_produtos (nome, preco) VALUES ('Mouse Gamer', 150.00);
```

### SELECT (Leitura com Filtro de Ativos)

```SQL
-- Buscar apenas produtos que não foram "excluídos"
SELECT * FROM tb_produtos WHERE st_ativo = TRUE;

-- Ordenação e Limite (Paginação)
SELECT nome, preco FROM tb_produtos 
WHERE st_ativo = TRUE 
ORDER BY preco DESC 
LIMIT 10;
```

### UPDATE (Atualização e Soft Delete)

```SQL
-- Atualização comum
UPDATE tb_produtos SET preco = 320.00 WHERE id = 1;

-- Simulação de DELETE (Soft Delete)
UPDATE tb_produtos SET st_ativo = FALSE WHERE id = 2;
```

---

## 4. Operações Importantes do Cotidiano

### Joins (Unindo Tabelas)

O dia a dia do desenvolvedor é unir dados de tabelas diferentes.

- **INNER JOIN:** Retorna apenas quando há correspondência em ambas as tabelas.
    
- **LEFT JOIN:** Retorna todos da esquerda, mesmo que não haja par na direita.
    

```SQL
SELECT p.nome, c.nome_categoria 
FROM tb_produtos p
INNER JOIN tb_categorias c ON p.categoria_id = c.id
WHERE p.st_ativo = TRUE;
```

### Agregações (Relatórios)

```SQL
SELECT COUNT(*) AS total_produtos, SUM(preco) AS valor_estoque 
FROM tb_produtos 
WHERE st_ativo = TRUE;
```

---

## 5. Dicas de Performance e Segurança

1. **Índices (`INDEX`):** Crie índices em colunas usadas frequentemente no `WHERE` (como o `st_ativo` ou `email`). Isso acelera a busca drasticamente.
    
2. **Transactions:** Ao fazer várias alterações que dependem uma da outra, use `START TRANSACTION` e `COMMIT`. Se algo der errado, use `ROLLBACK`.
    
3. **Nunca use `SELECT *` em produção:** Peça apenas as colunas que você vai usar. Isso economiza memória e rede.
    

---

## 6. Dicas de Produtividade no IntelliJ

- **Database Inspector:** Use a aba **Database** (lado direito). Você pode arrastar tabelas, editar dados diretamente na grade (como Excel) e o IntelliJ gera o SQL para você.
    
- **Console de Consulta:** O IntelliJ oferece **Autocomplete** para suas tabelas e colunas enquanto você digita SQL. Ele até valida se você escreveu o nome da tabela errado!
    
- **Visualização de Diagramas:** Clique com o botão direito na sua conexão de banco > **Diagrams > Show Visualization**. O IntelliJ desenha todo o seu DER (Diagrama Entidade Relacionamento) automaticamente.