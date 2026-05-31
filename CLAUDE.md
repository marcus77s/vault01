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
| `Knowledge/Summaries/` | Resumos de fontes ingeridas | Um arquivo por fonte |
| `Knowledge/Concepts/` | Páginas de entidades e conceitos | Uma ideia por arquivo |
| `Knowledge/Decisions/` | Síntese e raciocínio | Análises multi-fonte, "por que X não Y" |
| `Knowledge/Synthesis/` | Sínteses temáticas amplas | Visões cross-source de alto nível |
| `Knowledge/Pending/` | Conflitos aguardando Marcus | Contradições não resolvidas |
| `Projects/` | Estado de projetos ativos | Um arquivo por projeto |
| `Journal/` | Memória episódica | Uma nota por dia — append-only |
| `_workspace/active/` | RAM de agentes em execução | Temporário |
| `_workspace/archive/` | Tarefas concluídas | Aguardando processamento |
| `Constitution/` | Governança do ecossistema | Ver `Constitution/README.md` |
| `index.md` | Índice geral do wiki | Atualizar a cada ingestão |
| `log.md` | Log cronológico | Append-only — nunca editar entradas antigas |

---

## Frontmatter Padrão

Todo arquivo criado pelo Claude deve ter frontmatter YAML:

```yaml
---
type: summary | concept | decision | synthesis | project | journal | pending
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: []
sources: []        # arquivos fonte que embasam este arquivo
importance: low | medium | high
agent: claude
---
```

---

## Operação 1 — Ingestão de Fonte

**Gatilho**: Marcus diz "ingira", "processe", "adicione ao wiki" ou aponta para um arquivo.

**Fluxo**:

1. **Leia** a fonte (arquivo em `Clippings/`, `RSS articles/`, ou caminho fornecido)
2. **Discuta** brevemente com Marcus: principais insights, o que é relevante para o wiki
3. **Crie** `Knowledge/Summaries/<titulo-kebab>.md` com:
   - Frontmatter completo (type: summary, sources: [caminho da fonte])
   - `## Resumo` — o que a fonte diz (problema, solução, insights-chave)
   - `## Citações Relevantes` — trechos diretos importantes
   - `## Conexões` — lista de `[[WikiPage]]` existentes que este conteúdo toca
   - `## Lacunas / Perguntas` — o que a fonte levanta mas não responde
4. **Atualize** `Knowledge/Concepts/`:
   - Crie páginas novas para entidades relevantes mencionadas
   - Atualize páginas existentes com nova informação da fonte
5. **Verifique** `Knowledge/Decisions/`:
   - Esta fonte contradiz alguma decisão existente? → atualizar ou criar `Pending`
   - Reforça alguma decisão? → adicionar referência
6. **Sinalize contradições** → criar nota em `Knowledge/Pending/conflito-<data>.md`
7. **Atualize** `index.md`:
   - Adicione a fonte na seção "Fontes Ingeridas"
   - Adicione páginas novas criadas em suas categorias
8. **Append** em `log.md`:
   ```
   ## [YYYY-MM-DD] ingest | Título da Fonte
   Criado: Knowledge/Summaries/titulo-kebab.md
   Páginas atualizadas: [[Conceito1]], [[Conceito2]]
   Páginas criadas: [[NovoConceito]]
   ```

Uma ingestão típica toca 5–15 arquivos do wiki. Isso é normal e desejável.

---

## Operação 2 — Query

**Gatilho**: Marcus faz uma pergunta sobre o domínio do wiki.

**Fluxo**:

1. **Leia** `index.md` para identificar páginas relevantes para a pergunta
2. **Leia** as páginas identificadas em `Knowledge/`
3. **Sintetize** a resposta com referências `[[WikiPage]]` e citações de sources
4. **Pergunte** Marcus: "Quer que eu salve esta análise como página de síntese?"
5. Se sim → crie `Knowledge/Synthesis/<topico-kebab>.md` e adicione ao `index.md`
6. **Append** em `log.md`:
   ```
   ## [YYYY-MM-DD] query | Resumo da pergunta
   Páginas consultadas: [[P1]], [[P2]]
   Síntese salva: sim/não
   ```

---

## Operação 3 — Lint (Saúde do Wiki)

**Gatilho**: Marcus diz "verifique o wiki", "lint", "saúde do wiki".

**Fluxo**:

1. Leia `index.md` para ter o inventário completo
2. Amostre páginas de `Knowledge/` para verificar:
   - Páginas órfãs (listadas no índice mas sem links de entrada)
   - Conceitos mencionados em texto mas sem página própria
   - Contradições entre páginas
   - Claims que fontes mais recentes possam ter superado
   - Cross-references ausentes óbvias
3. Produza relatório com:
   - Problemas encontrados (ordenados por severidade)
   - Novas fontes a investigar
   - Páginas a criar
4. Crie `Knowledge/Pending/lint-YYYY-MM-DD.md` com o relatório completo
5. **Append** em `log.md`:
   ```
   ## [YYYY-MM-DD] lint
   Orphans: N. Conceitos sem página: X. Contradições: Y.
   Relatório: Knowledge/Pending/lint-YYYY-MM-DD.md
   ```

---

## Convenções de Linking

- Use `[[NomeDaPagina]]` para links internos (formato Obsidian wikilink)
- Nomes de página de conceitos: PascalCase → `[[AgentMemory]]`, `[[LangGraph]]`
- Nomes de arquivo: kebab-case → `agent-memory.md`, `lang-graph.md`
- Link **liberalmente** — toda menção de conceito relevante deve virar um link
- Links são o que torna o wiki valioso: cross-references já feitos = conhecimento compilado

---

## Formatos de Output Alternativos

Dependendo da query, o output pode ser:

| Formato | Quando usar |
|---------|------------|
| Página markdown | Padrão — qualquer síntese ou análise |
| Tabela de comparação | "Compare X e Y", "Diferenças entre A e B" |
| Marp slides (`marp: true` no frontmatter) | Apresentações, quando Marcus pedir |
| Script Python/matplotlib | Visualizações de dados do wiki |

Todo output gerado por query pode (e deve) ser salvo como página de síntese quando tiver valor duradouro.

---

## Regras Operacionais

1. **Leia `index.md` antes de qualquer operação** — para saber o que já existe
2. **Prefira atualizar páginas existentes** a criar duplicatas
3. **Nunca edite entradas antigas do `log.md`** — apenas append
4. **Fontes em `Clippings/` são imutáveis** — nunca modifique, mova ou delete
5. **Conflitos vão para `Knowledge/Pending/`** — Marcus decide, não o Claude
6. **Git commit** após cada ingestão completa (o plugin obsidian-git cuida do auto-commit)
7. **`log.md` é grep-friendly** — cada entrada começa com `## [YYYY-MM-DD]`

---

## Como Navegar o Wiki

```bash
# Ver as últimas 10 operações
grep "^## \[" log.md | tail -10

# Buscar por conceito
grep -r "AgentMemory" Knowledge/

# Ver páginas por tipo
grep -r "^type: concept" Knowledge/ -l
```

Consulte também `Constitution/README.md` para as regras de governança do ecossistema multi-agente.
