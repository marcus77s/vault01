---
type: concept
created: 2026-05-30
updated: 2026-05-30
tags: [openrouter, api, llm, models, provider]
sources: [raw/Hermes Agent Tutorial for Beginners - Step by Step-PT.md]
importance: medium
agent: claude
---

# OpenRouter

Plataforma unificada de acesso a múltiplos modelos de IA com uma única conta e fatura. Funciona como proxy/agregador de APIs.

## Função

Permite acessar DeepSeek, Claude, GPT, Qwen e outros modelos via uma única chave de API, sem necessidade de contas separadas em cada provedor.

## Uso com [[HermesAgent]]

- Configurado no `hermes setup` como provedor de IA
- Chave de API gerada em openrouter.ai → API Keys → New Key
- Limite de crédito configurável por chave (proteção de custo)
- Troca de modelo em runtime: `/model` no Telegram

## Modelos notáveis (contexto Hermes)

| Modelo | Uso | Custo aprox. |
|--------|-----|--------------|
| DeepSeek-V4 | Daily driver | $0.43/M in, $0.87/M out |
| Claude Opus 4.7 | Tarefas complexas | Alto |
| GPT-5.4 mini | ⚠️ Evitar (tool calls ruins) | — |
| Qwen3.x + thinking | ⚠️ Evitar (não usa ferramentas) | — |

## Monitoramento

- Activity page: gastos por hora/dia/semana, número de requests, tokens
- Limite por chave: pode definir teto mensal por chave de API

## Ligações

- [[HermesAgent]] — usa OpenRouter como backend de IA
