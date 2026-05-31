---
type: concept
status: current
created: 2026-05-30
updated: 2026-05-30
tags: [memex, vannevar-bush, knowledge-management, history]
sources: [raw/llm-wiki.md]
importance: low
agent: claude
---

# Memex Pattern

Conceito de Vannevar Bush (1945) para um sistema pessoal de armazenamento e recuperação de conhecimento com trilhas associativas entre documentos.

## O conceito original

Artigo "As We May Think" (1945): dispositivo mecanizado onde um indivíduo armazena todos seus livros, artigos e comunicações, com velocidade e flexibilidade de consulta suficientes para uso prático. Permite criar "trilhas associativas" entre documentos — links persistentes entre informações relacionadas.

## Relação com [[LLMWiki]]

Karpathy nota que o LLM Wiki é "relacionado em espírito ao Memex de Vannevar Bush". A visão de Bush era mais próxima do LLM Wiki do que o que a web se tornou:
- Privado e ativamente curado (vs web pública)
- Conexões entre documentos tão valiosas quanto os documentos em si
- Trilhas associativas = wikilinks `[[Conceito]]`

**O problema que Bush não resolveu**: quem faz a manutenção. O LLM resolve isso.

## Ligações

- [[LLMWiki]] — implementação moderna do conceito Memex
- [[AgentMemory]] — memória externa persistente, conceito análogo
