---
type: concept
status: current
created: 2026-05-30
updated: 2026-05-30
tags: [agent-skills, skills, workflow, automation]
sources: [raw/Hermes Agent Tutorial for Beginners - Step by Step-PT.md]
importance: medium
agent: claude
---

# AgentSkills

Sistema do [[HermesAgent]] que permite salvar workflows complexos como scripts reutilizáveis (Python), ativados por gatilhos em linguagem natural.

## Como funciona

1. Usuário pede ao agente para executar uma tarefa complexa
2. Agente executa e salva as etapas como skill nomeada
3. Skill fica disponível como comando reutilizável
4. Agente pode acionar a skill em [[CronJobs]] agendados

## Exemplo

```
Usuário: "Salve esse workflow como skill chamada competitor-watch. 
De agora em diante, quando eu te der um termo de pesquisa, 
encontre os 5 principais vídeos do YouTube, salve no arquivo, 
e aponte as lacunas."

→ Skill criada com gatilho: "qualquer termo de pesquisa" 
→ 4 etapas + Python script reutilizável
```

## Segurança

- Skills criadas pelo próprio usuário: seguras por padrão
- Skills de fontes externas: escaneadas pelo Hermes antes de instalar
- Recomendação: instalar apenas skills de fontes confiáveis

## Relação com [[AgentMemory]]

Skills são a **memória procedural** do agente — como ele sabe fazer tarefas repetitivas sem repensar do zero.

## Ligações

- [[HermesAgent]] — sistema que implementa skills
- [[CronJobs]] — skills podem ser agendadas para execução autônoma
- [[AgentMemory]] — skills como memória procedural
