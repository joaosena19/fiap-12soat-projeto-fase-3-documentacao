# ADR 0002 - Comunicação REST Síncrona

## Status

Aceito

## Contexto

O sistema precisa expor suas funcionalidades (cadastro de clientes, veículos, gestão de OS) para serem consumidas por interfaces web ou outros serviços. Era necessário definir o padrão de arquitetura dessa comunicação.

## Discussão e possibilidades

Sobre o protocolo, a escolha natural foi **REST**. É o padrão absoluto de mercado, a integração com .NET é nativa e é a tecnologia com a qual tenho mais familiaridade. Usar GraphQL ou gRPC traria uma curva de aprendizado que não se justifica para o escopo deste projeto.

Sobre o modelo de comunicação, analisei os casos de uso do sistema, e todos são ações diretas onde o usuário espera um feedback imediato de sucesso ou erro. Não há nenhum processamento pesado que justifique processamento assíncrono.

## Decisão

Foi decidido utilizar **API REST com comunicação Síncrona**.

## Consequências

**Positivas:**

* Simplicidade de implementação e debug.
* Feedback imediato para o usuário final (ele sabe na hora se o cadastro funcionou).
* Facilidade de documentar (Swagger/OpenAPI).

**Negativas:**

* Nenhum ponto negativo identificado até o momento.

---
Anterior: [ADR 0001 - C# e Plataforma .NET](0001_adr_csharp_como_linguagem.md)  
Próximo: [ADR 0003 - Arquitetura Monolítica para Aplicação Principal](0003_adr_arquitetura_monolitica.md)