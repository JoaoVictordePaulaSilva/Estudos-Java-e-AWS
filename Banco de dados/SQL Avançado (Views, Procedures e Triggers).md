## 1. Views (Visões)

Uma **View** é uma "tabela virtual" baseada no resultado de uma consulta `SELECT`. Ela não armazena dados próprios, mas funciona como um atalho para consultas complexas.

- **Por que usar?** Segurança (esconder colunas sensíveis) e simplicidade (abstrair JOINs gigantes).
    
- **Boas Práticas:** Use Views para relatórios que são consultados frequentemente.
    

```SQL
-- Criando uma view de produtos ativos com o nome da categoria
CREATE VIEW vw_produtos_detalhados AS
SELECT p.id, p.nome, p.preco, c.nome_categoria
FROM tb_produtos p
JOIN tb_categorias c ON p.categoria_id = c.id
WHERE p.st_ativo = TRUE;

-- Como usar: igual a uma tabela comum
SELECT * FROM vw_produtos_detalhados WHERE preco > 100;
```

---

## 2. Stored Procedures (Procedimentos Armazenados)

São blocos de código SQL que ficam guardados no banco e podem ser executados com um comando `CALL`. Elas aceitam parâmetros de entrada e saída.

- **Por que usar?** Centralizar lógica de negócio pesada e reduzir o tráfego de rede entre o Java e o Banco.
    

```SQL
DELIMITER $$

CREATE PROCEDURE sp_aplicar_desconto_categoria(IN categoria_id_param INT, IN porcentagem DECIMAL(5,2))
BEGIN
    UPDATE tb_produtos 
    SET preco = preco * (1 - (porcentagem / 100))
    WHERE categoria_id = categoria_id_param AND st_ativo = TRUE;
END $$

DELIMITER ;

-- Executando a procedure
CALL sp_aplicar_desconto_categoria(1, 10.0);
```

---

## 3. Triggers (Gatilhos)

São ações automáticas disparadas pelo banco de dados antes ou depois de um `INSERT`, `UPDATE` ou `DELETE`.

- **Caso de uso clássico (Auditoria):** Salvar quem alterou um registro e quando.
    
- **Cuidado:** Triggers escondem lógica. Use com moderação para não dificultar o debug do sistema.
    

```SQL
CREATE TRIGGER tr_log_preco_update
BEFORE UPDATE ON tb_produtos
FOR EACH ROW
BEGIN
    IF OLD.preco <> NEW.preco THEN
        INSERT INTO tb_log_precos (produto_id, preco_antigo, preco_novo, data_alteracao)
        VALUES (OLD.id, OLD.preco, NEW.preco, NOW());
    END IF;
END;
```

---

## 4. Transactions (Transações ACiD)

Essencial para garantir que uma operação complexa (ex: transferência bancária) ou ocorra por completo ou não ocorra nada.

- **ACID:** Atomicidade, Consistência, Isolamento e Durabilidade.
    


```SQL
START TRANSACTION;

UPDATE tb_contas SET saldo = saldo - 100 WHERE id = 1;
UPDATE tb_contas SET saldo = saldo + 100 WHERE id = 2;

-- Se tudo deu certo:
COMMIT;

-- Se algo falhou:
ROLLBACK;
```

---

## 5. Indexes Avançados e Explain

Para performance em bancos com milhões de registros:

- **EXPLAIN:** Use antes de um SELECT para ver como o MySQL está buscando os dados.
    
- **Índice Composto:** Quando você filtra sempre por duas colunas juntas (ex: `st_ativo` e `data_cadastro`).
    

```SQL
-- Analisando a performance da consulta
EXPLAIN SELECT * FROM tb_produtos WHERE st_ativo = TRUE AND categoria_id = 5;

-- Criando índice composto
CREATE INDEX idx_ativo_categoria ON tb_produtos(st_ativo, categoria_id);
```

---

## 6. Dicas de Produtividade no IntelliJ

- **Routine Editor:** No IntelliJ, você pode abrir Procedures e Functions em uma aba especial que destaca erros de sintaxe SQL específicos para o seu banco (MySQL/PostgreSQL).
    
- **Data Extractor:** Precisa levar dados de uma View para o Excel ou converter para JSON? Clique com o botão direito na grade de resultados > **Export Data**.
    
- **SQL Dialects:** O IntelliJ entende que o SQL do MySQL é diferente do Oracle. Configure o dialeto em `Settings > Languages & Frameworks > SQL Dialects` para ter o melhor autocomplete possível.