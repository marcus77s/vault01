# Memory Consolidation — 2025-06-07

## Sessões consolidadas nesta rodada

### 1. Graphify instalado e configurado para Hermes Agent
**Sessão:** `20260607_084503_34288a` (08:45 AM, 199 mensagens)

**Fatos principais:**
- Graphify (https://github.com/safishamsi/graphify) clonado e instalado via `uv tool install graphifyy` (versão 0.8.33, já presente no sistema)
- Skill Graphify instalada para Hermes: `graphify hermes install`
  - Criou `~/.hermes/skills/graphify/`
  - Injetou regras no `/home/marcus/AGENTS.md`
- Regras do AGENTS.md:
  - Para perguntas de codebase, usar `graphify query "<pergunta>"` quando `graphify-out/graph.json` existir
  - Usar `graphify path "<A>" "<B>"` para relações e `graphify explain "<conceito>"` para conceitos focados
  - Após modificar código, rodar `graphify update .` (AST-only, sem custo de API)
  - Se `graphify-out/wiki/index.md` existir, usar para navegação ampla
- Tentativa de criar notebook Colab para extração completa do projeto `editais_forcas` (1800+ TXTs) falhou por problema de tool calling (write_file sem content)

**Aprendizado:** Graphify já vinha instalado via `uv tool`; a skill Hermes adiciona integração nativa. O workflow recomendado: query → path/explain → update após mudanças.

---

### 2. Configuração da API Qwen (Alibaba Cloud Model Studio / 百炼)
**Sessão:** `20260607_065713_9f494a` (06:57 AM, 24 mensagens)

**Fatos principais:**
- Usuário obteve API key do console Model Studio em `ap-southeast-1` (Cingapura): https://modelstudio.console.alibabacloud.com/ap-southeast-1/
- **Base URL para Cingapura:** `https://{WorkspaceId}.ap-southeast-1.maas.aliyuncs.com/compatible-mode/v1`
  - Workspace ID: canto superior direito do console → nome da conta
- **Formato da key:** `sk-xxxxx` (geral) ou `sk-sp-xxxxx` (Coding Plan)
- **CRÍTICO:** Key só aparece **uma única vez** na criação — criptografia irreversível. Não dá pra recuperar depois.
- API 100% compatível com OpenAI Chat Completions
- Modelos principais:
  - `qwen-max` / `qwen-plus` — topo de linha, multimodal
  - `qwen3-7b` / `qwen3-14b` / `qwen3-32b` — série Qwen3 open-weight
  - `qwen-vl-plus` / `qwen-vl-max` — visão (imagem + texto)
  - `qwen2.5-coder-32b-instruct` — especializado em código
  - `qwen-omni-turbo` — áudio + texto + visão
- Uso via OpenAI SDK:
  ```python
  from openai import OpenAI
  client = OpenAI(api_key="***", base_url="https://SEU_WORKSPACE_ID.ap-southeast-1.maas.aliyuncs.com/compatible-mode/v1")
  ```
- Ou via SDK oficial: `pip install dashscope`
- **O usuário NÃO salvou a key inicial** — precisa criar outra no console

**Decisão/ação pendente:** Criar nova API key no console, copiar imediatamente, configurar no `.env` ou Hermes.

---

### 3. Consolidação anterior (cron job)
**Sessão:** `cron_da419e67160d_20260607_074517` (07:45 AM)
- Execução anterior deste mesmo job de consolidação de memória

---

## Resumo de ações recomendadas

1. **Qwen API:** Criar nova key no console Model Studio → copiar → configurar no ambiente
2. **Graphify:** Testar comandos `graphify query/explain/path` em projetos locais; adicionar hook `graphify update .` no workflow de desenvolvimento
3. **Notebook Colab:** Revisitar criação do notebook para extração do projeto `editais_forcas` quando necessário

---

*Consolidado automaticamente pelo job cron de memory-consolidation em 2025-06-07*