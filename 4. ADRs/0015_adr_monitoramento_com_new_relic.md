# ADR 0015 - Monitoramento com New Relic

## Status

Aceito

## Contexto

É necessário de uma solução de observabilidade para monitorar a aplicação e a infraestrutura. O Tech Challenge trouxe um requisito a escolha entre New Relic ou Datadog.

## Discussão e possibilidades

O fator decisivo foi o plano gratuito. O New Relic oferece 100GB de ingestão de dados por mês na faixa gratuita, e a maior parte dos recursos da plataforma, o que é mais que suficiente para atender a necessidade do projeto.

O Datadog já é bem mais limitado nos recursos gratuitos, e o free trial acaba após 14 dias.

A configuração das duas ferramentas é similar, então o Datadog não apresentou nenhuma vantagem técnica de facilidade de uso que justificasse a escolha.

Além disso, o recurso de logs in context do New Relic também pesou a favor, pois permite correlacionar automaticamente os logs da aplicação com os traces de performance, facilitando muito o debug.

## Decisão

Foi decidido utilizar o New Relic.

## Consequências

**Positivas:**

* Plano gratuito generoso.
* Recurso de logs in context nativo e fácil de usar.

**Negativas:**

* É necessário aprender NRQL para criar dashboards personalizados. É uma linguagem proprietária, mas como a sintaxe é simples e a documentação é boa, isso não chega a ser um problema real no dia a dia.

---
Anterior: [ADR 0014 - Proteção de Branches](0014_adr_protecao_das_branchs.md)  
Próximo: [ADR 0016 - Nível de Log para Erros de Negócio (4xx)](0016_adr_erros_tratados_como_log_information.md)