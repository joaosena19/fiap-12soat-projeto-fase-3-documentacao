# ADR 0017 - Imutabilidade Histórica de Itens e Serviços na Ordem de Serviço

## Status

Aceito

## Contexto

Uma ordem de serviço é um documento financeiro que representa um acordo realizado em um momento específico no tempo. O sistema possui cadastros gerais de serviços e itens de estoque, nos quais são definidos preços e descrições, mas esses valores podem mudar. Tornou-se necessário garantir que uma alteração de preço no catálogo atual não altere o valor de uma ordem de serviço fechada em um período anterior.

## Discussão e possibilidades

Uma abordagem puramente relacional seria criar um relacionamento direto (chave estrangeira) entre a linha da ordem de serviço e a tabela de catálogo de produtos. Isso economizaria espaço em disco, mas criaria um acoplamento perigoso. Caso o gerente alterasse o nome ou o preço de um serviço no cadastro principal, todas as ordens de serviço antigas que referenciam aquele ID seriam visualmente alteradas, comprometendo o histórico financeiro da oficina.

Poderia ser implementado um sistema de versionamento nas tabelas de catálogo, no qual cada alteração de preço criaria uma nova versão do produto. No entanto, essa abordagem adicionaria uma complexidade de gestão desnecessária para o escopo do projeto.

A solução adotada foi tratar a Ordem de Serviço e os Cadastros como domínios distintos. O cadastro representa o estado atual, enquanto a ordem de serviço representa um snapshot imutável do passado.

## Decisão

Foi decidido aplicar o padrão de desnormalização para garantir imutabilidade temporal.

Ao adicionar um item ou serviço em uma ordem, o sistema não cria apenas um vínculo com o ID original. Ele copia os dados para novas tabelas chamadas `itens_incluidos` e `servicos_incluidos`.

## Consequências

**Positivas:**

* Garante integridade histórica e financeira. O preço cobrado na época e descrição permanecem inalterados independente das atualizações futuras no catálogo.
* Desacoplamento de domínios. A Ordem de Serviço não quebra se um item de estoque for excluído do catálogo principal.

**Negativas:**

* Duplicação de dados no banco, já que repetimos as strings de nome e descrição para cada ordem de serviço gerada.

---
Anterior: [ADR 0016 - Nível de Log para Erros de Negócio (4xx)](0016_adr_erros_tratados_como_log_information.md)  
Próximo: [Estratégia de Deploy: Gatilho Manual (Workflow Dispatch)](0018_adr_deploy_via_workflow_dispatch.md)