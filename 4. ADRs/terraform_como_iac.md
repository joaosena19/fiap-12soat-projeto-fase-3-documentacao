# Terraform como Infrastructure as Code

## Status

Aceito

## Contexto

Criar e gerenciar a infraestrutura manualmente clicando no console da AWS é inviável. É um processo lento, sujeito a falhas humanas e impossível de versionar. Precisamos de uma ferramenta que automatize esse processo e garanta que o ambiente seja reprodutível.

## Discussão e possibilidades

A escolha ficou entre usar o CloudFormation da própria AWS ou o Terraform.

Optei pelo Terraform primeiramente para manter a continuidade do Tech Challenge 2. Mas o fator decisivo foi a capacidade dele de trabalhar com múltiplos providers.

Como estamos usando New Relic para monitoramento, o Terraform me permitiu codificar tanto a infraestrutura da AWS quanto a o Helm do New Relic. Se usasse CloudFormation, ficaria limitado apenas aos recursos da AWS. Além disso, por ser agnóstico à um cloud provider, facilita caso um dia seja necessário mudar de cloud.

## Decisão

Foi decidido utilizar Terraform para todo o provisionamento de infraestrutura.

## Consequências

**Positivas:**

* Permite configurar AWS e New Relic no mesmo projeto usando providers diferentes.
* Facilita a destruição e recriação do ambiente inteiro com poucos comandos.
* Não ficamos presos a uma tecnologia proprietária da Amazon.

**Negativas:**

* Gestão do `tfstate`. Diferente do CloudFormation, o Terraform exige que a gente cuide do arquivo tfstate e configure um bucket S3 para armazená-lo com segurança e evitar conflitos.