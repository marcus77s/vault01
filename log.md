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
## [2026-05-31] install | copilot-cli | Instalado com sucesso via npm (resolução de dependências com build-essential e python3-pip)

## [2026-06-01] governance | Codex participa do vault
Criado: [[CODEX.md]]
Páginas atualizadas: [[index.md]]
Contexto: Marcus apontou o caminho do vault Obsidian e pediu para o Codex usar o esquema de memória existente.

## [2026-06-01] update | CODEX.md
Alteração: incorporadas regras da Constituição do Vault, estrutura de memória, regras dos agentes e operação de lint. Corrigido frontmatter YAML completo em [[CODEX.md]].

## [2026-06-02] ingest | Composio + Nango: integrando agentes com 900+ ferramentas (Clippings/)
Criado: Knowledge/Summaries/composio-hermes-integracoes.md
Conceitos criados: [[Composio]], [[Nango]]
Conceitos atualizados: [[HermesAgent]] (seção Integrações Externas + ligações), [[AgentSkills]] (seção Skills de Integração + ligação Composio)
Fontes descartadas: VEO 3.1 ULTRA (clickbait), Trump/OVNIs (fora do domínio)
index.md corrigido: removidas 5 entradas inexistentes, adicionadas fontes reais, RSS articles removido (pasta não existe)

## [2026-06-02] install | LightRAG v1.5.0 — RAG com Grafo de Conhecimento
Repositório: https://github.com/hkuds/lightrag
LLM: meta/llama-3.2-90b-vision-instruct via NVIDIA API
Embedding: nvidia/nv-embed-v1 (4096 dims) via NVIDIA API
Binding: OpenAI → https://integrate.api.nvidia.com/v1
Servidor: Uvicorn na porta 9621
Gerenciador: uv (v0.11.16)
Diretório: /home/marcus/projeto_licitacoes/lightrag/
Testes: 17 entidades + 14 relações extraídas, queries hybrid e naive funcionando
Páginas criadas: [[Knowledge/LightRAG-NVIDIA-Setup]]
Páginas atualizadas: [[index.md]]

## [2026-06-03] fix | Áudio sumiu após cabo de fone ser puxado — PipeWire perfil "off"
Causa: WirePlumber salvou perfil da placa ALC897 como "off" após jack detect falhar
Solução: pactl set-card-profile + set-default-sink + set-sink-port (perfil analog-stereo)
Registrado: Journal/instalacoes.md

## [2026-06-03] update | Fix áudio ALC897 — solução real é pro-audio profile
Correção: solução anterior (analog-stereo) não funcionava pois WirePlumber exclui nós com available="no"
Solução real: perfil pro-audio via device.profile.priority.rules em ~/.config/wireplumber/wireplumber.conf.d/
Registro atualizado: Journal/instalacoes.md

## [2026-06-03] learning | NotebookLM MCP — stdio vs HTTP, Playwright session, localização em ~/tools/
Insights: MCP stdio roda como subprocesso (sem porta), depende de sessão Google ativa no browser, dist/index.js precisa rebuild após update
Registrado: Journal/instalacoes.md (seção Aprendizados)

## [2026-06-03] install | NotebookLM MCP v2.0.1 — MCP server para automação do Google NotebookLM
Pacote: @roomi-fields/notebooklm-mcp | Transporte: stdio | Config: ~/.claude/mcp.json
Funcionalidades: Q&A com citações, Studio (áudio/vídeo/infográfico), gestão de notebooks, multi-conta, batch_to_vault
Diretório: /home/marcus/tools/notebooklm-mcp/
Registrado: Journal/instalacoes.md

## [2026-06-04] install | Headroom — Camada de compressão de contexto para LLMs
Versão: 0.22.4 | Método: pip install em virtualenv | Porta proxy: 8787
Componentes instalados: headroom-ai[all] (fastapi, uvicorn, transformers, torch, mcp, etc.)
Páginas criadas: [[Knowledge/Summaries/headroom-installation-tutorial]]
Proxy iniciado: headroom proxy --port 8787 (background)
Teste rápido: headroom wrap echo "teste" → saída comprimida

## [2026-06-05] synthesis | X Scraping com Cookies + twscrape
Criado: Knowledge/Synthesis/x-scraping-com-cookies.md
Conceitos criados: [[Twscrape]], [[XCookieAuth]]
Contexto: tutorial derivado de sessão prática — autenticação testada ao vivo com cookies reais

## [2026-06-06] install | FinceptTerminal v4.0.3
Criado: Knowledge/Concepts/FinceptTerminal.md
Páginas atualizadas: [[Journal/instalacoes]], [[index.md]]
Páginas criadas: [[Knowledge/Concepts/FinceptTerminal]]
