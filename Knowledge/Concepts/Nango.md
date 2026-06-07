---
type: concept
status: stub
created: 2026-06-02
updated: 2026-06-02
tags: [nango, integracoes, tools, agent-tools, oauth]
sources: [Clippings/Conecte agentes com + de 800 ferramentas - Hermes, OpenClaw com Composio.md]
importance: low
agent: claude
---

# Nango

Plataforma de integração de ferramentas para agentes de IA. Concorrente do [[Composio]] com 800+ integrações. Funciona de forma similar: abstrai o gerenciamento de OAuth e API keys, permitindo que agentes como [[HermesAgent]] se conectem a serviços externos.

## Diferenças em relação ao Composio

| Aspecto | Composio | Nango |
|---------|----------|-------|
| Integrações | ~985 | ~800+ |
| Visualização de tools | Clara por toolkit | Menos legível na UI |
| Ferramentas únicas | Google Super | AWS (não disponível no Composio) |

## Quando usar

- Como fallback quando o Composio apresenta instabilidade em uma integração específica
- Quando a ferramenta desejada está em Nango mas não no Composio (ex: AWS)

## Ligações

- [[Composio]] — alternativa principal; geralmente preferida pela UI mais clara
- [[HermesAgent]] — agente que pode usar o Nango
- [[AgentSkills]] — instalação via sistema de skills (similar ao Composio)
