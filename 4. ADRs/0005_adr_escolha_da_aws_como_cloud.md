# ADR 0005 - AWS como Cloud Provider

## Status

Aceito

## Contexto

O Tech Challenge exige que a solução seja implantada em uma cloud. É preciso escolher qual vendor será utilizado para hospedar o cluster Kubernetes, Banco de Dados e Funções Serverless.

## Discussão e possibilidades

Foram avaliados os principais players do mercado: AWS, Azure e Google Cloud (GCP).

Tecnicamente, todos os três são excelentes e atenderiam aos requisitos de arquitetura. No entanto, para o critério de desempate, a AWS saiu na frente pois tem um Free Tier mais generoso, é a plataforma mais utilizada no mercado atualmente, e é a cloud adotada pela FIAP na maioria das aulas.

## Decisão

Foi decidido utilizar a Amazon Web Services (AWS) como provedor de nuvem.

## Consequências

**Positivas:**

* Alinhamento com as aulas da FIAP  .
* Economia de custos devido ao Free Tier.
* Facilidade em encontrar documentação e suporte comunitário.

**Negativas:**

* Nenhum ponto negativo identificado para o contexto deste projeto.

---
Anterior: [ADR 0004 - Clean Architecture](0004_adr_clean_architecture.md)  
Próximo: [ADR 0006 - Separação em Múltiplos Repositórios](0006_adr_separacao_dos_repositorios.md)