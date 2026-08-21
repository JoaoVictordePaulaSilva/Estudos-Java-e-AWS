# Redes e Conectividade na AWS

Esta nota aborda a estruturacao de redes logicas privadas na AWS e os componentes de seguranca e conexao externa.

## Amazon VPC (Virtual Private Cloud)

A Amazon VPC permite que voce crie uma rede virtual isolada e logicamente dedicada para a sua conta AWS. "Tudo comeca dentro de uma VPC", sendo a base para o provisionamento e seguranca de outros servicos (como instancias EC2 e bancos de dados).

### Sub-redes (Subnets)

Uma VPC e segmentada em sub-redes para melhor organizacao e controle de transito de dados:

- **Sub-rede Publica:** Contem recursos que precisam se comunicar diretamente com a internet publica (como servidores de apresentacao web).
- **Sub-rede Privada:** Destinada a recursos que nao devem ter acesso direto a internet ou que contem dados confidenciais (como bancos de dados e servidores de aplicacao backend).

## Elementos de Conectividade

A AWS fornece diferentes mecanismos de conexao de rede para a sua VPC:

### Internet Gateway (Gateway da Internet)

- **Definicao:** Componente de rede altamente disponivel anexado a VPC que estabelece a conexao fisica entre a rede privada e a internet publica. Permite transito de dados bidirecional para as sub-redes publicas.

### Gateway Privado Virtual (Virtual Private Gateway)

- **Definicao:** Ponto de entrada de rede privada na VPC que gerencia conexoes de rede criptografadas diretas, isolando o tráfego da internet comum.

### Conexao VPN

- **Definicao:** Estabelece uma conexao criptografada (IPsec VPN) entre o data center corporativo local e a VPC através da internet publica utilizando um Gateway Privado Virtual.

### AWS Direct Connect

- **Definicao:** Conexao fisica direta e dedicada que liga a rede corporativa do cliente a uma localizacao fisica do AWS Direct Connect, contornando totalmente a internet publica.
- **Vantagem:** Reducao drastica de custos de largura de banda, aumento de throughput e latencias consistentes.

## Seguranca de Rede: Firewalls Logicos

A AWS disponibiliza duas camadas de seguranca para filtrar o trafego de rede de entrada e saida:

### Security Groups (Grupos de Seguranca)

- **Atuacao:** No nivel da instancia (como instancia EC2). Atua como um firewall de host.
- **Tipo de Controle:** Com estado (stateful). Se o trafego de entrada for permitido, o trafego de retorno correspondente sera permitido automaticamente, sem necessidade de regras adicionais de saida.
- **Regras:** Permite apenas regras de permissao (allow rules). Por padrao, bloqueia todo o trafego ate que uma regra o permita.

### Network ACLs (NACL)

- **Atuacao:** No nivel da sub-rede. Atua como um firewall de rede de fronteira.
- **Tipo de Controle:** Sem estado (stateless). Requer explicitamente regras separadas para permitir o trafego de entrada e de saida.
- **Regras:** Suporta regras de permissao (allow) e regras de negacao explicita (deny rules). Processado em ordem numerica sequencial.

---

Retornar ao [[00-Indice-Estudos-AWS|Indice Principal]]