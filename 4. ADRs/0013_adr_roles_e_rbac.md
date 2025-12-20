# ADR 0013 - Controle de Acesso Baseado em Roles (RBAC)

## Status

Aceito

## Contexto

Nas fases anteriores, a autenticação era simples (Client Credentials), pois o sistema foi pensado apenas para uso interno por funcionários em um computador compartilhado.

O Tech Challenge 3 trouxe o requisito de autenticação baseada no CPF do cliente via Serverless. Isso obrigou o sistema a evoluir para suportar o conceito de "Usuário" e permitir que o cliente final acesse seus próprios dados remotamente, além dos funcionários da oficina.

## Discussão e possibilidades

Com a entrada do cliente no sistema, não era mais possível manter o acesso irrestrito a todos os recursos. Foi preciso diferenciar quem é funcionário de quem é apenas dono de um veículo.

A solução adotada foi o RBAC (Role-Based Access Control) combinado com verificação de propriedade (Ownership). Foram definidos perfis distintos:

* **Administrador:** Acesso total ao sistema (funcionários).
* **Cliente:** Acesso restrito apenas aos seus próprios dados.

Apenas verificar a role não era suficiente. Se um usuário tem a role de cliente, ele pode ver suas ordens de serviço, mas não pode ver *qualquer* ordem de serviço. Por isso foi implementada a lógica de ownership, onde o sistema valida se o recurso solicitado pertence ao ID do cliente logado.

## Decisão

Foi decidido implementar RBAC com validação de ownership através da classe `Ator`.

A classe `Ator` representa o usuário logado e é injetada em todos os casos de uso. Ela contém os IDs (usuário e cliente) e as roles. Os casos de uso utilizam métodos de extensão dessa classe para validar se a ação é permitida antes de executá-la.

Mais detalhes no [documento sobre autorização](../7.%20Autorização/1_autorizacao.md)

## Consequências

**Positivas:**

* Segurança granular. O código garante que um cliente nunca visualize dados de outro cliente.
* Atende o requisito do Tech Challenge de login por CPF.
* Classe `Ator` centraliza a lógica de autorização e permite um código fluente para validar as permissões.

**Negativas:**

* Aumentou a complexidade do código. Todo Use Case agora exige a injeção do `Ator` e uma etapa de validação.