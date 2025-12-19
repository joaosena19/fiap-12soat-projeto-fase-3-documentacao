# Plano de monitoramento

## New Relic

O New Relic foi escolhido como plataforma de monitoramento pois é um serviço completo e robusto, que integra facilmente com Kubernetes e AWS, e que tem um plano gratuito generoso que atende completamente o projeto.

Mais detalhes em ADR [todo: linkar adr do new relic]

## Dashboard

Este é o dashboard de monitoramento da aplicação no New Relic:

[todo: print do dashboard completo quando estiver pronto]

### Widgets

Estes são os widgets que compõem o dashboard:

#### Healthcheck & Uptime

Monitora a disponibilidade da API através de duas queries, avaliando a taxa de sucesso das requisições e o status do *Readiness Probe* do Kubernetes, indicando se a aplicação está conseguindo atender às requisições.

[todo: print do widget quando estiver pronto]

**Query 1:**
```sql
SELECT percentage(count(*), WHERE httpResponseCode NOT LIKE '5%') as 'Disponibilidade' 
FROM Transaction 
WHERE appName = 'Fiap.Fase3.Oficina.API' 
SINCE 1 hour ago 
TIMESERIES
```

**Query 2:**
```sql
SELECT min(ready) * 100 as 'K8s Readiness Probe' 
FROM K8sContainerSample 
WHERE containerName = 'container-oficina-mecanica-api' 
SINCE 1 hour ago 
TIMESERIES
```

#### Recursos K8s

Acompanha o consumo percentual de CPU e Memória do container em relação aos limites (limits) definidos no Kubernetes.

[todo: print do widget quando estiver pronto]

**Query:**
```sql
SELECT 
  (max(cpuUsedCores) / max(cpuLimitCores)) * 100 as 'CPU %',
  (max(memoryWorkingSetBytes) / max(memoryLimitBytes)) * 100 as 'Memória %'
FROM K8sContainerSample 
WHERE containerName = 'container-oficina-mecanica-api' 
SINCE 1 hour ago 
TIMESERIES
```

#### Latência das APIs

Exibe o tempo médio de resposta das transações.

[todo: print do widget quando estiver pronto]

**Query:**
```sql
SELECT average(duration) * 1000 as 'Latência (ms)' 
FROM Transaction 
WHERE appName = 'Fiap.Fase3.Oficina.API' 
TIMESERIES
```

#### Log de Erros Recentes

Lista os últimos 50 erros e falhas críticos registrados nos logs da aplicação, útil para monitorar erros imediatos.

[todo: print do widget quando estiver pronto]

**Query:**
```sql
SELECT timestamp, message, UseCase, ErrorType 
FROM Log 
WHERE level = 'ERROR' OR level = 'FATAL' 
SINCE 1 day ago 
LIMIT 50
```

#### Top Erros 4xx

Este widget mostra os erros 4xx mais frequentes na aplicação. São erros tratados causados por requisições inválidas dos clientes. É útil para descobrirmos aonde os clientes estão errando e melhorar a usabilidade do sistema.

[todo: print do widget quando estiver pronto]

**Query:**
```sql
SELECT count(*) as 'Ocorrências'
FROM Log
WHERE level = 'INFO'
AND traceId IN (
  SELECT traceId FROM Transaction WHERE httpResponseCode LIKE '4%'
)
FACET message_template
SINCE 1 week ago
LIMIT 10
```

#### Volume diário de ordens de serviço

Contabiliza novas ordens de serviço criadas diariamente, comparando com a semana anterior para medir a tendência de demanda do negócio.

É criado na aplicação através do Custom Event `OrdemServicoCriada`.

[todo: print do widget quando estiver pronto]

**Query:**
```sql
SELECT count(*) as 'Qtd Ordens' 
FROM OrdemServicoCriada 
SINCE 1 week ago 
TIMESERIES 1 day 
COMPARE WITH 1 week ago
```

#### Tempo médio de execução de ordens de serviço por status

Calcula o tempo médio que uma OS permanece em certos status antes de avançar. Status analisados: 'Em Diagnóstico', 'Em Execução', 'Finalizada'.

É criado na aplicação através do Custom Event `OrdemServicoMudancaStatus`.

[todo: print do widget quando estiver pronto]

**Query:**
```sql
SELECT average(DuracaoMs) / 1000 / 60 / 60 as 'Horas' 
FROM OrdemServicoMudancaStatus 
FACET StatusAnterior 
SINCE 1 week ago
```