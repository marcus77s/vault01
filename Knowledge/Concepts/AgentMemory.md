---
type: concept
status: current
created: 2026-05-30
updated: 2026-05-30
tags: [agent-memory, memory, persistence, cognitive-architecture]
sources: [raw/llm-wiki.md, raw/Hermes Agent Tutorial for Beginners - Step by Step-PT.md]
importance: high
agent: claude
---

# AgentMemory

Capacidade de um agente de IA de manter e recuperar informação entre sessões distintas. Central para arquitetura cognitiva de agentes.

## Formas de implementação

### Memória Interna (in-context)
- Incluída no prompt a cada sessão
- Limitada pelo tamanho do contexto
- Exemplo: resumo de preferências do usuário injetado no system prompt

### Memória Externa (out-of-context)
- Armazenada fora do modelo (arquivos, banco de dados)
- Recuperada por busca (RAG, index, grep)
- Exemplos: [[LLMWiki]], ChromaDB, SQLite

### Memória do [[HermesAgent]]
- Preferências salvas em arquivos no servidor VPS
- Contexto acumulado entre conversas via Telegram
- "Quanto mais tempo você tiver o Hermes, mais ele acumula, mais contexto, mais conhecimento e menos você precisa se repetir"

## Dimensões da memória

| Dimensão | Descrição |
|----------|-----------|
| **Semântica** | Fatos e conhecimento (quem é o usuário, domínio de trabalho) |
| **Episódica** | Histórico de interações passadas |
| **Procedural** | Como fazer tarefas (→ [[AgentSkills]] no Hermes) |

## LLM Wiki como memória externa

O padrão [[LLMWiki]] pode ser entendido como uma implementação de memória externa de longo prazo:
- O wiki é o "estado cerebral" persistente do agente
- O schema (CLAUDE.md) é a "meta-memória" — como o agente sabe como operar
- O log.md é a memória episódica

## Ligações

- [[LLMWiki]] — implementação de memória externa via wiki markdown
- [[RAG]] — técnica de recuperação de memória externa
- [[HermesAgent]] — agente com memória persistente integrada
- [[AgentSkills]] — memória procedural (como fazer tarefas)
