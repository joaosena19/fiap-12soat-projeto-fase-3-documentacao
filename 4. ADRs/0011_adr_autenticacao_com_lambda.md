# Autenticação com AWS Lambda

## Status

Aceito

## Contexto

É preciso definir como será feito o login e a proteção das rotas da API. Além disso, o Tech Challenge possui um requisito obrigatório de utilizar funções serverless em alguma parte da arquitetura.

## Discussão e possibilidades

Poderia ter implementado a autenticação dentro da aplicação principal, mas isso não atenderia o requisito de serverless do Tech Challenge.

O Amazon Cognito foi considerado, mas foi descartado pois preciso de uma lógica customizada de autenticação que acessa o banco de dados para validar o status atual do usuário. Implementar essa lógica manualmente via código oferece mais controle do que tentar adaptar o Cognito.

A solução encontrada foi usar o AWS Lambda em dois momentos:

1. **Login:** Uma função que recebe o documento e senha, consulta o banco e retorna o token JWT.
2. **Authorizer:** Uma função atrelada ao API Gateway que intercepta as requisições e valida o token.

## Decisão

Foi decidido mover toda a camada de autenticação (Login e Validação de Token) para AWS Lambda.

## Consequências

**Positivas:**

* Atende o requisito obrigatório de serverless do Tech Challenge.
* Retira a carga de processamento de autenticação da API principal.
* Escala automaticamente conforme a demanda de acessos.

**Negativas:**

* Maior complexidade de infraestrutura.
* É necessário manter um pipeline de deploy separado apenas para as Lambdas.
* Exige uma configuração de monitoramento específica no New Relic, diferente da aplicação principal.