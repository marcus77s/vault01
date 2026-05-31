---
type: constitution
status: current
created: 2026-05-31
updated: 2026-05-31
tags: [governance, agents, update, tutorial, schema]
importance: high
agent: claude
---

# Tutorial de Atualização de Schema — Para Agentes

Este documento é para qualquer agente (Gemini, Codex, GPT, Claude, etc.) que operou
neste vault antes de **2026-05-31** e precisa se atualizar com as mudanças de schema.

Leia este arquivo **antes** de fazer qualquer operação no vault se você não reconhecer
o campo `status:` no frontmatter das páginas.

---

## O que mudou em 2026-05-31

### 1. Novo campo `status` no frontmatter

**Antes:**
```yaml
---
type: concept
created: 2026-05-30
updated: 2026-05-30
tags: [agent-memory]
importance: high
agent: claude
---
```

**Depois:**
```yaml
---
type: concept
status: current
created: 2026-05-30
updated: 2026-05-31
tags: [agent-memory]
importance: high
agent: claude
---
```

**Valores válidos para `status`:**

| Valor | Significado | Quando usar |
|-------|-------------|-------------|
| `current` | Informação verificada e atualizada | Padrão para páginas novas |
| `stub` | Página criada mas conteúdo incompleto | Quando criar placeholder para expandir depois |
| `outdated` | Conteúdo provavelmente superado | Quando nova fonte contradiz ou supera o conteúdo |

### 2. Regra obrigatória: manter `updated:` atual

O campo `updated:` agora tem uma regra ativa: **toda vez que você editar qualquer
parte de uma página existente, atualize `updated:` para a data de hoje.**

Páginas com `updated` > 60 dias são candidatas ao processo de lint.

### 3. Novos diretórios criados

Os seguintes diretórios agora existem (antes eram referenciados no schema mas não
existiam de fato):

```
Knowledge/Decisions/    — decisões e trade-offs ("por que X e não Y")
Knowledge/Pending/      — conflitos, contradições e relatórios de lint
_workspace/active/      — rascunhos de tarefas longas em andamento
_workspace/archive/     — tarefas concluídas aguardando processamento
```

Se você tinha o hábito de não usar esses diretórios porque não existiam, agora pode.

### 4. Nova Operação 4 — Manutenção

Existe agora um workflow explícito para atualizar páginas existentes. Veja a seção
completa em `CLAUDE.md` → "Operação 4 — Manutenção de Páginas Existentes".

Resumo rápido:
- Leia a página antes de editar
- Edite o conteúdo
- Atualize `updated:` no frontmatter
- Se ficou obsoleto mas tem valor histórico → mova para seção `## [Histórico]`
- Se está completamente superado → mude para `status: outdated` + nota em `Pending/`
- Append em `log.md` com `## [YYYY-MM-DD] update | NomeDaPagina`

### 5. Convenção de nomenclatura corrigida

O schema antigo dizia "kebab-case para arquivos de conceito" — isso estava **errado**.
A convenção correta, que já estava sendo usada na prática:

| Tipo | Convenção | Exemplo |
|------|-----------|---------|
| Arquivos em `Knowledge/Concepts/` | **PascalCase** | `AgentMemory.md` |
| Wikilinks de conceito | **PascalCase** | `[[AgentMemory]]` |
| Summaries, Decisions, Synthesis, Projects, Journal | **kebab-case** | `hermes-agent-tutorial.md` |

---

## O que você precisa fazer agora

### Passo 1 — Atualizar seu próprio arquivo de schema

Se você tem um arquivo de instruções dentro do vault (como `GEMINI.md`), adicione
as novas regras a ele. Os campos mínimos a adicionar:

```
- status: current | stub | outdated (novo campo obrigatório no frontmatter)
- updated: sempre atualizar ao editar qualquer página
- Operação 4 — Manutenção (novo workflow)
- Knowledge/Decisions/ e Knowledge/Pending/ agora existem e devem ser usados
```

### Passo 2 — Corrigir páginas que você criou sem o campo `status`

Se você criou páginas `Knowledge/Concepts/`, `Knowledge/Summaries/`, ou similares
sem o campo `status:`, corrija assim:

1. Abra cada página
2. Adicione `status: current` logo após a linha `type:`
3. Atualize `updated:` para a data de hoje
4. Salve

**Grep para encontrar suas páginas sem status:**
```bash
grep -rL "^status:" Knowledge/ Projects/ Journal/
```

### Passo 3 — Verificar `updated:` nas suas páginas

Se você editou páginas após a criação sem atualizar o `updated:`, corrija:

```bash
# Ver todas as datas updated (ordenadas)
grep -r "^updated:" Knowledge/ | sort -t: -k3
```

Qualquer página com `updated` diferente de hoje que você sabe que foi editada
recentemente → corrija manualmente.

### Passo 4 — Referenciar `raw/` como fonte imutável

O diretório `raw/` agora é listado explicitamente como fonte bruta imutável,
igual a `Clippings/` e `RSS articles/`. Se você referenciar fontes de `raw/`
em `sources:`, use o caminho relativo: `raw/nome-do-arquivo.md`.

---

## Checklist de atualização

Marque cada item antes de continuar operando no vault:

- [ ] Li o `CLAUDE.md` atualizado (ou meu equivalente de schema)
- [ ] Entendo o campo `status:` e seus três valores
- [ ] Sei que devo atualizar `updated:` toda vez que editar uma página
- [ ] Sei que `Knowledge/Decisions/`, `Knowledge/Pending/`, `_workspace/` agora existem
- [ ] Conheço a Operação 4 — Manutenção
- [ ] Corrigi minhas páginas anteriores adicionando `status: current`
- [ ] Atualizei meu próprio arquivo de schema (GEMINI.md, CLAUDE.md, etc.)

---

## Referência rápida — Frontmatter completo

```yaml
---
type: summary | concept | decision | synthesis | project | journal | pending
status: current | stub | outdated
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: []
sources: []
importance: low | medium | high
agent: nome-do-agente
---
```

---

## Dúvidas?

Consulte:
- `CLAUDE.md` — schema completo e operações
- `Constitution/README.md` — regras de governança
- `log.md` — histórico de operações (para entender o contexto das mudanças)

Se encontrar contradição entre este tutorial e `CLAUDE.md`, **`CLAUDE.md` prevalece**.
Este tutorial descreve a transição; `CLAUDE.md` é o estado definitivo.
