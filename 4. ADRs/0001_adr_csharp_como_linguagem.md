# ADR 0001 - C# e Plataforma .NET

## Status

Aceito

## Contexto

É preciso definir a linguagem de programação e o framework principal para o desenvolvimento do backend da aplicação. A escolha deve levar em conta a robustez para suportar as regras de negócio, o ecossistema de bibliotecas e a produtividade do desenvolvimento.

## Discussão e possibilidades

Avaliei três opções principais:

1. **C# (.NET):** É uma linguagem robusta, fortemente tipada e padrão de mercado corporativo. Tenho alta familiaridade com ela, o que garante velocidade no desenvolvimento e segurança na implementação de padrões complexos.
2. **Java:** Tão robusto quanto o C#, porém não tenho conhecimento prévio da linguagem. A curva de aprendizado inviabilizaria a entrega do projeto dentro do prazo.
3. **Node.js:** Tenho conhecimento, mas para este projeto, que envolve modelagem de domínio rica (DDD), considero o C# mais forte e estruturado devido à sua tipagem estática e recursos de Orientação a Objetos.

## Decisão

Foi decidido utilizar C# com a plataforma .NET.

## Consequências

**Positivas:**

* Alta produtividade devido à minha familiaridade com a stack.
* Ecossistema maduro (Entity Framework, Visual Studio, NuGet, etc).

**Negativas:**

* As imagens Docker tendem a ser um pouco maiores se comparadas com Node ou Go.
* Consumo de memória do container pode ser maior do que stacks mais leves.

---
Anterior: [Fluxo de criação de Ordem de Serviço](../3.%20Diagramas%20de%20Sequ%C3%AAncia/2_criacao_os.md)  
Próximo: [ADR 0002 - Comunicação REST Síncrona](0002_adr_padrao_comunicacao_rest_sincrono.md)