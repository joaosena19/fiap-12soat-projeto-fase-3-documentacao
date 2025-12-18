# Modelo de banco de dados

## Escolha do banco de dados

## Tecnologia
- **Sistema**: PostgreSQL
- **ORM**: Entity Framework Core (API Backend) e Dapper (Lambda Functions)

O motivo da escolha do banco PostgreSQL é por ser um banco relacional, que se encaixa bem com esta aplicação, já que temos diversos relacionamentos entre Cliente, Veículo, Ordem de Serviço etc. e especificamente o Postgre pois é gratuito e facilmente configurável via Docker.

Foi adotada uma abordagem code-first, mapeando as entidades e delegando para o Entity Framework Core a criação das tabelas, definição de campos e relacionamentos.

## Diagrama de Entidade e Relacionamento

![Diagrama ER](Anexos/diagrama_er.png)

## Relacionamentos

### Ordem de Serviço

### Serviços

### Itens de estoque

### Clientes e Usuários

`clientes` possuem um ou mais `veiculos`. Eles são os donos dos veículos e indiretamente podem ser associados à ordens de serviço.

`usuarios` possuem diversas `roles` através da tabela auxilar `usuarios_roles`. Eles são atores dentro do sistema que realizam ações.

`clientes` e `usuários` não estão fisicamente ligados, eles são independentes e podem existir um sem um outro. A necessidade disso é que um cliente pode ser cadastrado no sistema sem ele diretamente acessá-lo (e.g.: atendimento de balcão), e o usuário também não necessariamente é ligada a um cliente, pois pode ser apenas um usuário administrador que gerencia o sistema sem nunca atuar como cliente. 

Eventualmente, clientes e usuários podem estar ligados de forma fraca com através da propriedade `documento_identificador`.