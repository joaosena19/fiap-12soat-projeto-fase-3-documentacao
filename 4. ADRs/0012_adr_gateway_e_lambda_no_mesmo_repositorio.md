# ADR 0012 - Localização da Infraestrutura do API Gateway

## Status

Aceito

## Contexto

Idealmente, toda a infraestrutura deveria estar centralizada no repositório de Infraestrutura (`fiap-12soat-projeto-fase-3-terraform`). No entanto, existe uma cadeia de dependência que inviabiliza colocar o API Gateway junto com a Infraestrutura Base.

1. **Infra Base (Repo Terraform):** Cria VPC, Subnets e Security Groups. Precisa existir primeiro.
2. **Código Lambda (Repo Lambda):** Precisa da Infra Base para rodar (VPC ID, Subnet IDs).
3. **API Gateway:** Precisa do Lambda para existir (precisa do ARN da função para criar a rota e permissões).

## Discussão e possibilidades

Tentar centralizar o API Gateway no repositório de infraestrutura gerou uma dependência circular:

* Se o API Gateway tentar subir junto com a Infra Base: Falha, pois o Lambda (que vive no repositório `fiap-12soat-projeto-fase-3-lambda`) ainda não existe e não tem ARN.
* Se o Lambda tentar subir antes da Infra Base: Falha, pois não tem a infraestrutura criada.

A única forma de resolver linearmente é:

1. Rodar pipeline de Infra Base.
2. Rodar pipeline do Lambda, que lê a Infra Base, cria a função e, na sequência, cria o API Gateway.

## Decisão

Foi decidido manter a definição do API Gateway no repositório do Lambda (`fiap-12soat-projeto-fase-3-lambda`).

Dessa forma, o repositório do Lambda consome os dados da Infra Base, provisiona a função e, no mesmo passo, provisiona o API Gateway.

## Consequências

**Positivas:**

* **Resolução de Dependência Circular:** resolvido.

**Negativas:**

* **Fragmentação da Infraestrutura:** O API Gateway, fica definido fora do repositório central de infraestrutura.