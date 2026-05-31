# Log do Wiki — vault01

Registro cronológico append-only. Nunca editar entradas antigas.
Formato grep-friendly: cada entrada começa com `## [YYYY-MM-DD]`

---

## [2026-05-30] ingest | LLM Wiki — Padrão Karpathy (raw/llm-wiki.md)
Criado: Knowledge/Summaries/llm-wiki-karpathy.md
Páginas criadas: [[LLMWiki]], [[RAG]], [[MemexPattern]], [[AgentMemory]]
Páginas atualizadas: —
Nota: documento fundador do próprio padrão usado neste vault

## [2026-05-30] ingest | Hermes Agent Tutorial (raw/Hermes Agent Tutorial for Beginners - Step by Step-PT.md)
Criado: Knowledge/Summaries/hermes-agent-tutorial.md
Páginas criadas: [[HermesAgent]], [[OpenRouter]], [[AgentSkills]], [[CronJobs]], [[TelegramBot]]
Páginas atualizadas: [[AgentMemory]] (adicionada referência ao Hermes como implementação)
Nota: arquivo PT traduzido manualmente após falha do app de tradução em 11:36

## [2026-05-30] project | Diretor de Cinema
Criado: Projects/diretor-de-cinema.md
Descrição: Agente LLM local para breakdown técnico de roteiros (atores, câmeras, iluminação, cenas internas/externas)

## [2026-05-30] project | Adopted LLM Wiki memory scheme
Updated [[GEMINI.md]] with rules. Initialized Gemini CLI as agent.
Páginas criadas: [[GEMINI.md]]
Páginas atualizadas: [[index.md]]

## [2026-05-31] install | n8n — Plataforma de Automação de Workflows
Versão: 2.22.5 | Node: v24.16.0 | Gerenciador: pm2 | Porta: 5678
Problema original: instalado via npx (cache temporário), não abria.
Solução: `npm install -g n8n` + pm2 para persistência de processo.
URL: http://localhost:5678
Criado: Journal/instalacoes.md (seção n8n)
Páginas atualizadas: [[index.md]]

## [2026-05-31] governance | Tutorial de atualização de schema para agentes
Criado: Constitution/agent-update-tutorial.md
Contexto: schema atualizado em 2026-05-31 com status field, novos dirs, Operação 4,
correção de nomenclatura. Tutorial guia agentes anteriores a fazer a transição.
