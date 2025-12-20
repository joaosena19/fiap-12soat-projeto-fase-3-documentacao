
# Oficina Mecânica API
API para gerenciamento de oficina mecânica

## Version: v1

**Contact information:**  
João Dainese  
joaosenadainese@gmail.com  

### /api/cadastros/clientes

#### GET
##### Summary:

Buscar todos os clientes

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Lista de clientes retornada com sucesso |
| 403 | Acesso negado |
| 500 | Erro interno do servidor |

#### POST
##### Summary:

Criar um novo cliente

##### Responses

| Code | Description |
| ---- | ----------- |
| 201 | Cliente criado com sucesso |
| 400 | Dados inválidos fornecidos |
| 403 | Acesso negado - Usuário só pode criar cliente com o mesmo documento |
| 409 | Conflito - Cliente já existe |
| 500 | Erro interno do servidor |

### /api/cadastros/clientes/{id}

#### GET
##### Summary:

Buscar cliente por ID

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | ID do cliente | Yes | string (uuid) |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Cliente encontrado com sucesso |
| 403 | Acesso negado |
| 404 | Cliente não encontrado |
| 500 | Erro interno do servidor |

#### PUT
##### Summary:

Atualizar um cliente existente

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | ID do cliente a ser atualizado | Yes | string (uuid) |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Cliente atualizado com sucesso |
| 400 | Dados inválidos fornecidos |
| 403 | Acesso negado |
| 404 | Cliente não encontrado |
| 500 | Erro interno do servidor |

### /api/cadastros/clientes/documento/{documento}

#### GET
##### Summary:

Buscar cliente por documento (CPF ou CNPJ)

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| documento | path | CPF ou CNPJ, com ou sem formatação | Yes | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Cliente encontrado com sucesso |
| 403 | Acesso negado |
| 404 | Cliente não encontrado |
| 500 | Erro interno do servidor |

### /api/estoque/itens

#### GET
##### Summary:

Buscar todos os itens de estoque

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Lista de itens de estoque retornada com sucesso |
| 500 | Erro interno do servidor |

#### POST
##### Summary:

Criar um novo item de estoque

##### Responses

| Code | Description |
| ---- | ----------- |
| 201 | Item de estoque criado com sucesso |
| 400 | Dados inválidos fornecidos |
| 500 | Erro interno do servidor |

### /api/estoque/itens/{id}

#### GET
##### Summary:

Buscar item de estoque por ID

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | ID do item de estoque | Yes | string (uuid) |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Item de estoque encontrado com sucesso |
| 404 | Item de estoque não encontrado |
| 500 | Erro interno do servidor |

#### PUT
##### Summary:

Atualizar um item de estoque existente

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | ID do item de estoque a ser atualizado | Yes | string (uuid) |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Item de estoque atualizado com sucesso |
| 400 | Dados inválidos fornecidos |
| 404 | Item de estoque não encontrado |
| 500 | Erro interno do servidor |

### /api/estoque/itens/{id}/quantidade

#### PATCH
##### Summary:

Atualizar apenas a quantidade de um item de estoque

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | ID do item de estoque | Yes | string (uuid) |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Quantidade atualizada com sucesso |
| 400 | Dados inválidos fornecidos |
| 404 | Item de estoque não encontrado |
| 500 | Erro interno do servidor |

### /api/estoque/itens/{id}/disponibilidade

#### GET
##### Summary:

Verificar disponibilidade de um item de estoque

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | ID do item de estoque | Yes | string (uuid) |
| quantidadeRequisitada | query | Quantidade necessária para verificação | No | integer |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Verificação realizada com sucesso |
| 400 | Dados inválidos fornecidos |
| 404 | Item de estoque não encontrado |
| 500 | Erro interno do servidor |

### /api/ordens-servico

#### GET
##### Summary:

Buscar todas as ordens de serviço

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Lista de ordens de serviço retornada com sucesso |
| 403 | Acesso negado. Apenas administradores podem listar ordens de serviço |
| 500 | Erro interno do servidor |

#### POST
##### Summary:

Criar uma nova ordem de serviço

##### Responses

| Code | Description |
| ---- | ----------- |
| 201 | Ordem de serviço criada com sucesso |
| 400 | Dados inválidos fornecidos |
| 403 | Acesso negado - apenas administradores podem criar ordens de serviço |
| 422 | Veículo não encontrado |
| 500 | Erro interno do servidor |

