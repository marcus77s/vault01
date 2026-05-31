---
type: concept
created: 2026-05-30
updated: 2026-05-30
tags: [llm-wiki, knowledge-base, pattern, obsidian]
sources: [raw/llm-wiki.md]
importance: high
agent: claude
---

# LLM Wiki

Padrão arquitetural para bases de conhecimento pessoais mantidas por LLMs. Cunhado por Andrej Karpathy.

## Definição

Um LLM Wiki é uma coleção estruturada e interligada de arquivos markdown onde o LLM **escreve e mantém** o conteúdo incrementalmente — em vez de apenas recuperar de fontes brutas como no [[RAG]].

A distinção fundamental: o wiki é um **artefato persistente e composto**. Quando uma nova fonte é adicionada, o LLM integra o conhecimento ao wiki existente — atualiza páginas de entidades, revisa resumos, sinaliza contradições. O conhecimento é compilado uma vez e mantido atualizado, não re-derivado a cada query.

## Arquitetura

```
Fontes brutas (imutáveis)
        ↓ ingest
    Wiki (LLM escreve)
    ├── Summaries/     — um arquivo por fonte ingerida
    ├── Concepts/      — páginas de entidades e conceitos
    ├── Decisions/     — sínteses e raciocínio
    ├── Synthesis/     — visões temáticas amplas
    └── Pending/       — conflitos aguardando humano
        ↑ query
    Schema (CLAUDE.md / AGENTS.md)
```

## Propriedades

- **Persistência**: o wiki sobrevive entre conversas; o LLM lê o estado atual antes de agir
- **Composição**: cada ingestão enriquece páginas existentes, não apenas adiciona uma nova
- **Navegabilidade**: wikilinks (`[[Conceito]]`) criam grafo de conhecimento navegável no Obsidian
- **Grep-friendly**: convenções consistentes permitem busca com ferramentas Unix simples
- **Manutenção zero-custo**: LLMs não se cansam de atualizar cross-references

## Comparação com RAG

| Dimensão | LLM Wiki | [[RAG]] |
|----------|----------|---------|
| Conhecimento | Compilado e mantido | Re-derivado a cada query |
| Cross-references | Pré-construídas | Não existem |
| Contradições | Sinalizadas na ingestão | Invisíveis |
| Infraestrutura | Markdown + git | Vector DB + embeddings |
| Escala | ~100s fontes (index.md) | Milhares de docs |

## Implementações conhecidas

- Este vault (`vault01`) — implementação de Marcus com Claude Code
- Qualquer Obsidian vault com CLAUDE.md/AGENTS.md seguindo este padrão

## Ligações

- [[RAG]] — abordagem alternativa para knowledge retrieval
- [[MemexPattern]] — inspiração histórica (Vannevar Bush, 1945)
- [[AgentMemory]] — LLM Wiki como forma de memória externa de longo prazo
