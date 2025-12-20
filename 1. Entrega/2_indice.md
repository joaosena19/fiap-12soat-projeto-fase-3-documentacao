# Índice

Este arquivo serve como referência para cada um dos pontos de avaliação do Tech Challenge. Cada termo está linkado para o respectivo arquivo de documentação.

Se for sua primeira leitura, siga a navegação "Próximo" ao final de cada arquivo.

## Pontos de Avaliação

1. Estrutura dos repositórios
    1. Repositórios com links:
        - [fiap-12soat-projeto-fase-3-terraform](https://github.com/joaosena19/fiap-12soat-projeto-fase-3-terraform)
        - [fiap-12soat-projeto-fase-3-banco](https://github.com/joaosena19/fiap-12soat-projeto-fase-3-banco)
        - [fiap-12soat-projeto-fase-3-lambda](https://github.com/joaosena19/fiap-12soat-projeto-fase-3-lambda)
        - [fiap-12soat-projeto-fase-3-aplicacao](https://github.com/joaosena19/fiap-12soat-projeto-fase-3-aplicacao)
        - [fiap-12soat-projeto-fase-3-documentacao](https://github.com/joaosena19/fiap-12soat-projeto-fase-3-documentacao)
    2. Veja [ADR 0006 - Separação em Múltiplos Repositórios](../4.%20ADRs/0006_adr_separacao_dos_repositorios.md)
    3. Veja [ADR 0012 - Localização da Infraestrutura do API Gateway](../4.%20ADRs/0012_adr_gateway_e_lambda_no_mesmo_repositorio.md)
2. Proteções de branch e CI/CD - Veja [ADR 0014 - Proteção de Branches](../4.%20ADRs/0014_adr_protecao_das_branchs.md)
3. API Gateway
    1. [Configuração do API Gateway](https://github.com/joaosena19/fiap-12soat-projeto-fase-3-lambda/tree/main/terraform) no repositório Lambda
    2. [Diagrama de componentes evidenciando API Gateway](../2.%20Diagramas%20de%20Componentes%20(C4)/1_diagrama_de_componentes_c4.md)
4. Serverless Functions
    1. [Repositório do Lambda](https://github.com/joaosena19/fiap-12soat-projeto-fase-3-lambda)
    2. [Código das funções serverless](https://github.com/joaosena19/fiap-12soat-projeto-fase-3-lambda/tree/main/src)
    3. Veja [ADR 0011 - Autenticação com AWS Lambda](../4.%20ADRs/0011_adr_autenticacao_com_lambda.md)
5. Banco de Dados gerenciado
    1. Veja [ADR 0008 - PostgreSQL no Amazon RDS](../4.%20ADRs/0008_adr_banco_de_dados_rds_postgres.md)
    2. [Repositório do banco de dados](https://github.com/joaosena19/fiap-12soat-projeto-fase-3-banco)
6. Kubernetes
    1. Veja [ADR 0009 - Kubernetes e HPA](../4.%20ADRs/0009_adr_kubernetes_e_hpa.md)
    2. [Repositório da aplicação, pasta k8s/](https://github.com/joaosena19/fiap-12soat-projeto-fase-3-aplicacao/tree/main/k8s)
    3. [Arquivo oficina-mecanica-hpa.yaml](https://github.com/joaosena19/fiap-12soat-projeto-fase-3-aplicacao/blob/main/k8s/api/oficina-mecanica-hpa.yaml)
7. Terraform
    1. [Repositório da infraestrutura base](https://github.com/joaosena19/fiap-12soat-projeto-fase-3-terraform)
    2. [Repositório do Lambda](https://github.com/joaosena19/fiap-12soat-projeto-fase-3-lambda)
    3. [Repositório do banco de dados](https://github.com/joaosena19/fiap-12soat-projeto-fase-3-banco)
    4. Veja [ADR 0007 - Terraform como Infrastructure as Code](../4.%20ADRs/0007_adr_terraform_como_iac.md)
    5. Veja [ADR 0012 - Localização da Infraestrutura do API Gateway](../4.%20ADRs/0012_adr_gateway_e_lambda_no_mesmo_repositorio.md)
8. Monitoramento e Observabilidade
    1. Veja [ADR 0015 - Monitoramento com New Relic](../4.%20ADRs/0015_adr_monitoramento_com_new_relic.md)
    2. Veja [ADR 0016 - Nível de Log para Erros de Negócio (4xx)](../4.%20ADRs/0016_adr_erros_tratados_como_log_information.md)
    3. Veja componentes do dashboard em [Plano de monitoramento](../6.%20Plano%20de%20monitoramento/1_plano_de_monitoramento.md#dashboard)
    4. Veja alerta em [Plano de monitoramento](../6.%20Plano%20de%20monitoramento/1_plano_de_monitoramento.md#alertas)
9. [Logs estruturados](../6.%20Plano%20de%20monitoramento/1_plano_de_monitoramento.md#log-estruturado-na-aplicação)
10. [Diagrama de Componentes](../2.%20Diagramas%20de%20Componentes%20(C4)/1_diagrama_de_componentes_c4.md)
11. Diagramas de Sequência
    1. [Fluxo de autenticação](../3.%20Diagramas%20de%20Sequência/1_auth.md)
    2. [Fluxo de criação de ordem de serviço](../3.%20Diagramas%20de%20Sequência/2_criacao_os.md)
12. [RFCs e ADRs](../4.%20ADRs/0001_adr_csharp_como_linguagem.md) - ADRs seguem o modelo de Michael Nygard, com adição de uma seção para discussões, atuando também como RFCs
13. Justificativa para escolha do banco de dados 
    1. Veja [ADR 0008 - PostgreSQL no Amazon RDS](../4.%20ADRs/0008_adr_banco_de_dados_rds_postgres.md)
    2. [Justificativa para escolha do PostgreSQL](../5.%20Banco%20de%20dados%20e%20modelo%20ER/1_banco_de_dados_modelo_er.md#escolha-do-banco-de-dados)
14. [Modelo ER e relacionamentos do banco de dados](../5.%20Banco%20de%20dados%20e%20modelo%20ER/1_banco_de_dados_modelo_er.md)
15. [Documentação da API](../8.%20Endpoints/1_endpoints.md)