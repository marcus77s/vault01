---
type: concept
status: current
created: 2026-05-30
updated: 2026-05-30
tags: [hermes-agent, nous-research, open-source, agent, vps]
sources: [raw/Hermes Agent Tutorial for Beginners - Step by Step-PT.md]
importance: high
agent: claude
---

# Hermes Agent

Agente de IA de código aberto desenvolvido pela Nous Research. Predecessor/sucessor do OpenClaw com memória mais forte e sistema de habilidades.

## Características

- **Autonomia**: age proativamente (envia mensagens primeiro, executa em cronograma)
- **[[AgentMemory]] persistente**: lembra preferências e contexto do usuário entre conversas
- **[[AgentSkills]]**: salva workflows como scripts Python reutilizáveis
- **[[CronJobs]]**: agendamento em linguagem natural via Telegram
- **Self-hosted**: roda em VPS próprio, dados no servidor do usuário

## Deploy Recomendado

- **VPS**: Hostinger KVM2 (2 vCPU, 8GB RAM, 100GB) — plano mínimo funcional com Docker
- **Container**: Docker (deploy automático via Hostinger, ou manual via `docker compose`)
- **Interface**: [[TelegramBot]] (ou Discord, Slack, WhatsApp)
- **Modelo padrão**: DeepSeek-V4 via [[OpenRouter]] (bom custo-benefício para uso diário)

## Instalação

```bash
hermes setup          # wizard de configuração inicial
hermes gateway run    # inicia listener do Telegram
hermes doctor         # diagnóstico de problemas
```

## Modelos a evitar

- **GPT-5.4 mini** — ruim em tool calls
- **Qwen3.x com thinking tags** — tende a não usar ferramentas

## Segurança

- Restringir acesso por Telegram user ID (configurado no setup)
- Skills externas são escaneadas antes de instalar
- Gateway roda como usuário `hermes` (não root)

## Diferenças do OpenClaw

- Memória mais robusta
- Sistema de habilidades estruturado
- Maior segurança
- Migração: `hermes import openclaw` (comando único)

## Ligações

- [[OpenRouter]] — provedor de modelos de IA
- [[AgentSkills]] — sistema de habilidades reutilizáveis
- [[AgentMemory]] — memória persistente cross-sessão
- [[CronJobs]] — agendamento de tarefas autônomas
- [[TelegramBot]] — interface principal de mensagens
