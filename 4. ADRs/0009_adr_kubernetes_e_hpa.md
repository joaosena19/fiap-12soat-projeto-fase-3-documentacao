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

* Cada pod possui `limits` de **250m de CPU** (0.25 vCPU) e **256Mi de memória**.
* No pior cenário, com 5 pods, o consumo total seria de **1.25 vCPU** e aproximadamente **1.3 GB de RAM**.
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