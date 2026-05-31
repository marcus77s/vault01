---
type: project
created: 2026-05-30
updated: 2026-05-30
tags: [cinema, filmagem, llm-agent, automacao, roteiro]
sources: []
importance: high
agent: Codex
---

# Projeto: Agente LLM para Direção de Cinema

## Objetivo

Criar um agente de IA (LLM + automação local) que analise roteiros de cinema e produza
um breakdown técnico completo de cada cena, incluindo:

- Quantos artistas/atores por cena
- Ângulo de câmera
- Tipo de iluminação
- Quantidade de câmeras
- Figurantes e quantos
- Se a cena é interna ou externa
- Qual cena (identificação/número)
- Demais parâmetros de produção

## Stack Prevista

- LLM local (Ollama + modelo de código aberto)
- Agente orquestrador (Python) para interpretar roteiro e extrair metadados
- Formato de entrada: roteiro (.txt, .fountain, .pdf)
- Formato de saída: tabela/template de produção (CSV, JSON, markdown)

## Funcionalidades Planejadas

1. **Parser de Roteiro** — extrair cenas, personagens, diálogos
2. **Análise por Cena** — classificar internas/externas, dia/noite, elenco
3. **Sugestão de Enquadramento** — ângulos, lentes, cobertura de câmeras
4. **Folha de Chamada** — quantos atores, figurantes, equipamentos por dia
5. **Integração com Planilha de Produção** — exportar para formato usado por produtoras

## Estado Atual

Ideia inicial. Nada implementado ainda.

## Próximos Passos

1. Definir formato de roteiro suportado (Fountain? PDF parse?)
2. Escolher modelo LLM local (Llama, Mistral, Qwen)
3. Criar protótipo do parser de cenas
4. Testar com roteiro curto (curta-metragem)
5. Validar saída com profissional de produção

## Referências

- [[HermesAgent]] — possível inspiração para arquitetura de agente
- [[LLMWiki]] — padrão de memória persistente do projeto
- [[AgentSkills]] — sistema de skills reutilizáveis
