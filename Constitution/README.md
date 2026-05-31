---
type: constitution
created: 2026-05-26
updated: 2026-05-30
tags: [governance, llm-wiki, memory]
sources:
  - ../../tutorial-llm-wiki.md
importance: high
agent: Codex
---

# Constituição do Vault

Este vault opera como uma **LLM Wiki**: uma memória persistente, interligada e
mantida por agentes. Marcus faz a curadoria das fontes e das perguntas; os agentes
leem, sintetizam, conectam e registram o conhecimento trabalhado.

Regra fundamental: `Clippings/` e `RSS articles/` são fontes brutas imutáveis.
Agentes leem essas pastas, mas nunca modificam, movem ou removem seus arquivos.
Conteúdo criado por agente deve ir para `Knowledge/`, `Projects/`, `Journal/`,
`_workspace/` ou `Constitution/`, conforme o papel da nota.

## Estrutura de Pastas

| Pasta | Tipo de memória | Regra |
|-------|-----------------|-------|
| `/Clippings/` | Fonte bruta | Imutável. Web clips e documentos de entrada. |
| `/RSS articles/` | Fonte bruta | Imutável. Artigos vindos de RSS. |
| `/Knowledge/Summaries/` | Ingestão | Um resumo por fonte ingerida. |
| `/Knowledge/Concepts/` | Semântica | Uma ideia, entidade ou conceito por arquivo. |
| `/Knowledge/Decisions/` | Raciocínio | Decisões, trade-offs e justificativas. |
| `/Knowledge/Synthesis/` | Síntese | Análises temáticas multi-fonte. |
| `/Knowledge/Pending/` | Human-in-loop | Conflitos, dúvidas e lint aguardando Marcus. |
| `/Projects/` | Projetos ativos | Estado atual de cada projeto. |
| `/Journal/` | Episódica | Uma nota por dia ou registro append-only. |
| `/_workspace/active/` | RAM | Rascunhos de agentes em execução. Temporário. |
| `/_workspace/archive/` | RAM arquivada | Tarefas concluídas aguardando processamento. |
| `/Constitution/` | Governança | Leis e convenções do ecossistema. |
| `/index.md` | Mapa do wiki | Inventário navegável; ler antes de operar. |
| `/log.md` | Histórico | Append-only; cada entrada começa com `## [YYYY-MM-DD]`. |

## Regras dos Agentes

1. Ler `index.md` antes de qualquer operação no wiki.
2. Preferir atualizar páginas existentes a criar duplicatas.
3. Usar `Knowledge/Summaries/` para ingestões, `Concepts/` para fatos atômicos, `Decisions/` para raciocínio e `Synthesis/` para análises amplas.
4. Criar notas em `Knowledge/Pending/` quando houver conflito, contradição ou decisão que dependa de Marcus.
5. Nunca editar entradas antigas de `log.md`; apenas anexar novas entradas.
6. Manter `Journal/` append-only.
7. Usar wikilinks `[[NomeDaPagina]]` liberalmente para conceitos relevantes.
8. Usar nomes de conceitos em PascalCase e arquivos em kebab-case.
9. Todo arquivo criado por agente deve ter frontmatter YAML completo.
10. Fazer commit após tarefa crítica quando o fluxo de Git estiver disponível.

## Frontmatter Padrão

```yaml
---
type: summary | concept | decision | synthesis | project | journal | pending
status: current | stub | outdated
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: []
sources: []        # caminhos relativos ao vault
importance: low | medium | high
agent: nome-do-agente
---
```

`updated` deve ser mantido atual — atualize sempre que editar qualquer campo ou seção.
`status: stub` para páginas incompletas; `status: outdated` para conteúdo superado.

## Operações Canônicas

### Ingestão

Gatilhos: Marcus diz "ingira", "processe", "adicione ao wiki" ou aponta para uma
fonte.

Fluxo: ler a fonte, discutir brevemente os insights, criar um resumo em
`Knowledge/Summaries/`, atualizar conceitos e decisões, criar pendências se houver
contradição, atualizar `index.md` e anexar entrada em `log.md`.

### Query

Gatilho: Marcus faz uma pergunta sobre o domínio do wiki.

Fluxo: ler `index.md`, consultar páginas relevantes em `Knowledge/`, sintetizar a
resposta com wikilinks e fontes, perguntar se Marcus quer salvar como síntese e
anexar entrada em `log.md`.

### Lint

Gatilhos: "verifique o wiki", "lint" ou "saúde do wiki".

Fluxo: ler `index.md`, procurar órfãos, conceitos sem página, contradições, claims
superados e cross-references ausentes; salvar relatório em `Knowledge/Pending/` e
anexar entrada em `log.md`.
