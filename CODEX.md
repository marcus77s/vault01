---
type: constitution
status: current
created: 2026-06-01
updated: 2026-06-01
tags: [governance, codex, llm-wiki, memory]
sources:
  - Constitution/README.md
  - Constitution/agent-update-tutorial.md
  - CLAUDE.md
importance: high
agent: Codex
---

# LLM Wiki Schema — Codex no vault01

Este arquivo registra como o Codex deve operar neste vault. A fonte de verdade do
schema continua sendo `CLAUDE.md`, `Constitution/README.md` e
`Constitution/agent-update-tutorial.md`; se houver contradição, seguir esses
arquivos nessa ordem prática: `CLAUDE.md` para workflow, `Constitution/README.md`
para governança, tutorial para transição de schema.

Vault localizado em: `/home/marcus/Documentos/vault01/vault01/`

## Regra Fundamental

`Clippings/`, `RSS articles/` e `raw/` são fontes brutas imutáveis. O Codex pode
ler e citar esses arquivos, mas nunca modificar, mover ou remover.

Conteúdo criado por agente deve ir para `Knowledge/`, `Projects/`, `Journal/`,
`_workspace/` ou `Constitution/`, conforme o papel da nota.

## Estrutura de Memória

| Pasta | Tipo de memória | Regra |
|-------|-----------------|-------|
| `Clippings/` | Fonte bruta | Imutável. Web clips e documentos de entrada. |
| `RSS articles/` | Fonte bruta | Imutável. Artigos vindos de RSS. |
| `raw/` | Fonte bruta | Imutável. Arquivos locais de entrada. |
| `Knowledge/Summaries/` | Ingestão | Um resumo por fonte ingerida. |
| `Knowledge/Concepts/` | Semântica | Uma ideia, entidade ou conceito por arquivo. |
| `Knowledge/Decisions/` | Raciocínio | Decisões, trade-offs e justificativas. |
| `Knowledge/Synthesis/` | Síntese | Análises temáticas multi-fonte. |
| `Knowledge/Pending/` | Human-in-loop | Conflitos, dúvidas e lint aguardando Marcus. |
| `Projects/` | Projetos ativos | Estado atual de cada projeto. |
| `Journal/` | Episódica | Uma nota por dia ou registro append-only. |
| `_workspace/active/` | RAM | Rascunhos de tarefas longas em andamento. |
| `_workspace/archive/` | RAM arquivada | Tarefas concluídas aguardando processamento. |
| `Constitution/` | Governança | Leis e convenções do ecossistema. |
| `index.md` | Mapa do wiki | Inventário navegável; ler antes de operar. |
| `log.md` | Histórico | Append-only; cada entrada começa com `## [YYYY-MM-DD]`. |

## Antes de Operar

1. Ler `index.md` para saber o que já existe.
2. Ler a página relevante antes de editar.
3. Preferir atualizar páginas existentes a criar duplicatas.
4. Usar `rg` para busca no vault.

## Regras dos Agentes

1. Ler `index.md` antes de qualquer operação no wiki.
2. Preferir atualizar páginas existentes a criar duplicatas.
3. Usar `Knowledge/Summaries/` para ingestões, `Knowledge/Concepts/` para fatos atômicos, `Knowledge/Decisions/` para raciocínio e `Knowledge/Synthesis/` para análises amplas.
4. Criar notas em `Knowledge/Pending/` quando houver conflito, contradição ou decisão que dependa de Marcus.
5. Nunca editar entradas antigas de `log.md`; apenas anexar novas entradas.
6. Manter `Journal/` append-only.
7. Usar wikilinks `[[NomeDaPagina]]` liberalmente para conceitos relevantes.
8. Usar nomes de conceitos em PascalCase e arquivos em kebab-case.
9. Todo arquivo criado por agente deve ter frontmatter YAML completo.
10. Fazer commit após tarefa crítica quando o fluxo de Git estiver disponível.

## Frontmatter Obrigatório

Todo arquivo novo criado pelo Codex deve ter frontmatter YAML completo:

```yaml
---
type: summary | concept | decision | synthesis | project | journal | pending
status: current | stub | outdated
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: []
sources: []
importance: low | medium | high
agent: Codex
---
```

- `status: current` para conteúdo verificado e útil.
- `status: stub` para placeholder incompleto.
- `status: outdated` para conteúdo superado.
- Sempre atualizar `updated:` ao editar qualquer página existente.

## Convenções

- Conceitos em `Knowledge/Concepts/`: PascalCase, como `AgentMemory.md`.
- Wikilinks de conceitos: PascalCase, como `[[AgentMemory]]`.
- Summaries, Decisions, Synthesis, Projects e Journal: kebab-case.
- Usar wikilinks liberalmente quando um conceito já existe ou merece virar página.

## Operações

### Ingestão

Quando Marcus pedir para ingerir/processar/adicionar uma fonte:

1. Ler a fonte.
2. Checar `index.md` e páginas relacionadas.
3. Criar ou atualizar `Knowledge/Summaries/`.
4. Criar ou atualizar conceitos em `Knowledge/Concepts/`.
5. Registrar decisões em `Knowledge/Decisions/` quando houver trade-off claro.
6. Criar pendência em `Knowledge/Pending/` se houver conflito ou incerteza.
7. Atualizar `index.md`.
8. Append em `log.md`.

### Query

Quando Marcus perguntar algo sobre o domínio do wiki:

1. Ler `index.md`.
2. Consultar páginas relevantes em `Knowledge/`.
3. Responder com síntese e referências por wikilink.
4. Perguntar se Marcus quer salvar a análise como `Knowledge/Synthesis/`.
5. Append em `log.md` registrando a consulta.

### Lint

Quando Marcus pedir "verifique o wiki", "lint" ou "saúde do wiki":

1. Ler `index.md`.
2. Procurar páginas órfãs, conceitos sem página, links quebrados, contradições, claims superados e páginas `stub` ou `outdated`.
3. Salvar relatório em `Knowledge/Pending/lint-YYYY-MM-DD.md`.
4. Append em `log.md`.

### Manutenção

Quando atualizar página existente:

1. Ler a página antes.
2. Editar somente o trecho necessário.
3. Atualizar `updated:` para a data de hoje.
4. Preservar histórico se conteúdo antigo ainda tiver valor.
5. Marcar `status: outdated` e criar `Knowledge/Pending/` se a página inteira estiver superada.
6. Append em `log.md`.

## Log

`log.md` é append-only. Nunca editar entradas antigas. Cada nova entrada começa com:

```md
## [YYYY-MM-DD] tipo | Título
```
