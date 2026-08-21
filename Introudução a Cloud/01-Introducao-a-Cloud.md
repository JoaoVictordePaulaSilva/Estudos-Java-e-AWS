# Introducao a Computacao em Nuvem

Esta nota contem os conceitos fundamentais de computacao em nuvem, comparacoes com a infraestrutura fisica tradicional e os modelos de servico e implantacao.

## O Modelo Cliente-Servidor

A computacao moderna e baseada no modelo cliente-servidor:

- **Cliente:** Navegador web ou aplicativo que faz uma solicitacao de dados ou servicos.
- **Servidor:** Computador que recebe a solicitacao, processa-a e retorna a resposta ao cliente.
- Na AWS, esses servidores sao virtualizados e disponibilizados sob demanda.

## On-Premises versus Nuvem

- **On-Premises (Local):** Exige alto investimento inicial (CapEx) em servidores fisicos, gerenciamento de espaco, energia, refrigeracao e equipe de manutencao. Ha um risco inerente de comprar capacidade excessiva (ociosidade) ou insuficiente (perda de usuarios por sobrecarga).
- **Nuvem (Cloud):** Substitui a despesa de capital por despesa operacional (OpEx). O provedor gerencia a infraestrutura fisica, e o usuario paga apenas pelo que consome, com capacidade flexivel.

## Principais Beneficios da Nuvem

1. **Custo Variavel:** Pague apenas pelo que utilizar, sem necessidade de adivinhar a capacidade necessaria.
2. **Economia de Escala:** Custos mais baixos devido ao imenso volume de clientes atendidos pelo provedor.
3. **Elasticidade:** Capacidade de aumentar ou diminuir recursos computacionais automaticamente conforme a demanda.
4. **Velocidade e Agilidade:** Recursos podem ser provisionados em minutos em vez de semanas.
5. **Alcance Global:** Implantacao de aplicacoes em multiplas regioes geograficas do mundo com poucos cliques.

## Modelos de Servico em Nuvem

A divisao de responsabilidades tecnicas entre o cliente e o provedor de nuvem e classificada em tres modelos principais:

### IaaS (Infraestrutura como Servico)

- **Definicao:** Fornece os componentes basicos de TI, como servidores (CPU), memoria e armazenamento.
- **Perfil do Usuario:** Administradores de Sistemas (Sysadmins).
- **Responsabilidade do Usuario:** Gerencia o sistema operacional, os middlewares, o runtime das aplicacoes e os dados.
- **Exemplo AWS:** Amazon EC2.

### PaaS (Plataforma como Servico)

- **Definicao:** O provedor gerencia o hardware e o sistema operacional subjacentes. O usuario nao precisa se preocupar com atualizacoes ou patches de seguranca do servidor.
- **Perfil do Usuario:** Desenvolvedores de software.
- **Responsabilidade do Usuario:** Implantar (deploy) e gerenciar a aplicacao desenvolvida.
- **Exemplo AWS:** AWS Elastic Beanstalk.

### SaaS (Software como Servico)

- **Definicao:** Aplicacao completa e acabada executada e gerenciada inteiramente pelo provedor de nuvem.
- **Perfil do Usuario:** Clientes finais ou usuarios corporativos.
- **Responsabilidade do Usuario:** Utilizar o servico e configurar permissoes basicas.
- **Exemplo Geral:** E-mail corporativo (como Gmail ou Microsoft 365).

> [!NOTE] A decisao sobre qual modelo escolher deve se basear no nivel de controle de infraestrutura que a organizacao deseja manter em relacao a agilidade que necessita.

## Modelos de Implantacao de Nuvem

Determina onde os recursos estao estruturados e distribuidos fisicamente:

- **Cloud-based (Totalmente na Nuvem):** Toda a aplicacao e executada e hospedada na nuvem. Todos os ativos sao provisionados no provedor.
- **Hibrido:** Conecta recursos baseados na nuvem com a infraestrutura local (on-premises). Utilizado em estrategias de migracao gradual ou para manter dados legados locais devido a regulamentacoes.
- **On-Premises / Nuvem Privada:** Recursos implantados em data centers locais usando tecnologias de virtualizacao. Nao oferece os beneficios totais da escala da nuvem publica, mas mantem controle fisico absoluto sobre o hardware.

---

Retornar ao [[00-Indice-Estudos-AWS|Indice Principal]]