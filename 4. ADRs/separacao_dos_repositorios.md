# Separação em Múltiplos Repositórios

## Status

Aceito

## Contexto

O projeto é composto por diversas camadas distintas: Infraestrutura Base, Banco de Dados, Autenticação Serverless e a API Principal. Era preciso definir como organizar o código fonte dessas partes.

O enunciado do Tech Challenge trouxe um requisito explícito de que a entrega deveria ser feita em repositórios separados para demonstrar a capacidade de orquestrar pipelines independentes.

## Discussão e possibilidades

Não houve avaliação de alternativas, pois a separação era uma regra obrigatória para a avaliação do projeto. A solução foi dividida em 4 repositórios conforme o Tech Challenge:

1. **Infraestrutura:** VPC e Cluster EKS.
2. **Banco:** RDS PostgreSQL.
3. **Lambda:** Autenticação e API Gateway.
4. **Aplicação:** API da Oficina (.NET).

Além deles, foi criado um quinto repositório exclusivo para a documentação (este repositório), para centralizar todas as informações.

## Decisão

Foi decidido manter a estrutura de múltiplos repositórios com um repositório adicional para documentação.

## Consequências

**Positivas:**

* **Separação de Responsabilidades:** Cada repositório tem um foco claro e específico.
* **Pipelines Independentes:** Cada repositório tem seu próprio CI/CD. É possível fazer deploy da infraestrutura sem disparar desnecessariamente o build da aplicação, e vice-versa.

**Negativas:**

* **Complexidade de Integração:** Compartilhar informações entre os repositórios tornou-se mais difícil. Foi necessário usar `terraform_remote_state` e scripts auxiliares nos pipelines para buscar outputs de um repositório para usar no outro (como a aplicação precisando saber o endereço do banco que está em outro repo).