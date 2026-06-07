---
type: index
updated: 2026-06-04status: current
---

# Índice do Wiki — vault01

Índice de navegação do wiki. Claude atualiza este arquivo a cada ingestão.
Leia este arquivo antes de qualquer operação para saber o que já existe.

---

## Fontes Brutas Disponíveis

Arquivos em `Clippings/` aguardando ingestão (pasta `RSS articles/` não existe):

### Clippings
- `VEO 3.1 ULTRA GRÁTIS Como Usar SEM PAGAR + Super Grok Liberado! (ToolWallet).md` — clickbait; tutorial sobre acesso "gratuito" ao VEO 3.1 via extensão suspeita; **não ingerir** (sem valor técnico)
- `FOI AGORA - TRUMP CONFESSOU 'SÃO COISAS DE EXTRATERRESTRES'...` — conteúdo sobre OVNIs/Trump; **não ingerir** (fora do domínio do wiki)

---

## Fontes Ingeridas

### raw/
- [[Knowledge/Summaries/llm-wiki-karpathy]] — Padrão LLM Wiki (Karpathy): wiki persistente mantido por LLM vs RAG; 3 camadas, 3 operações
- [[Knowledge/Summaries/hermes-agent-tutorial]] — Tutorial completo Hermes Agent
- [[Knowledge/LightRAG-NVIDIA-Setup]] — Configuração LightRAG com API NVIDIA
- [[Knowledge/Fontes-Oficiais-Licitacoes]] — PNCP, Compras.gov.br e fontes oficiais de dados de licitações

### Clippings/
- [[Knowledge/Summaries/composio-hermes-integracoes]] — Composio + Nango: integração de agentes com 900+ serviços externos sem gestão manual de OAuth

---

## Páginas do Wiki

### Conceitos (`Knowledge/Concepts/`)

#### Padrões & Arquitetura
- [[Knowledge/Concepts/LLMWiki]] — Wiki persistente mantido por LLM; artefato composto vs RAG
- [[Knowledge/Concepts/RAG]] — Retrieval-Augmented Generation; comparação com LLM Wiki
- [[Knowledge/Concepts/MemexPattern]] — Visão de Vannevar Bush (1945); inspiração histórica do LLM Wiki

#### Agentes & Memória
- [[Knowledge/Concepts/AgentMemory]] — Memória persistente em agentes; formas (interna/externa), dimensões (semântica/episódica/procedural)
- [[Knowledge/Concepts/AgentSkills]] — Sistema de skills do Hermes: workflows salvos como scripts Python reutilizáveis
- [[Knowledge/Concepts/CronJobs]] — Tarefas agendadas em linguagem natural; execução autônoma no VPS

#### Ferramentas
- [[Knowledge/Concepts/HermesAgent]] — Agente open-source Nous Research; self-hosted, memória persistente, skills, cron
- [[Knowledge/Concepts/OpenRouter]] — Agregador de APIs de LLM; acesso a múltiplos modelos com uma conta
- [[Knowledge/Concepts/TelegramBot]] — Interface de mensagens do Hermes; criação via BotFather
- [[Knowledge/Concepts/Composio]] — Plataforma de integração para agentes; conecta a 900+ serviços externos sem gestão manual de OAuth
- [[Knowledge/Concepts/Nango]] — Concorrente do Composio; 800+ integrações; fallback quando Composio não tem uma ferramenta específica
- [[Knowledge/Concepts/Twscrape]] — Biblioteca Python para scraping do X via cookies de sessão; sem API key necessária
- [[Knowledge/Concepts/XCookieAuth]] — Autenticação no X via cookies de navegador (auth_token + ct0 + twid)
- [[Knowledge/Concepts/FinceptTerminal]] — Terminal desktop C++20+Qt6 de análise financeira; 37 agentes IA, 100+ conectores, QuantLib, paper trading

### Decisões (`Knowledge/Decisions/`)

*Nenhuma ainda.*

### Sínteses (`Knowledge/Synthesis/`)

- [[Knowledge/Synthesis/x-scraping-com-cookies]] — Tutorial completo: autenticação no X via cookies + twscrape; todos os métodos da API com exemplos de código

### Resumos de Fontes (`Knowledge/Summaries/`)

- [[Knowledge/Summaries/llm-wiki-karpathy]] — raw/llm-wiki.md (Karpathy, 2026-05-30)
- [[Knowledge/Summaries/hermes-agent-tutorial]] — raw/Hermes Agent Tutorial PT (Metics Media, 2026-05-30)
- [[Knowledge/Summaries/composio-hermes-integracoes]] — Clippings/Composio + Nango (Elber Domingos, 2026-06-01)
- [[Knowledge/Summaries/headroom-installation-tutorial]] — Instalação e tutorial do Headroom (2026-06-04)

---

## Projetos (`Projects/`)

- [[Projects/diretor-de-cinema]] — Agente LLM para direção de cinema: breakdown técnico de cenas (atores, câmeras, iluminação, internas/externas)
- [[Projects/licitacoes-forcas-armadas]] — RAG híbrido (ChromaDB + PNCP + Claude) para gerar editais militares (FAB, Marinha, Exército) que passem em auditorias do TCU

---

## Journal (`Journal/`)

- [[Journal/instalacoes]] — Registro de instalações no PC local: versão, método, comandos úteis, auto-start

---

## Governança

- [[Constitution/README]] — Regras e estrutura do ecossistema multi-agente
- [[Constitution/agent-update-tutorial]] — Tutorial para agentes se atualizarem com o schema de 2026-05-31
- [[CLAUDE.md]] — Schema do LLM Wiki (instruções para Claude)
- [[GEMINI.md]] — Schema do LLM Wiki (instruções para Gemini CLI)
- [[CODEX.md]] — Schema do LLM Wiki (instruções para Codex)

---

## Estatísticas

|| Métrica | Valor |
||---------|-------|
|| Fontes brutas disponíveis (Clippings) | 2 (não ingeridas — fora do domínio) |
|| Fontes ingeridas | 5 |
|| Páginas de conceitos | 14 |
|| Páginas de resumos | 4 |
|| Páginas de síntese | 1 |
|| Decisões | 0 |
| Projetos | 2 |
| Última atualização | 2026-06-07 |
