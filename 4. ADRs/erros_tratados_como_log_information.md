# Nível de Log para Erros de Negócio (4xx)

## Status

Aceito

## Contexto

O sistema lança exceções de domínio (`DomainException`) quando regras de negócio são violadas ou quando recursos não são encontrados. Esses eventos resultam em status codes 4xx para o cliente. Era preciso decidir como registrar esses eventos na ferramenta de monitoramento, pois eles contém informações relevantes sobre o uso do sistema.

## Discussão e possibilidades

A primeira opção seria simplesmente não logar, tratando como um fluxo normal de resposta HTTP. O problema é que eu perderia a visão de métricas importantes, como tentativas de cadastro duplicado ou erros de validação frequentes que podem indicar problemas de UX.

Outra opção seria logar como Warning ou Error. Rejeitei essa ideia porque erro de usuário não é erro de sistema. Se eu logar como erro, vou sujar meus dashboards de disponibilidade e posso disparar alertas falsos por causa de usuário errando senha ou input inválido. Warning também não parecia correto, pois o sistema se comportou exatamente como esperado ao rejeitar o dado.

## Decisão

Foi decidido logar exceções tratadas e erros de client-side (4xx) com o nível Information.

## Consequências

**Positivas:**

* Rastreabilidade limpa. Consigo separar facilmente nos dashboards o que é bug real (Error 500) do que é rejeição de negócio (Info 400).
* Permite gerar insights de produto através dos logs (ex: qual o erro de validação mais comum?) sem gerar ruído nos logs.

**Negativas:**

* Pode aumentar o volume de logs disparados se tivermos muitos usuários errando validações, consumindo a cota de ingestão do New Relic mais rápido.