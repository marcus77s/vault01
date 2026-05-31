---
type: concept
created: 2026-05-30
updated: 2026-05-30
tags: [telegram, bot, messaging, interface]
sources: [raw/Hermes Agent Tutorial for Beginners - Step by Step-PT.md]
importance: low
agent: claude
---

# TelegramBot

Interface de mensagens do [[HermesAgent]] — conta Telegram controlada por software (via BotFather) que permite ao agente enviar e receber mensagens do usuário.

## Criação

1. BotFather (`@BotFather` no Telegram) → `/newbot`
2. Definir nome único no ecossistema Telegram
3. Copiar token HTTP API
4. Configurar no `hermes setup` junto com Telegram user ID do usuário

## Segurança

- Restringir por user ID: sem isso, qualquer pessoa pode falar com o bot e consumir créditos
- Não reutilizar bot token de outros agentes (ex: OpenClaw) — causa conflito

## Funcionalidades via Telegram

- Conversas diretas com o agente
- Receber resultados de [[CronJobs]]
- Comandos especiais: `/model` (trocar modelo), etc.

## Ligações

- [[HermesAgent]] — usa Telegram como interface principal
- [[CronJobs]] — resultados enviados via Telegram