### /api/ordens-servico/{id}

#### GET
##### Summary:

Buscar ordem de serviço por ID

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | ID da ordem de serviço | Yes | string (uuid) |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Ordem de serviço encontrada com sucesso |
| 403 | Acesso negado. Apenas administradores ou donos da ordem de serviço podem visualizá-la |
| 404 | Ordem de serviço não encontrada |
| 500 | Erro interno do servidor |

### /api/ordens-servico/codigo/{codigo}

#### GET
##### Summary:

Buscar ordem de serviço por código

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| codigo | path | Código da ordem de serviço | Yes | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Ordem de serviço encontrada com sucesso |
| 403 | Acesso negado. Apenas administradores ou donos da ordem de serviço podem visualizá-la |
| 404 | Ordem de serviço não encontrada |
| 500 | Erro interno do servidor |

### /api/ordens-servico/completa

#### POST
##### Summary:

Criar uma nova ordem de serviço completa com cliente, veículo, serviços e itens

##### Responses

| Code | Description |
| ---- | ----------- |
| 201 | Ordem de serviço criada com sucesso |
| 400 | Dados inválidos fornecidos |
| 403 | Acesso negado - apenas administradores podem criar ordens de serviço |
| 422 | Erro de validação ou regra de negócio |
| 500 | Erro interno do servidor |

### /api/ordens-servico/{id}/servicos

#### POST
##### Summary:

Adicionar serviços à ordem de serviço

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | ID da ordem de serviço | Yes | string (uuid) |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Serviços adicionados com sucesso |
| 400 | Dados inválidos fornecidos |
| 404 | Ordem de serviço não encontrada |
| 422 | Serviço não encontrado |
| 500 | Erro interno do servidor |

### /api/ordens-servico/{id}/itens

#### POST
##### Summary:

Adicionar item à ordem de serviço

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | ID da ordem de serviço | Yes | string (uuid) |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Item adicionado com sucesso |
| 400 | Dados inválidos fornecidos |
| 404 | Ordem de serviço não encontrada |
| 422 | Item de estoque não encontrado |
| 500 | Erro interno do servidor |

### /api/ordens-servico/{id}/servicos/{servicoIncluidoId}

#### DELETE
##### Summary:

Remover serviço da ordem de serviço

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | ID da ordem de serviço | Yes | string (uuid) |
| servicoIncluidoId | path | ID do serviço incluído a ser removido | Yes | string (uuid) |

##### Responses

| Code | Description |
| ---- | ----------- |
| 204 | Serviço removido com sucesso |
| 403 | Acesso negado |
| 404 | Ordem de serviço ou serviço não encontrado |
| 422 | Erros de regra do domínio |
| 500 | Erro interno do servidor |

### /api/ordens-servico/{id}/itens/{itemIncluidoId}

#### DELETE
##### Summary:

Remover item da ordem de serviço

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | ID da ordem de serviço | Yes | string (uuid) |
| itemIncluidoId | path | ID do item incluído a ser removido | Yes | string (uuid) |

##### Responses

| Code | Description |
| ---- | ----------- |
| 204 | Item removido com sucesso |
| 403 | Acesso negado |
| 404 | Ordem de serviço ou item não encontrado |
| 422 | Erro de regra do domínio |
| 500 | Erro interno do servidor |

### /api/ordens-servico/{id}/cancelar

#### POST
##### Summary:

Cancelar ordem de serviço

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | ID da ordem de serviço | Yes | string (uuid) |

##### Responses

| Code | Description |
| ---- | ----------- |
| 204 | Ordem de serviço cancelada com sucesso |
| 400 | Dados inválidos fornecidos |
| 403 | Acesso negado. Apenas administradores podem cancelar ordens de serviço |
| 404 | Ordem de serviço não encontrada |
| 500 | Erro interno do servidor |

### /api/ordens-servico/{id}/iniciar-diagnostico

#### POST
##### Summary:

Iniciar diagnóstico da ordem de serviço

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | ID da ordem de serviço | Yes | string (uuid) |

##### Responses

| Code | Description |
| ---- | ----------- |
| 204 | Diagnóstico iniciado com sucesso |
| 400 | Dados inválidos fornecidos |
| 403 | Acesso negado |
| 404 | Ordem de serviço não encontrada |
| 422 | Erro de regra do domínio |
| 500 | Erro interno do servidor |

### /api/ordens-servico/{id}/orcamento

#### POST
##### Summary:

