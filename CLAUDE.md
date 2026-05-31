# LLM Wiki Schema — vault01

## O que é este vault

Este vault é uma **LLM Wiki**: uma base de conhecimento persistente e interligada
mantida pelo Claude Code. Marcus cuida da curadoria de fontes e faz as perguntas.
Claude escreve e mantém todo o wiki — resumos, páginas de conceitos, sínteses,
cross-references, log e índice.

**Regra fundamental**: arquivos em `Clippings/` e `RSS articles/` são **fontes brutas
imutáveis**. O Claude lê, nunca modifica. Tudo o que o Claude cria vai em `Knowledge/`.

Vault localizado em: `/home/marcus/Documentos/vault01/vault01/`

---

## Estrutura de Pastas

| Pasta | Papel | Regra |
|-------|-------|-------|
| `Clippings/` | Fontes brutas (web clips) | **Imutável** — LLM só lê |
| `RSS articles/` | Fontes brutas (RSS) | **Imutável** — LLM só lê |
| `raw/` | Fontes brutas (arquivos locais) | **Imutável** — LLM só lê |
| `Knowledge/Summaries/` | Resumos de fontes ingeridas | Um arquivo por fonte |
| `Knowledge/Concepts/` | Páginas de entidades e conceitos | Uma ideia por arquivo |
| `Knowledge/Decisions/` | Decisões e trade-offs | "Por que X e não Y" |
| `Knowledge/Synthesis/` | Sínteses temáticas amplas | Visões cross-source de alto nível |
| `Knowledge/Pending/` | Conflitos aguardando Marcus | Contradições + relatórios de lint |
| `Projects/` | Estado de projetos ativos | Um arquivo por projeto |
| `Journal/` | Memória episódica e registros | Append-only |
| `_workspace/active/` | RAM de agentes em execução | Temporário — limpar ao concluir |
| `_workspace/archive/` | Tarefas concluídas | Aguardando processamento |
| `Constitution/` | Governança do ecossistema | Ver `Constitution/README.md` |
| `index.md` | Índice geral do wiki | Atualizar a cada operação |
| `log.md` | Log cronológico | Append-only — nunca editar entradas antigas |

---

## Frontmatter Padrão

Todo arquivo criado pelo Claude deve ter frontmatter YAML completo:

```yaml
---
type: summary | concept | decision | synthesis | project | journal | pending
status: current | stub | outdated
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: []
sources: []        # caminhos relativos ao vault (ex: raw/llm-wiki.md)
importance: low | medium | high
agent: claude
---
```

**Regra `updated`**: sempre que editar qualquer campo ou seção de uma página existente,
atualize o `updated:` para a data de hoje. Páginas com `updated` > 60 dias são candidatas
a lint.

**Regra `status`**:
- `current` — informação verificada e atualizada
- `stub` — página criada mas conteúdo incompleto; precisa expansão
- `outdated` — conteúdo provavelmente superado; marcar e avisar Marcus

---

## Convenções de Nomenclatura

| Tipo de arquivo | Convenção | Exemplo |
|-----------------|-----------|---------|
| Conceitos (`Knowledge/Concepts/`) | **PascalCase** | `AgentMemory.md` |
| Wikilinks de conceito | **PascalCase** | `[[AgentMemory]]` |
| Summaries, Decisions, Synthesis | **kebab-case** | `hermes-agent-tutorial.md` |
| Projects, Journal | **kebab-case** | `diretor-de-cinema.md` |

Link liberalmente — toda menção de conceito relevante deve virar `[[WikiLink]]`.
Links são o que torna o wiki valioso: cross-references prontos = conhecimento compilado.

---

## Operação 1 — Ingestão de Fonte

**Gatilho**: Marcus diz "ingira", "processe", "adicione ao wiki" ou aponta para um arquivo.

**Fluxo**:

1. **Leia** a fonte (`Clippings/`, `RSS articles/`, `raw/`, ou caminho fornecido)
2. **Discuta** brevemente com Marcus: principais insights, o que é relevante para o wiki
3. **Crie** `Knowledge/Summaries/<titulo-kebab>.md` com:
   - Frontmatter completo (`type: summary`, `status: current`, `sources: [caminho]`)
   - `## Resumo` — problema, solução, insights-chave
   - `## Citações Relevantes` — trechos diretos importantes
   - `## Conexões` — lista de `[[WikiPage]]` existentes que este conteúdo toca
   - `## Lacunas / Perguntas` — o que a fonte levanta mas não responde
4. **Atualize** `Knowledge/Concepts/`:
   - Crie páginas novas (`status: current`) para entidades relevantes
   - Atualize páginas existentes + atualize o campo `updated:`
5. **Verifique** `Knowledge/Decisions/`:
   - Esta fonte contradiz alguma decisão? → atualizar ou criar `Pending`
   - Reforça alguma decisão? → adicionar referência
