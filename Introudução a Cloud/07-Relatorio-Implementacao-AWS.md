# Relatorio de Implementacao de Servicos AWS

**Data:** 21 de Agosto de 2026  
**Empresa:** BioPharma S.A.  
**Responsavel:** João Victor de Paula Silva

---

### RELATORIO DE IMPLEMENTACAO DE SERVICOS AWS

#### Introdução

Este relatorio apresenta o processo de implementacao de ferramentas na empresa **BioPharma S.A.**, realizado pela **Consultoria de Solucoes Cloud AWS**. O objetivo do projeto foi elencar 3 servicos AWS com a finalidade de realizar diminuicao de custos imediatos, otimizar processos operacionais de pesquisa e desenvolvimento (P&D) e garantir a conformidade regulatoria de longo prazo.

#### Descricao do Projeto

O projeto de implementacao de ferramentas foi dividido em 3 etapas, cada uma com seus objetivos especificos. A seguir, sao descritas as etapas do projeto:

##### Etapa 1:

- **Nome da ferramenta:** Amazon S3 (Simple Storage Service) com S3 Lifecycle Policies e S3 Glacier Deep Archive
- **Foco da ferramenta:** Armazenamento seguro de objetos com alta durabilidade (99.999999999%) e otimizacao automatica de custos de armazenamento.
- **Descricao de caso de uso:** Armazenar dados brutos de sequenciamento genetico, registros historicos de ensaios clinicos e relatorios de conformidade regulatoria exigidos pela ANVISA e FDA. Os dados ativos de pesquisas sao armazenados na classe Standard. Usando regras de ciclo de vida do S3, apos 30 dias de inatividade os arquivos sao movidos para o S3 Standard-IA (Infrequent Access) ou S3 Intelligent-Tiering. Apos 1 ano, sao arquivados automaticamente no S3 Glacier Deep Archive para retencao regulatoria obrigatoria de longo prazo (com custo ate 90% menor e tempo de recuperacao de ate 12 horas), reduzindo drasticamente as despesas com storages locais fisicos on-premises.

##### Etapa 2:

- **Nome da ferramenta:** Amazon RDS (Relational Database Service) com implantacao Multi-AZ
- **Foco da ferramenta:** Banco de dados relacional gerenciado com alta disponibilidade, backups automaticos e seguranca integrada.
- **Descricao de caso de uso:** Gerenciamento estruturado de formulas quimicas de medicamentos, controle de lotes de fabricacao, registros de pacientes de testes clinicos e dados de controle de qualidade da linha de producao. A implantacao em Multi-AZ garante a alta disponibilidade necessaria para manter o banco ativo mesmo em falhas de datacenter, enquanto o backup automatizado e a criptografia nativa com AWS KMS garantem a protecao de segredo industrial e propriedade intelectual sem exigir servidores dedicados on-premises, eliminando custos de capital (CapEx).

##### Etapa 3:

- **Nome da ferramenta:** AWS Lambda
- **Foco da ferramenta:** Computacao serverless orientada a eventos com cobranca estrita por milissegundo de execucao de codigo.
- **Descricao de caso de uso:** Automacao de processamento e validacao de dados de sensores IoT de geladeiras de armazenamento frio de vacinas e medicamentos biologicos. O codigo Lambda e disparado imediatamente apos o recebimento de dados do sensor no Amazon S3, analisando leituras termicas e enviando alertas caso ocorra desvios de temperatura. Por ser serverless, o Lambda nao exige servidores ligados 24/7, gerando custo zero em momentos de ociosidade operacional e eliminando despesas desnecessarias de infraestrutura de computacao continua.

---

#### Conclusao

A implementacao de ferramentas na empresa **BioPharma S.A.** tem como esperado a reducao drastica de despesas de capital (CapEx) para despesas operacionais (OpEx) flexiveis, a eliminacao de custos com servidores fisicos ociosos locais e a garantia de alta disponibilidade e conformidade regulatorias para arquivos de auditoria de longa duracao, o que aumentara a eficiencia e a produtividade da empresa. Recomenda-se a continuidade da utilizacao das ferramentas implementadas e a busca por novas tecnologias que possam melhorar ainda mais os processos da empresa.

#### Anexos

1. **Manual de Politicas de Ciclo de Vida do S3:** Guia de transicao automatica de dados para arquivos regulatórios e classes Glacier.
2. **Guia de Seguranca de Banco de Dados:** Documentacao de integracao do Amazon RDS Multi-AZ com criptografia de chaves no AWS KMS.
3. **Diagrama de Arquitetura Serverless IoT:** Estrutura de disparo de alertas de temperatura de vacinas com AWS Lambda.

