# Armazenamento e Bancos de Dados na AWS

Esta nota aborda as opcoes de armazenamento de dados e os principais sistemas de gerenciamento de bancos de dados relacionais e nao relacionais da AWS.

## Tipos de Armazenamento

A AWS oferece solucoes focadas em diferentes formatos de armazenamento de dados:

### Armazenamento em Bloco: Amazon EBS (Elastic Block Store)

- **Definicao:** Armazenamento em bloco de alto desempenho projetado para uso com o Amazon EC2. Funciona de maneira analoga a um disco rigido ou SSD conectado fisicamente ao servidor virtual.
- **Caracteristicas:** Persistente (os dados sobrevivem ao encerramento da instancia se configurado). Um volume EBS e associado a uma unica instancia em uma mesma Zona de Disponibilidade.

### Armazenamento de Arquivos: Amazon EFS (Elastic File System)

- **Definicao:** Sistema de arquivos elastico, sem servidor (serverless) e gerenciado, baseado no protocolo NFS (Network File System).
- **Caracteristicas:** Permite conexao simultanea de centenas de instancias EC2 em diferentes Zonas de Disponibilidade para compartilhamento de dados comum de arquivos.

### Armazenamento de Objetos: Amazon S3 (Simple Storage Service)

- **Definicao:** Servico de armazenamento de objetos projetado para armazenar e recuperar qualquer quantidade de dados com durabilidade de 99,999999999% (11 nones).

#### Conceitos Basicos do S3

- **Buckets:** Contêineres lógicos para armazenar objetos na AWS. Cada conta permite ate 100 buckets por padrao.
- **Objetos:** Arquivos que variam de 0 a 5TB em tamanho, contendo os dados e metadados.
- **Recursos:** Controle de acesso granular por objeto, versionamento de arquivos e hospedagem de sites estáticos.
- **Casos de uso principais:** Data lakes, arquivamento de logs históricos e backups.

#### Classes de Armazenamento S3

As categorias de armazenamento ajudam a otimizar custos com base na frequencia de acesso e disponibilidade:

- **S3 Standard:** Projetado para dados acessados com frequencia. Armazena dados em no minimo tres Zonas de Disponibilidade. Custo mais alto por GB armazenado.
- **S3 Standard-IA (Infrequent Access):** Para dados acessados com menos frequencia, mas que exigem acesso em milissegundos quando solicitados. Armazenado em no minimo tres Zonas de Disponibilidade. Custo por GB armazenado reduzido, porem possui tarifa de recuperacao por GB.
- **S3 One Zone-IA:** Semelhante ao Standard-IA, mas armazena dados em apenas uma Zona de Disponibilidade. Custo de armazenamento 20% menor, porem nao possui redundancia geografica contra desastres fisicos.
- **S3 Intelligent-Tiering:** Monitora padroes de acesso e move arquivos automaticamente entre classes de acesso frequente e infrequente para reduzir custos sem impacto operacional.
- **S3 Glacier Instant Retrieval:** Baixo custo para dados arquivados que precisam de recuperacao imediata (milissegundos).
- **S3 Glacier Flexible Retrieval:** Arquivo de baixo custo com tempos de recuperacao flexiveis de minutos a horas.
- **S3 Glacier Deep Archive:** Opcao de mais baixo custo da AWS para arquivamento de longo prazo. Tempo de recuperacao padrão de 12 a 48 horas.

## Bancos de Dados na AWS

A AWS possui solucoes especificas para diferentes modelos de dados:

### Relacional (SQL)

#### Amazon RDS (Relational Database Service)

- **Definicao:** Servico totalmente gerenciado para bancos de dados relacionais. Facilita a atualizacao de patches, backups automaticos e alta disponibilidade de maneira automatizada.
- **Motores suportados:** MySQL, PostgreSQL, MariaDB, Oracle, Microsoft SQL Server e Amazon Aurora.

#### Amazon Aurora

- **Definicao:** Motor de banco de dados relacional compativel com MySQL e PostgreSQL desenvolvido pela AWS para obter alto desempenho (ate 5x mais rapido que o MySQL padrao).

### Nao Relacional (NoSQL)

#### Amazon DynamoDB

- **Definicao:** Banco de dados NoSQL do tipo chave-valor totalmente gerenciado e sem servidor (serverless).
- **Caracteristicas:** Desempenho ultraveloz e consistente com latencia abaixo de 10 milissegundos em qualquer escala de acesso. Escala recursos computacionais de forma automatica e possui replicação de dados regional.

### Analise e Big Data

#### Amazon Redshift

- **Definicao:** Servico de Data Warehouse em escala de petabytes rapido e totalmente gerenciado. Projetado para analise massiva de dados e Business Intelligence (BI).

#### Amazon ElastiCache

- **Definicao:** Cache na memoria totalmente gerenciado compativel com Redis e Memcached para acelerar o tempo de resposta das aplicacoes.

---

Retornar ao [[00-Indice-Estudos-AWS|Indice Principal]]