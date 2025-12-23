# ADR 0009 - Kubernetes e HPA

## Status

Aceito

## Contexto

Para garantir alta disponibilidade e escalabilidade da API, era necessário usar uma solução de orquestração de containers. O Tech Challenge exige explicitamente o uso de Kubernetes.

Além de subir o cluster, também era preciso garantir que a aplicação suportasse picos de acesso. Para isso, foi configurado o Horizontal Pod Autoscaler (HPA), permitindo que a aplicação escale automaticamente conforme a carga aumenta.

## Discussão e possibilidades

Como a infraestrutura está na AWS, a escolha pelo EKS foi natural.

O HPA foi configurado da seguinte forma:

* **Mínimo de réplicas:** 1  
* **Máximo de réplicas:** 5  
* **Trigger:** Escala quando o uso de CPU ultrapassa 70%

Antes de definir esses valores, foi feito um cálculo simples de capacidade para garantir que o cluster aguentaria a escala máxima sem problemas:

* Cada pod possui `limits` de **500m de CPU** (0.5 vCPU) e **512Mi de memória**.
* No pior cenário, com 5 pods, o consumo total seria de **2.5 vCPU** e aproximadamente **2.5 GB de RAM**.
* O cluster utiliza instâncias `t3.small` (2 vCPUs, 2 GB de RAM), com um Node Group configurado para no mínimo 2 e no máximo 3 nós.

Mesmo com o HPA no limite, a aplicação consome apenas parte da capacidade disponível. Com dois nós ativos, o cluster já oferece 4 vCPUs, o que garante margem suficiente para escalar sem gargalos.

## Decisão

Foi decidido utilizar **EKS** para a orquestração dos containers e **HPA** para a escalabilidade horizontal da API.

## Consequências

**Positivas:**

* Escalabilidade automática, ajustando o número de réplicas conforme a demanda.
* Melhor resiliência a picos de acesso sem intervenção manual.

**Negativas:**

* Maior complexidade operacional.
* Custo adicional do control plane do EKS, mas é necessário.

---
Anterior: [ADR 0008 - PostgreSQL no Amazon RDS](0008_adr_banco_de_dados_rds_postgres.md)  
Próximo: [ADR 0010 - Estratégia de Segurança Zero Trust](0010_adr_estrategia_seguranca_zero_trust.md)