6. **Sinalize contradições** → `Knowledge/Pending/conflito-<data>.md`
7. **Atualize** `index.md` — nova fonte em "Fontes Ingeridas", novas páginas nas categorias
8. **Append** em `log.md`:
   ```
   ## [YYYY-MM-DD] ingest | Título da Fonte
   Criado: Knowledge/Summaries/titulo-kebab.md
   Conceitos criados: [[Conceito1]], [[Conceito2]]
   Conceitos atualizados: [[Conceito3]] (adicionado X)
   ```

---

## Operação 2 — Query

**Gatilho**: Marcus faz uma pergunta sobre o domínio do wiki.

**Fluxo**:

1. **Leia** `index.md` para identificar páginas relevantes
2. **Leia** as páginas identificadas em `Knowledge/`
3. **Sintetize** a resposta com referências `[[WikiPage]]` e citações de sources
4. **Pergunte** Marcus: "Quer que eu salve esta análise como página de síntese?"
5. Se sim → crie `Knowledge/Synthesis/<topico-kebab>.md` (`status: current`) e adicione ao `index.md`
6. **Append** em `log.md`:
   ```
   ## [YYYY-MM-DD] query | Resumo da pergunta
   Páginas consultadas: [[P1]], [[P2]]
   Síntese salva: Knowledge/Synthesis/topico.md | não
   ```

---

## Operação 3 — Lint (Saúde do Wiki)

**Gatilho**: Marcus diz "verifique o wiki", "lint", "saúde do wiki".

**Fluxo**:

1. **Inventário** — leia `index.md`
2. **Verifique** amostrando páginas em `Knowledge/`:
   - Páginas com `status: stub` ou `status: outdated`
   - `updated` > 60 dias (potencialmente obsoleto)
   - Wikilinks no texto que não têm página própria
   - Contradições entre páginas do mesmo conceito
   - Claims em Summaries que fontes mais recentes contradizem
3. **Comandos úteis**:
   ```bash
   # Páginas stub ou outdated
   grep -r "status: stub\|status: outdated" Knowledge/ -l

   # Páginas não atualizadas há mais de 60 dias (checar manualmente)
   grep -r "^updated:" Knowledge/ | sort -t: -k2

   # Wikilinks sem página correspondente (links quebrados)
   grep -roh '\[\[[A-Za-z][A-Za-z0-9-]*\]\]' Knowledge/ | sort -u

   # Buscar por conceito
   grep -r "AgentMemory" Knowledge/
   ```
4. **Salve** relatório em `Knowledge/Pending/lint-YYYY-MM-DD.md`
5. **Append** em `log.md`:
   ```
   ## [YYYY-MM-DD] lint
   Stubs: N. Outdated: X. Links quebrados: Y. Contradições: Z.
   Relatório: Knowledge/Pending/lint-YYYY-MM-DD.md
   ```

---

## Operação 4 — Manutenção de Páginas Existentes

**Gatilho**: Marcus diz "atualize X", "isso mudou", "adicione Y ao conceito Z", ou ao ingerir
uma fonte que contradiz/expande conteúdo existente.

**Fluxo**:

1. **Leia** a página existente antes de qualquer edição
2. **Edite** o conteúdo relevante
3. **Sempre** atualize `updated: YYYY-MM-DD` no frontmatter
4. Se o conteúdo antigo se tornou obsoleto mas ainda tem valor histórico:
   - Mova para seção `## [Histórico]` no final da página, com data
   - Mantenha `status: current` se a página em geral ainda está válida
5. Se a informação inteira está superada → mude para `status: outdated` e crie nota em
   `Knowledge/Pending/` avisando Marcus
6. **Append** em `log.md`:
   ```
   ## [YYYY-MM-DD] update | NomeDaPagina
   Alteração: descrição do que mudou e por quê
   ```

---

## Formatos de Output

| Formato | Quando usar |
|---------|------------|
| Página markdown | Padrão — qualquer síntese ou análise |
| Tabela de comparação | "Compare X e Y", "Diferenças entre A e B" |
| Marp slides (`marp: true` no frontmatter) | Apresentações, quando Marcus pedir |

---

## Regras Operacionais

1. **Leia `index.md` antes de qualquer operação** — para saber o que já existe
2. **Prefira atualizar páginas existentes** a criar duplicatas
3. **Atualize `updated:` sempre que editar uma página**
4. **Nunca edite entradas antigas do `log.md`** — apenas append
5. **Fontes em `Clippings/`, `RSS articles/` e `raw/` são imutáveis** — nunca modifique, mova ou delete
6. **Conflitos e lint vão para `Knowledge/Pending/`** — Marcus decide, não o Claude
7. **`_workspace/active/`** — use para rascunhos de tarefas longas; mova para `archive/` ao concluir
8. **Git commit** após cada ingestão completa

---

## Navegação Rápida

```bash
# Ver as últimas 10 operações
grep "^## \[" log.md | tail -10

# Buscar por conceito em todo o wiki
grep -r "LangGraph" Knowledge/

# Ver todas as páginas por tipo
grep -rl "^type: concept" Knowledge/
grep -rl "^status: stub" Knowledge/

# Ver estrutura do vault
find . -name "*.md" -not -path "./.git/*" -not -path "./.obsidian/*" | sort
```

Consulte também `Constitution/README.md` para as regras de governança do ecossistema.
