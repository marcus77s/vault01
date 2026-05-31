---
type: summary
status: current
created: 2026-05-30
updated: 2026-05-30
tags: [llm-wiki, knowledge-base, rag, obsidian, pattern]
sources: [raw/llm-wiki.md]
importance: high
agent: claude
---

# LLM Wiki — Padrão Karpathy

**Fonte:** [GitHub Gist — karpathy](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)

## Resumo

O LLM Wiki é um padrão arquitetural para bases de conhecimento pessoais onde o LLM não apenas recupera informação (como no [[RAG]]) mas **constrói e mantém incrementalmente um wiki persistente** de arquivos markdown interligados.

A diferença central: no RAG o LLM re-deriva conhecimento do zero a cada query. No LLM Wiki o conhecimento é compilado uma vez e mantido atualizado — as cross-references já existem, as contradições já foram sinalizadas, a síntese já reflete tudo que foi lido.

**As 3 camadas:**
1. **Fontes brutas** — imutáveis, o LLM só lê
2. **Wiki** — diretório de markdown gerado/mantido pelo LLM (summaries, concept pages, synthesis)
3. **Schema** — arquivo CLAUDE.md / AGENTS.md que define convenções e workflows

**As 3 operações:**
- **Ingest** — LLM lê nova fonte, cria summary, atualiza conceitos, atualiza index
- **Query** — LLM lê index, consulta páginas relevantes, sintetiza resposta; boas respostas viram novas páginas
- **Lint** — health-check periódico: contradições, páginas órfãs, claims desatualizados

**Navegação:**
- `index.md` — catálogo por categoria; LLM lê primeiro em toda query
- `log.md` — registro cronológico append-only; grep-friendly com prefixo `## [YYYY-MM-DD]`

## Citações Relevantes

> "The wiki is a persistent, compounding artifact. The cross-references are already there. The contradictions have already been flagged. The synthesis already reflects everything you've read."

> "The human's job is to curate sources, direct the analysis, ask good questions, and think about what it all means. The LLM's job is everything else."

> "Obsidian is the IDE; the LLM is the programmer; the wiki is the codebase."

> "Humans abandon wikis because the maintenance burden grows faster than the value. LLMs don't get bored, don't forget to update a cross-reference, and can touch 15 files in one pass."

## Conexões

- [[LLMWiki]] — conceito central deste padrão
- [[RAG]] — abordagem alternativa que este padrão supera para knowledge bases pessoais
- [[MemexPattern]] — inspiração histórica (Vannevar Bush, 1945)
- [[AgentMemory]] — memória persistente em agentes; LLM Wiki é uma forma de memória externa

## Lacunas / Perguntas

- Como escalar além de ~100 fontes sem RAG? O autor menciona `qmd` (BM25 + vector search local) mas não detalha integração
- Qual o limite prático de páginas antes que o index.md se torne ineficiente?
- Como lidar com fontes contraditórias em domínios que evoluem rápido (ex: papers de ML)?
- Estratégias de versionamento quando o LLM atualiza páginas existentes
