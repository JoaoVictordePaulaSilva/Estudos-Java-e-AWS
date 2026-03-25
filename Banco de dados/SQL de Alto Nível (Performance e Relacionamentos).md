## 1. Tipos de Relacionamentos (Lógica e Implementação)

Mapear corretamente a vida real para o banco de dados evita redundância e inconsistência.

|**Relacionamento**|**Como implementar?**|**Exemplo Prático**|
|---|---|---|
|**1:1 (Um para Um)**|A FK fica em uma das tabelas com restrição `UNIQUE`.|`Usuario` e `PerfilConfiguracao`.|
|**1:N (Um para Muitos)**|A FK fica na tabela "Muitos" apontando para a "Um".|`Categoria` (1) e `Produtos` (N).|
|**N:N (Muitos para Muitos)**|Necessita de uma **Tabela Intermediária** (Join Table) com duas FKs.|`Estudantes` e `Cursos`.|

### Dica de Integridade: `ON DELETE CASCADE` vs `SET NULL`

Ao definir uma FK, você escolhe o que acontece se o pai for deletado:

- **`CASCADE`**: Deleta os filhos automaticamente (Cuidado!).
    
- **`SET NULL`**: Mantém os filhos, mas zera a referência.
    
- **`RESTRICT`**: Impede a exclusão do pai enquanto houver filhos.
    

---

## 2. Window Functions (Funções de Janela)

Diferente do `GROUP BY`, as _Window Functions_ realizam cálculos em um conjunto de linhas, mas mantêm as linhas individuais no resultado.

- **Sintaxe:** `FUNCTION() OVER (PARTITION BY ... ORDER BY ...)`
    

```SQL
-- Ranking de produtos mais caros por categoria
SELECT 
    nome, 
    preco, 
    categoria_id,
    RANK() OVER (PARTITION BY categoria_id ORDER BY preco DESC) as ranking_no_setor
FROM tb_produtos;
```

---

## 3. Common Table Expressions (CTE - `WITH`)

As CTEs permitem criar "tabelas temporárias" nomeadas que tornam queries complexas muito mais legíveis do que subconsultas aninhadas.

```SQL
WITH media_precos AS (
    SELECT categoria_id, AVG(preco) as media FROM tb_produtos GROUP BY categoria_id
)
SELECT p.nome, p.preco, m.media
FROM tb_produtos p
JOIN media_precos m ON p.categoria_id = m.categoria_id
WHERE p.preco > m.media; -- Apenas produtos acima da média da categoria
```

---

## 4. Índices Avançados e Full-Text Search

Quando o `LIKE '%termo%'` fica lento em textos grandes, usamos o **Full-Text Index**.

- **Índice Único (`UNIQUE`)**: Garante que não existam valores duplicados (ex: CPF).
    
- **Full-Text**: Permite buscas por relevância linguística.
    

```SQL
-- Criando índice para busca textual
ALTER TABLE tb_produtos ADD FULLTEXT(nome, descricao);

-- Buscando de forma performática
SELECT * FROM tb_produtos 
WHERE MATCH(nome, descricao) AGAINST('teclado mecanico rgb' IN NATURAL LANGUAGE MODE);
```

---

## 5. Transações e Níveis de Isolamento

Em sistemas de alta concorrência, o MySQL permite configurar o quão "isolada" uma transação é das outras:

1. **READ UNCOMMITTED**: Pode ler dados "sujos" (não commitados).
    
2. **READ COMMITTED**: Só lê o que foi confirmado.
    
3. **REPEATABLE READ**: (Padrão do MySQL) Garante que a mesma leitura dentro da transação retorne sempre o mesmo valor.
    
4. **SERIALIZABLE**: Travamento total (mais seguro, porém mais lento).
    

---

## 6. Dicas de Produtividade no IntelliJ

- **Refactor SQL**: Se você renomear uma coluna na tabela através da aba **Database**, o IntelliJ pode escanear seu código Java e sugerir a alteração nas queries `@Query` do Spring Data JPA.
    
- **Explain Plan Visual**: Ao rodar uma query pesada, use o botão **Explain Plan**. O IntelliJ gera um fluxograma mostrando onde o banco está perdendo tempo (ex: "Full Table Scan" em vez de usar índice).
    
- **SQL Injection Check**: O IntelliJ destaca em roxo/amarelo se você estiver concatenando Strings em queries SQL, o que é um risco de segurança, sugerindo o uso de `PreparedStatement`.