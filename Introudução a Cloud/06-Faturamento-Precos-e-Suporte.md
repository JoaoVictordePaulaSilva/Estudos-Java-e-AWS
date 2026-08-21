# Faturamento, Monitoramento e Suporte

Esta nota detalha as ferramentas de faturamento e analise de custos, as ferramentas de monitoramento em tempo real, os planos de suporte disponiveis e os frameworks estruturais recomendados pela AWS.

## Gerenciamento de Custos e Faturamento

### Painel de Faturamento (Billing Dashboard)

- Permite visualizar faturas mensais detalhadas, monitorar limites do nível gratuito e gerenciar Savings Plans adquiridos.

### AWS Budgets

- Permite planejar e definir orcamentos de custo e uso personalizados.
- **Mecanismo:** Envia alertas em tempo real por e-mail ou canais de notificacao se os limites de custo ou uso de recursos forem ultrapassados (ou estiverem projetados para exceder o valor limite).

### AWS Cost Explorer

- Interface grafica usada para detalhar, visualizar e prever custos da AWS historicos de ate 12 meses. Permite filtrar gastos por tags de aplicacoes, servicos e regioes.

## Monitoramento, Auditoria e Recomendacoes

A AWS fornece tres servicos complementares essenciais para analise de conformidade, operacional e custos:

### Amazon CloudWatch

- **Atuacao:** Monitoramento de desempenho operacional em tempo real de infraestruturas e aplicacoes.
- **Funcionalidades:** Coleta métricas de desempenho (uso de CPU do EC2, latencias), centraliza arquivos de log em tempo real e permite configurar alarmes para acionar acoes de mitigacao automatizadas.

### AWS CloudTrail

- **Atuacao:** Auditoria operacional e governanca de seguranca de atividades na conta AWS.
- **Funcionalidades:** Registra e guarda transacoes e chamadas de API feitas na console web, CLI ou SDK (quem, o que, quando e como a solicitacao foi feita). Os logs de transacao sao gravados de forma segura em buckets S3. Possui o CloudTrail Insights para detectar atividades de chamadas de API incomuns.

### AWS Trusted Advisor

- **Atuacao:** Otimizacao e boas praticas de arquitetura.
- **Funcionalidades:** Analisa de forma continua o ambiente AWS e fornece recomendacoes estruturadas em 5 categorias principais:
    1. Otimizacao de custos.
    2. Seguranca.
    3. Desempenho.
    4. Tolerancia a falhas.
    5. Limites de servicos.

## Planos de Suporte AWS

Os clientes possuem acesso a diferentes niveis de planos de suporte tecnico e consultoria operacional baseados em suas necessidades de negocios:

- **Basic:** Gratuito e incluido por padrao em todas as contas. Oferece atendimento ao cliente 24/7 para problemas de faturamento, documentacao tecnica, whitepapers e acesso limitado a verificacoes de seguranca e limites do Trusted Advisor.
- **Developer:** Recomendado para ambientes de teste e avaliacao inicial de servicos. Fornece suporte tecnico via e-mail em horario comercial por meio de um contato autorizado da conta.
- **Business:** Recomendado para ambientes de producao empresarial. Oferece suporte por chat e telefone 24/7 com engenheiros de suporte, menor tempo de resposta de resposta para casos criticos e acesso completo a todas as recomendacoes do Trusted Advisor.
- **Enterprise On-Ramp:** Oferece suporte empresarial básico, suporte tecnico 24/7 de alta prioridade e acesso a um grupo de Gerentes de Contas Tecnicas (TAM) compartilhado para orientacao arquitetural.
- **Enterprise:** Recomendado para empresas com aplicacoes de missao critica operando na nuvem. Oferece tempos de resposta ultravelozes (abaixo de 15 minutos para incidentes de severidade critica), concierge de faturamento e um Gerente de Contas Tecnicas (TAM) dedicado para coordenar o suporte operacional e arquitetural continuo.

## Frameworks de Adocao e Arquitetura

### AWS Well-Architected Framework

Conjunto de principios de projeto e praticas recomendadas estruturadas em 6 pilares de conhecimento para criar arquiteturas seguras, resilientes, de alto desempenho e economicas:

1. **Excelencia Operacional:** Executar e monitorar sistemas, entregando melhorias continuas de processos.
2. **Seguranca:** Proteger ativos, dados e sistemas de informacoes, alem de gerenciar riscos de acesso.
3. **Confiabilidade:** Garantir que cargas de trabalho executem de forma pretendida e se recuperem de falhas de hardware ou rede automaticamente.
4. **Eficiencia de Performance:** Utilizar recursos de computacao de forma estruturada para atender requisitos de mudancas de mercado.
5. **Sustentabilidade:** Minimizar o impacto ambiental da infraestrutura por meio do consumo energetico otimizado.
6. **Otimizacao de Custos:** Evitar despesas desnecessarias e gerenciar custos do ambiente de maneira eficiente.

### AWS CAF (Cloud Adoption Framework)

Auxilia organizacoes a estruturar e acelerar a migracao bem-sucedida para a nuvem por meio de perspectivas focadas em negocios, pessoas, governanca, plataforma, seguranca e operacoes.

## Migracao de Dados Fisica: Familia AWS Snow

Especialmente util quando a organizacao enfrenta restricoes graves de largura de banda e tempo de rede para migrar volumes macicos de dados para a AWS (copiar 1 PB de dados a 1 Gbps levaria cerca de 100 dias ininterruptos).

- **Dispositivos disponiveis (Snowcone e Snowball):** Dispositivos robustos de armazenamento fisico e computacao de borda enviados pela AWS para o local corporativo. O cliente copia os dados diretamente via rede local e envia o dispositivo de volta por transportadora fisica segura para carregamento direto em buckets S3 na infraestrutura AWS.

---

Retornar ao [[00-Indice-Estudos-AWS|Indice Principal]]