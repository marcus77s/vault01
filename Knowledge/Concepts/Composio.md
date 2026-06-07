---
type: concept
status: current
created: 2026-06-02
updated: 2026-06-02
tags: [composio, integracoes, tools, agent-tools, oauth]
sources: [Clippings/Conecte agentes com + de 800 ferramentas - Hermes, OpenClaw com Composio.md]
importance: high
agent: claude
---

# Composio

Plataforma de integração de ferramentas para agentes de IA. Permite que agentes como [[HermesAgent]] e OpenClaw se conectem a 900+ serviços externos sem que o desenvolvedor precise gerenciar OAuth, API keys ou consoles de cada plataforma manualmente.

## O que resolve

Conectar um agente a serviços externos normalmente exige:
- Criar um "aplicativo" no console de cada plataforma (Google, Microsoft, Meta, etc.)
- Gerenciar Client ID, Client Secret, redirect URIs
- Lidar com tokens de acesso e refresh tokens

O Composio abstrai tudo isso: o agente gera um link de autorização, o usuário clica e autoriza — o Composio cuida do resto.

## Tipos de integração

| Tipo | Descrição |
|------|-----------|
| **Tools** | Ações que o agente executa na ferramenta (ex: criar evento, enviar e-mail, deletar comentário) |
| **Triggers** | Webhooks — quando algo acontece na ferramenta, notifica o agente (ex: novo contato adicionado) |

## Funcionalidades notáveis

- **Google Super**: conexão única que dá acesso a Gmail, Drive, Calendar, Sheets, Analytics e mais
- **985 Tool Kits** (na data do vídeo): cada toolkit tem múltiplas tools e triggers
- Instalação feita pelo próprio agente via skill + comando `composio login -y`
- Painel web em `composio.dev` para visualizar conexões ativas

## Instalação no Hermes

```
Usuário → Hermes: "Instale o Composio"
Hermes executa: composio login -y
Hermes gera link de autenticação
Usuário autoriza no navegador
→ Composio disponível como skill
```

Após isso, pedir conexões é em linguagem natural:
```
"Quero conectar no Microsoft Teams pelo Composio"
→ Hermes gera link, usuário autoriza, conexão pronta
```

## Alternativa

[[Nango]] — concorrente com 800+ integrações, interface diferente. Usar quando uma integração específica não está disponível no Composio ou quando o Composio apresenta instabilidade.

## Ligações

- [[HermesAgent]] — agente que usa o Composio
- [[AgentSkills]] — Composio é instalado e operado via sistema de skills
- [[Nango]] — alternativa/concorrente
- [[TelegramBot]] — interface pela qual o usuário instrui o agente