Gerar orçamento da ordem de serviço

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | ID da ordem de serviço | Yes | string (uuid) |

##### Responses

| Code | Description |
| ---- | ----------- |
| 201 | Orçamento gerado com sucesso |
| 400 | Dados inválidos fornecidos |
| 403 | Acesso negado |
| 404 | Ordem de serviço não encontrada |
| 409 | Orçamento já foi gerado |
| 422 | Erro de regra do domínio |
| 500 | Erro interno do servidor |

### /api/ordens-servico/{id}/orcamento/aprovar

#### POST
##### Summary:

Aprovar orçamento da ordem de serviço, iniciando sua execução

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | ID da ordem de serviço | Yes | string (uuid) |

##### Responses

| Code | Description |
| ---- | ----------- |
| 204 | Orçamento aprovado com sucesso |
| 400 | Dados inválidos fornecidos |
| 404 | Ordem de serviço não encontrada |
| 422 | Erro de regra do domínio |
| 500 | Erro interno do servidor |

### /api/ordens-servico/{id}/orcamento/desaprovar

#### POST
##### Summary:

Desaprovar orçamento ordem de serviço, causando seu cancelamento

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | ID da ordem de serviço | Yes | string (uuid) |

##### Responses

| Code | Description |
| ---- | ----------- |
| 204 | Orçamento desaprovado com sucesso |
| 400 | Dados inválidos fornecidos |
| 404 | Ordem de serviço não encontrada |
| 422 | Erro de regra do domínio |
| 500 | Erro interno do servidor |

### /api/ordens-servico/{id}/finalizar-execucao

#### POST
##### Summary:

Finalizar execução da ordem de serviço

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | ID da ordem de serviço | Yes | string (uuid) |

##### Responses

| Code | Description |
| ---- | ----------- |
| 204 | Execução finalizada com sucesso |
| 400 | Dados inválidos fornecidos |
| 403 | Acesso negado |
| 404 | Ordem de serviço não encontrada |
| 422 | Erro de regra do domínio |
| 500 | Erro interno do servidor |

### /api/ordens-servico/{id}/entregar

#### POST
##### Summary:

Entregar ordem de serviço

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | ID da ordem de serviço | Yes | string (uuid) |

##### Responses

| Code | Description |
| ---- | ----------- |
| 204 | Ordem de serviço entregue com sucesso |
| 400 | Dados inválidos fornecidos |
| 403 | Acesso negado |
| 404 | Ordem de serviço não encontrada |
| 422 | Erro de regra do domínio |
| 500 | Erro interno do servidor |

### /api/ordens-servico/tempo-medio

#### GET
##### Summary:

Obter tempo médio de execução das ordens de serviço. Considera apenas ordes de serviço entregues, com criação de acordo com a quantidade de dias específicada.

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| quantidadeDias | query | Quantidade de dias para análise (1-365). Padrão: 365 | No | integer |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Tempo médio calculado com sucesso |
| 400 | Parâmetros inválidos ou nenhuma ordem encontrada |
| 403 | Acesso negado |
| 422 | Erro de regra do domínio |
| 500 | Erro interno do servidor |

### /api/ordens-servico/busca-publica

#### POST
##### Summary:

Busca pública de ordem de serviço por código e documento do cliente

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Busca realizada com sucesso |

### /api/ordens-servico/orcamento/aprovar/webhook

#### POST
##### Summary:

Webhook para aprovação de orçamento de ordem de serviço, iniciando sua execução

##### Responses

| Code | Description |
| ---- | ----------- |
| 204 | Orçamento aprovado com sucesso |
| 400 | Dados inválidos fornecidos |
| 401 | Assinatura HMAC inválida ou ausente |
| 404 | Ordem de serviço não encontrada |
| 422 | Erro de regra do domínio |
| 500 | Erro interno do servidor |

### /api/ordens-servico/orcamento/desaprovar/webhook

#### POST
##### Summary:

Webhook para desaprovação de orçamento ordem de serviço, causando seu cancelamento

##### Responses

| Code | Description |
| ---- | ----------- |
| 204 | Orçamento desaprovado com sucesso |
| 400 | Dados inválidos fornecidos |
| 401 | Assinatura HMAC inválida ou ausente |
| 404 | Ordem de serviço não encontrada |
| 422 | Erro de regra do domínio |
| 500 | Erro interno do servidor |

### /api/ordens-servico/status/webhook

#### POST
##### Summary:

