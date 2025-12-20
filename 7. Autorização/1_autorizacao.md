# Autorização

## Contexto

Inicialmente o projeto não possuía o conceito de "usuário", a autenticação com a API era feita via Client Credentials (Client ID + Client Secret) e qualquer pessoa com um token válido poderia acessar todos os recursos. Isso foi suficiente para a primeira e segunda fase do Tech Challenge, imaginado um sistema que seria usado apenas dentro da Oficina, em um computador compartilhado pelos funcionários.

O Tech Challenge 3 teve como requisito autenticação via Function Serverless baseada no CPF do cliente. Isso implicou na necessidade de criar um perfil de usuário e deixar com que o **cliente** acessasse o sistema, algo que não havia sido previsto inicialmente.

## Implementação

### Usuário x Cliente

Primeiramente, o sistema diferencia o conceito de **Usuário** e **Cliente**. O Cliente é a pessoa dona do veículo, que indiretamente está associada a Ordens de Serviço.

O Usuário é a pessoa que efetivamente acessa o sistema, podendo ser um funcionário da Oficina (mecânico, atendente, gerente) ou o próprio Cliente (dono do veículo).

Um Cliente pode ser um Usuário, e um Usuário pode ser um Cliente, mas não necessariamente os dois precisam estar associados. É possível que o Cliente não seja Usuário (por exemplo atendimento de balcão, onde um funcionário administrador criou o registro daquele Cliente), e também é possível que um Usuário não seja um Cliente (por exemplo, um funcionário que acessa o sistema).

### Criação de Usuários

Os usuários são criados através do `CriarUsuarioUseCase`, que está disponível apenas para Administradores. Esse UseCase recebe uma o documento do usuário, suas roles, e uma senha em texto plano que será hasheada com Argon2 e antes de ser armazenada no banco de dados.

### Roles de Usuário

Os Usuários possuem Roles (perfis) que definem o que eles podem fazer no sistema. As Roles são:

- Administrador: acesso total ao sistema, pode gerenciar usuários, clientes, veículos, ordens de serviço, etc.
- Cliente: acesso restrito, pode ver e gerenciar apenas seu própria cadastro e visualizar suas ordens de serviço.
- Sistema: acesso aos webhooks com autenticação HMAC

### Ownership

Um usuário Administrador pode acessar e gerenciar qualquer recurso do sistema, porém um usuário Cliente só pode acessar os recursos que pertencem a ele mesmo. Por exemplo, um usuário Cliente autenticado e com token válido não pode simplesmente ter acesso a uma rota de buscar ordem de serviço, senão ele poderia ver as ordens de serviço de qualquer outro cliente.

Isso é implementado através dos extensions methods na classe `Ator`, que podem receber um Aggregate que possui um `ClienteId`, ou então receber um Gateway (repository) para verificar se o recurso pertence ao cliente do usuário autenticado.

### Classe Ator

Para implementar a autorização baseada em roles e ownership, foi criada a classe `Ator`, que representa o usuário que está executando a ação. Cada um dos Use Cases recebe uma instância de `Ator` que informa quem está executando a ação, e o Use Case pode então verificar as permissões necessárias.

O Ator tem informações de `UsuarioId`, `ClienteId` (opcional) e uma lista de `Roles`. Cada módulo do sistema implementa extensions methods como `PodeListarClientes` ou `PodeAcessarVeiculo` que encapsulam a lógica de verificar as roles e ownership necessárias para aquela ação.

O uso dentro Use Case fica muito simples e fluente, chamando os métodos de Ator no início do método, por exemplo:

```csharp
    public async Task ExecutarAsync(Ator ator, [... parâmetros do caso de uso ...])
    {
        try
        {
            if (!ator.PodeGerenciarOrdemServico())
                throw new DomainException("Acesso negado");

        }catch (DomainException ex)
        {
            // tratamento de erro
        }
```

### Código relacionado:

#### Banco de Dados

Tabelas: `clientes`, `usuarios`, `usuarios_roles`, `roles`

#### API Principal

`\Domain\Identidade\` -> classes de Usuário e Roles de domínio
`\Application\Identidade\` -> use cases de usuário, e classe Ator com seus métodos de extensão
`\Infrastructure\Authentication\AtorFactories\` -> factory que cria classe Ator a partir do token JWT

#### Lambda Login

`\AuthLambda\LoginHandler.cs` -> busca usuário no banco e valida senha, gera token JWT com roles e IDs