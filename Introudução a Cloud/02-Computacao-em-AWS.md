# Computacao na AWS

Esta nota detalha os principais servicos de computacao da AWS, focando no Amazon EC2, conceitos de elasticidade e as ferramentas de conteineres e serverless.

## Amazon EC2 (Elastic Compute Cloud)

O Amazon EC2 fornece capacidade computacional segura e redimensionavel na nuvem por meio de maquinas virtuais conhecidas como instancias.

### Modelos de Cobranca de Instancias

A AWS oferece diferentes formas de adquirir e pagar por instancias EC2, adequando-se ao perfil financeiro e previsibilidade da aplicacao:

#### Sob Demanda (On-Demand)

- **Caracteristicas:** Ideal para cenarios sem padrao reconhecido de utilizacao dos recursos. Nao exige compromissos de longo prazo ou pagamentos antecipados.
- **Custo:** Maior valor por hora, porem totalmente flexivel. A capacidade pode ser aumentada ou reduzida a qualquer momento.

#### Instancias Reservadas (Reserved Instances)

- **Caracteristicas:** Ideal para cargas de trabalho previsiveis e de longo prazo.
- **Custo:** Oferece descontos significativos em relacao a tarifa sob demanda em troca de um compromisso de utilizacao de 1 a 3 anos.

#### Savings Plans

- **Caracteristicas:** Ideal para cargas previsiveis de longo prazo, mas com maior flexibilidade entre familias de instancias e regioes.
- **Custo:** Precos baixos em troca de um compromisso consistente de uso medido em USD/hora por um periodo de 1 a 3 anos. O uso excedente ao contratado e cobrado na tarifa sob demanda convencional.

#### Instancias Spot (Spot Instances)

- **Caracteristicas:** Utiliza a capacidade computacional excedente e ociosa da AWS. Pode sofrer interrupcoes caso a AWS precise da capacidade de volta (com aviso previo de 2 minutos). Ideal para processamento em lote, analises de dados e testes.
- **Custo:** Ate 90% mais barato em relacao ao modelo sob demanda.

#### Hosts Dedicados (Dedicated Hosts)

- **Caracteristicas:** Servidor fisico dedicado exclusivamente ao uso do cliente. Ajuda a cumprir requisitos estritos de conformidade regulatoria e politicas de licenciamento de software especificas (como licencas por socket fisico).

## Escalabilidade e Elasticidade de Rede

Para garantir que a aplicacao atenda a variacoes de trafego sem interrupcoes e de forma eficiente em termos de custo, utilizam-se dois servicos combinados:

### AWS Auto Scaling

- **Funcao:** Monitora a carga das aplicacoes e ajusta automaticamente a quantidade de instancias EC2 ativa.
- **Mecanismo:** Adiciona instancias durante picos de demanda (escala horizontal para cima) e remove instancias quando a demanda cai (escala horizontal para baixo) para economizar recursos.

### Elastic Load Balancing (ELB)

- **Funcao:** Distribui de forma automatica o trafego de entrada entre multiplos destinos, como instancias EC2, conteineres e enderecos IP.
- **Beneficio:** Evita que uma unica instancia fique sobrecarregada, alem de garantir alta disponibilidade ao desviar trafego de instancias com falha (health checks).

## Servicos de Conteineres na AWS

Os conteineres fornecem uma forma consistente de empacotar aplicacoes com suas respectivas dependencias e executa-las isoladamente.

- **Amazon ECR (Elastic Container Registry):** Registro gerenciado de imagens Docker. Permite armazenar, compactar, criptografar e controlar o acesso as imagens que serao executadas.
- **Amazon ECS (Elastic Container Service):** Servico de orquestracao de conteineres nativo da AWS, altamente escalavel e projetado para rodar aplicacoes Dockerizadas.
- **Amazon EKS (Elastic Kubernetes Service):** Servico gerenciado que facilita a execucao do Kubernetes na AWS sem a necessidade de instalar e operar o painel de controle (control plane) de Kubernetes proprio.
- **AWS Fargate:** Mecanismo de computacao sem servidor (serverless) para conteineres. Funciona tanto com o ECS quanto com o EKS, eliminando a necessidade de gerenciar, provisionar ou corrigir servidores fisicos subjacentes. O usuario define os limites de CPU e memoria e o Fargate gerencia a infraestrutura.

## Computacao Sem Servidor (Serverless)

### AWS Lambda

- **Definicao:** Servico que executa codigo em resposta a eventos (como uploads no S3, alteracoes em tabelas de banco de dados ou requisicoes HTTP).
- **Funcionamento:** Totalmente gerenciado. O usuario fornece apenas o codigo e a AWS cuida do provisionamento, escalabilidade e alta disponibilidade.
- **Cobranca:** Cobrado por tempo de execucao do codigo em milissegundos e quantidade de solicitacoes. Nao ha cobranca quando o codigo nao esta sendo executado.

---

Retornar ao [[00-Indice-Estudos-AWS|Indice Principal]]