Webhook para alterar o status da ordem de serviço

##### Responses

| Code | Description |
| ---- | ----------- |
| 204 | Status alterado com sucesso |
| 400 | Dados inválidos fornecidos |
| 401 | Assinatura HMAC inválida ou ausente |
| 404 | Ordem de serviço não encontrada |
| 422 | Erro de regra do domínio |
| 500 | Erro interno do servidor |

### /api/cadastros/servicos

#### GET
##### Summary:

Buscar todos os serviços

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Lista de serviços retornada com sucesso |
| 500 | Erro interno do servidor |

#### POST
##### Summary:

Criar um novo serviço

##### Responses

| Code | Description |
| ---- | ----------- |
| 201 | Serviço criado com sucesso |
| 400 | Dados inválidos fornecidos |
| 409 | Conflito - Serviço já existe |
| 500 | Erro interno do servidor |

### /api/cadastros/servicos/{id}

#### GET
##### Summary:

Buscar serviço por ID

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | ID do serviço | Yes | string (uuid) |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Serviço encontrado com sucesso |
| 404 | Serviço não encontrado |
| 500 | Erro interno do servidor |

#### PUT
##### Summary:

Atualizar um serviço existente

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | ID do serviço a ser atualizado | Yes | string (uuid) |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Serviço atualizado com sucesso |
| 400 | Dados inválidos fornecidos |
| 404 | Serviço não encontrado |
| 500 | Erro interno do servidor |

### /api/identidade/usuarios/documento/{documento}

#### GET
##### Summary:

Buscar usuário por documento (CPF ou CNPJ)

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| documento | path | CPF ou CNPJ, com ou sem formatação | Yes | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Usuário encontrado com sucesso |
| 404 | Usuário não encontrado |
| 500 | Erro interno do servidor |

### /api/identidade/usuarios

#### POST
##### Summary:

Criar um novo usuário

##### Responses

| Code | Description |
| ---- | ----------- |
| 201 | Usuário criado com sucesso |
| 400 | Dados inválidos fornecidos |
| 409 | Conflito - Usuário já existe |
| 500 | Erro interno do servidor |

### /api/cadastros/veiculos

#### GET
##### Summary:

Buscar todos os veículos

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Lista de veículos retornada com sucesso |
| 403 | Acesso negado |
| 500 | Erro interno do servidor |

#### POST
##### Summary:

Criar um novo veículo

##### Responses

| Code | Description |
| ---- | ----------- |
| 201 | Veículo criado com sucesso |
| 400 | Dados inválidos fornecidos |
| 403 | Acesso negado |
| 409 | Placa já cadastrada |
| 500 | Erro interno do servidor |

### /api/cadastros/veiculos/{id}

#### GET
##### Summary:

Buscar veículo por ID

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | ID do veículo | Yes | string (uuid) |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Veículo encontrado com sucesso |
| 403 | Acesso negado |
| 404 | Veículo não encontrado |
| 500 | Erro interno do servidor |

#### PUT
##### Summary:

Atualizar um veículo existente

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | ID do veículo | Yes | string (uuid) |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Veículo atualizado com sucesso |
| 400 | Dados inválidos fornecidos |
| 403 | Acesso negado |
| 404 | Veículo não encontrado |
| 500 | Erro interno do servidor |

### /api/cadastros/veiculos/placa/{placa}

#### GET
##### Summary:

Buscar veículo por placa

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| placa | path | Placa do veículo | Yes | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Veículo encontrado com sucesso |
| 403 | Acesso negado |
| 404 | Veículo não encontrado |
| 500 | Erro interno do servidor |

### /api/cadastros/veiculos/cliente/{clienteId}

#### GET
##### Summary:

Buscar veículos por ID do cliente

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| clienteId | path | ID do cliente | Yes | string (uuid) |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Veículos encontrados com sucesso |
| 403 | Acesso negado |
| 422 | Cliente não encontrado |
| 500 | Erro interno do servidor |

### /auth/authenticate

#### POST
##### Summary:

Realiza o login e retorna o Token JWT (Processado via AWS Lambda)

##### Description:

Este endpoint é interceptado pelo API Gateway e processado por uma AWS Lambda externa. O endpoint não é implementado diretamente na aplicação, mas é documentado aqui para referência da API completa.

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Token gerado com sucesso |
| 400 | Dados de entrada inválidos |
| 404 | Usuário não encontrado |
| 500 | Erro interno do servidor |
