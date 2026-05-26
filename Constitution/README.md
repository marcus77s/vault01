---
type: constitution
created: 2026-05-26
---

# Constituição do Vault

## Estrutura de Pastas

| Pasta | Tipo de Memória | Regra |
|-------|----------------|-------|
| `/_workspace/active/` | RAM (curto prazo) | Rascunhos de agentes em execução. Arquivos temporários. |
| `/_workspace/archive/` | RAM arquivada | Concluídos, aguardando processamento pelo Bibliotecário. |
| `/Knowledge/Concepts/` | Semântica | Uma ideia por arquivo. Notas atômicas. |
| `/Knowledge/Decisions/` | Raciocínio | Decisões + justificativas ("por que X, não Y"). |
| `/Knowledge/Pending/` | Human-in-loop | Conflitos e decisões aguardando humano. |
| `/Journal/` | Episódica | Uma nota por dia. Append-only. |
| `/Projects/` | Projetos ativos | Estado atual de cada projeto. |
| `/Constitution/` | Governança | Leis do ecossistema. |

## Regras dos Agentes

1. **Append-only em Journal** — nunca sobrescrever, apenas adicionar ao final.
2. **Notas atômicas em Knowledge** — um conceito por arquivo.
3. **Conhecimento ≠ Raciocínio** — fatos em `Concepts/`, decisões em `Decisions/`.
4. **Conflito entre agentes** → criar nota em `Knowledge/Pending/` para resolução humana.
5. **Todo arquivo criado por agente** deve ter frontmatter YAML com `created`, `type`, `tags` e `agent`.
6. **Git commit** após cada tarefa crítica com mensagem descritiva.

## Frontmatter Padrão

```yaml
---
type: concept | decision | project | journal | workspace
created: YYYY-MM-DD
tags: []
agent: nome-do-agente
importance: low | medium | high
---
```
