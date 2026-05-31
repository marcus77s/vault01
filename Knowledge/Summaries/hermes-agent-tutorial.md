---
type: summary
status: current
created: 2026-05-30
updated: 2026-05-30
tags: [hermes-agent, tutorial, vps, telegram, openrouter, skills, cron]
sources: [raw/Hermes Agent Tutorial for Beginners - Step by Step-PT.md]
importance: medium
agent: claude
---

# Hermes Agent — Tutorial Passo a Passo

**Fonte:** Tutorial em vídeo (Metics Media) — traduzido para PT

## Resumo

Guia completo de instalação e configuração do [[HermesAgent]] em VPS (Hostinger KVM2), incluindo integração com Telegram, seleção de modelo via [[OpenRouter]], sistema de [[AgentSkills]] e [[CronJobs]].

**Stack:** Hermes Agent (Nous Research) + Docker + Hostinger VPS + Telegram Bot + OpenRouter

**Fluxo de instalação:**
1. Deploy automático via Hostinger (plano KVM2 — 2 vCPU, 8GB RAM, Docker pré-configurado)
2. Terminal web → `hermes setup` (wizard de configuração)
3. Escolha de provedor: [[OpenRouter]] (acesso a múltiplos modelos com uma conta)
4. Criação de bot Telegram via BotFather + restrição por user ID
5. `hermes gateway run` → agente escuta mensagens do Telegram em background

**Modelo recomendado para iniciantes:** DeepSeek-V4 (~$0.43/M tokens entrada). Evitar: GPT-5.4 mini (ruim em tool calls), Qwen3.x com thinking tags (tende a não usar ferramentas).

**Sistema de habilidades:** Agente salva workflows como skills reutilizáveis (Python scripts). Skills criadas pelo próprio usuário são seguras por padrão; skills externas são escaneadas antes de instalar.

**Memória persistente:** Agente salva preferências e contexto do usuário entre conversas. Quanto mais uso, mais contexto acumulado.

**Cron jobs:** Agendamento em linguagem natural ("toda segunda às 9h, execute X"). Resultado enviado via Telegram. Sem necessidade de código ou sintaxe cron manual.

**Monitoramento de custos:** OpenRouter Activity page (por chave de API) + Hostinger Billing.

## Citações Relevantes

> "É como ter uma versão pessoal do ChatGPT que vive em seu próprio servidor, conversa com você por meio de aplicativos de bate-papo que você já usa e melhora quanto mais você o usa."

> "Quanto mais tempo você tiver o Hermes, mais ele acumula, mais contexto, mais conhecimento e menos você precisa se repetir."

> "Qualquer coisa que você possa descrever em uma frase, o agente pode agendar."

## Conexões

- [[HermesAgent]] — o sistema descrito neste tutorial
- [[OpenRouter]] — provedor de IA usado para acessar múltiplos modelos
- [[AgentSkills]] — sistema de habilidades reutilizáveis
- [[AgentMemory]] — memória persistente cross-sessão
- [[CronJobs]] — agendamento de tarefas em linguagem natural
- [[TelegramBot]] — interface de mensagens do agente

## Lacunas / Perguntas

- Como migrar do OpenClaw para o Hermes? (mencionado mas não detalhado)
- Quais são os limites da versão gratuita do OpenRouter?
- Como o sistema de skills lida com conflitos entre skills com nomes similares?
- Segurança: o tutorial menciona restringir por user ID, mas não cobre autenticação mais robusta
