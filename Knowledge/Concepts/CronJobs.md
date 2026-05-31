---
type: concept
created: 2026-05-30
updated: 2026-05-30
tags: [cron, scheduling, automation, agent]
sources: [raw/Hermes Agent Tutorial for Beginners - Step by Step-PT.md]
importance: medium
agent: claude
---

# CronJobs (Agentes)

Tarefas agendadas executadas autonomamente pelo agente em intervalos definidos, sem intervenção do usuário.

## No contexto do [[HermesAgent]]

- Agendamento em **linguagem natural** via Telegram ("toda segunda às 9h, execute X")
- Executa mesmo com laptop desligado (roda no VPS)
- Resultado enviado via Telegram ao concluir
- Fuso horário configurável e persistido para futuros jobs

## Exemplo de uso

```
Usuário: "Toda segunda às 9h, execute minha skill competitor-watch 
em 3 termos: 'email marketing tutorial', 'WordPress tutorial', 
'SEO tutorial'. Envie resumo no Telegram com as lacunas."

→ Job agendado, confirmação com próximo horário de execução
```

## Teste manual

```
Usuário: "Execute esse job completo agora."
→ Executa imediatamente para validar output antes do agendamento
```

## Casos de uso comuns

- Briefings matinais
- Relatórios semanais de pesquisa/competidores
- Monitoramento de preços ou alertas
- Qualquer tarefa descritível em uma frase + frequência

## Ligações

- [[HermesAgent]] — implementa cron jobs em linguagem natural
- [[AgentSkills]] — skills podem ser usadas como payload de cron jobs
