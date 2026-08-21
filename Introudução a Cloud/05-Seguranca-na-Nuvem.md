# Seguranca e Conformidade na AWS

Esta nota abrange as responsabilidades mutuas de seguranca entre a AWS e o cliente, controle de acessos corporativo e gerenciamento de chaves.

## O Modelo de Responsabilidade Compartilhada

A seguranca na AWS e estabelecida de maneira colaborativa:

- **Seguranca DA Nuvem (Responsabilidade da AWS):** A AWS protege a infraestrutura global fisica que executa todos os servicos oferecidos. Isso inclui a seguranca fisica de regioes, Zonas de Disponibilidade, seguranca do hardware de computacao, roteadores de rede e camadas de virtualizacao.
- **Seguranca NA Nuvem (Responsabilidade do Cliente):** O cliente gerencia e configura a seguranca das aplicacoes e dados implantados. Isso inclui a seguranca de dados dos clientes, criptografia, configuracoes de rede (como Security Groups e NACLs) e gerenciamento de usuarios e acessos pelo IAM.

## IAM (Identity and Access Management)

O IAM permite controlar o acesso de forma segura aos servicos e recursos da AWS. Os conceitos fundamentais sao:

- **Usuario Raiz (Root User):** Criado no momento de abertura da conta. Possui controle total e absoluto sobre todas as configuracoes e custos. Deve ser usado apenas nas primeiras etapas ou tarefas especificas que o exijam, aplicando autenticacao de multiplos fatores (MFA) obrigatoriamente.
- **Usuarios IAM:** Identidades criadas dentro da conta para pessoas especificas realizarem tarefas cotidianas.
- **Grupos IAM:** Colecoes de usuarios IAM. Permite associar permissoes comuns a multiplos usuarios simultaneamente.
- **Funcoes IAM (Roles):** Identidades atribuidas temporariamente a usuarios ou servicos da AWS (como permitir que uma instancia EC2 grave dados em um bucket S3 de forma segura, sem expor credenciais fisicas de login).
- **Politicas IAM (Policies):** Documentos JSON que definem explicitamente quais acoes sao permitidas ou negadas em determinados recursos. Aplica o Principio do Menor Privilegio (conceder apenas as permissoes necessarias para a tarefa ser concluida).

## AWS Organizations

O AWS Organizations e um servico gratuito de governanca que permite gerenciar centralizadamente multiplas contas AWS a medida que a organizacao cresce.

### Desafios de Administracao com Multiplas Contas

- Dificuldade em gerenciar custos isolados.
- Atingir limites de servico (soft e hard limits) impostos por conta.
- Manter a consistencia de seguranca entre ambientes de desenvolvimento e producao.

### Solucoes Oferecidas

- **Faturamento Consolidado:** Agrupa o custo de todas as contas membro em uma unica fatura global, permitindo o compartilhamento de descontos por volume (como taxas reduzidas de uso de S3 ou EC2 pelo somatorio de consumo).
- **Agrupamento Hierarquico:** Permite estruturar as contas em Unidades Organizacionais (OUs) hierarquicas refletindo departamentos de negocio ou ciclo de vida de software (ex: Dev, Teste, Prod).
- **Service Control Policies (SCPs):** Politicas de controle centralizadas usadas para definir as permissoes maximas que as contas membro pertencentes as OUs podem exercer, impedindo acoes criticas de seguranca mesmo para administradores locais de contas membro.

## Criptografia e Gerenciamento de Chaves

A criptografia protege as informacoes sensiveis contra acesso nao autorizado por meio de algoritmos codificados, hashes e assinaturas digitais.

### Dados em Repouso (Data at Rest)

- Refere-se aos dados armazenados fisicamente.
- **Exemplos:** Dados persistidos em volumes EBS ou objetos em buckets S3.

### Dados em Transito (Data in Transit)

- Refere-se aos dados trafegando ativamente na rede de uma origem para um destino.
- **Protecao:** Criptografados atraves de protocolos HTTPS, TLS/SSL ou conexoes de rede privadas seguras.

### AWS Key Management Service (KMS)

- Servico gerenciado que facilita a criacao, rotatividade e controle de chaves de criptografia usadas para proteger dados em repouso nos servicos AWS de forma automatica.

## AWS Artifact

O AWS Artifact e o portal gratuito de autoatendimento que fornece acesso sob demanda a relatorios de conformidade e auditoria de seguranca da AWS (como ISO, PCI DSS, SOC 1, 2 e 3) para demonstrar a conformidade da infraestrutura AWS aos auditores do cliente.

---

Retornar ao [[00-Indice-Estudos-AWS|Indice Principal]]