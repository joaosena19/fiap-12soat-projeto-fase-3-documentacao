# Arquitetura Monolítica para Aplicação Principal

## Status

Aceito

## Contexto

É preciso definir a arquitetura da aplicação principal do sistema de ordens de serviço. A escolha da arquitetura impacta diretamente na manutenção, escalabilidade e desempenho do sistema.

## Discussão e possibilidades

A princípio foi considerado um arquitetura monolítica, pois é a mais simples de se implementar e nos permite focar nos outros requisitos de entrega.

O sistema é pequeno e simples, então não há nenhuma desvantagem de ser um monolito neste momento.

Outras alternativas seriam completamente serverless ou microsserviços, mas ambos seriam muito mais custosos, mais difíceis de testar e de dar manutenção, sendo que as vantagens que oferecem não fazem sentido neste momento do projeto.

Contudo, como é requisito do Tech Challenge o uso de funções serveless, o fluxo de autenticação usa AWS Lambda. Mais detalhes em [ADR 0011 - Autenticação com Lambda](0011_adr_autenticacao_com_lambda.md).

## Decisão

Foi decido que a aplicação principal será monolítica, com fluxo de autenticação em AWS Lambda.

## Consequências

**Positivas:**

- Deploy simples (apenas 1 container).
- Zero latência entre módulos.
- Facilidade para testar e debuggar fluxos completos.

Negativas:

- Falha crítica derruba todo o sistema (Single Point of Failure).
- Escala vertical ou horizontal de toda a aplicação, sem granularidade por módulo (por exemplo, se o fluxo da ordem de serviço for mais usado que o de cadastros, ele não tem como escalar de forma independente).