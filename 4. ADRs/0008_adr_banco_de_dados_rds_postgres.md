# ADR 0008 - PostgreSQL no Amazon RDS

## Status

Aceito

## Contexto

Como a infraestrutura do projeto está hospedada na AWS, a escolha concentrou-se nos serviços gerenciados disponíveis nesse ecossistema.

Era preciso escolher um banco de dados. O domínio do sistema é relacional, então um banco SQL é a escolha natural.

Além disso, o Tech Challenge estabelece como requisito obrigatório a utilização de um serviço de banco de dados gerenciado, o que inviabiliza a adoção de um banco executando em container ou máquina virtual gerenciada manualmente.

## Discussão e possibilidades

Avaliei o SQL Server, que seria o natural para .NET, mas rejeitei porque é pago. O AWS Aurora também foi cogitado, mas descartei porque ele não está no free tier.

A escolha ficou com o PostgreSQL por ser relacional, robusto e totalmente gratuito. Para a hospedagem, optei pelo Amazon RDS para atender o requisito de serviço gerenciado mas que ainda está dentro do Free Tier da AWS.

## Decisão

Foi decidido utilizar o **Amazon RDS com PostgreSQL**.

## Consequências

**Positivas:**

* Banco gratuito.
* Atende o requisito de usar serviço gerenciado.

**Negativas:**

* Nenhum ponto negativo identificado até o momento.

---
Anterior: [ADR 0007 - Terraform como Infrastructure as Code](0007_adr_terraform_como_iac.md)  
Próximo: [ADR 0009 - Kubernetes e HPA](0009_adr_kubernetes_e_hpa.md)