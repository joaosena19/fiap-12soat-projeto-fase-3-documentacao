# Estratégia de Segurança Zero Trust

## Status

Aceito

## Contexto

O sistema expõe endpoints na internet e roda dentro de um cluster Kubernetes. Era necessário decidir se a segurança seria focada apenas no perímetro (confiando no tráfego após passar pelo Gateway) ou se adotaríamos uma postura onde cada componente deve validar as requisições individualmente.

## Discussão e possibilidades

Temos dois pontos onde é possível validar o token JWT da requisição: AWS Gateway e Aplicação Backend. Não foi considerado validar em apenas uma delas, pois Zero Trust é padrão de segurança de mercado, assim, cada camada deve ter sua própria validação independente.

## Decisão

Foi decidido aplicar a arquitetura Zero Trust com dupla validação de token no Gateway e no Backend.

## Consequências

**Positivas:**

* **Redundância de segurança** Caso haja uma falha na configuração de rotas do Gateway ou uma brecha de segurança no perímetro, a aplicação final permanece protegida e recusa conexões não autenticadas.
* **Economia de recursos no cluster** O tráfego inválido é barrado na borda (Gateway/Lambda), impedindo que requisições ilegítimas consumam CPU e memória dos pods da aplicação principal.

**Negativas:**

* **Aumento da complexidade operacional** A solução exigiu o desenvolvimento e manutenção de uma função Lambda Authorizer adicional especificamente para realizar essa interceptação no Gateway.
* **Latência adicional** Cada requisição passa por dois processos de validação de token antes de ser processada pela regra de negócio.