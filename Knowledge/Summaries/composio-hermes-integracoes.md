---
type: summary
status: current
created: 2026-06-02
updated: 2026-06-02
tags: [composio, nango, hermes-agent, integracoes, tools]
sources: [Clippings/Conecte agentes com + de 800 ferramentas - Hermes, OpenClaw com Composio.md]
importance: high
agent: claude
---

# Composio + Hermes: Conectando Agentes a 900+ Ferramentas

**Fonte**: vídeo "Conecte agentes com + de 800 ferramentas - Hermes, OpenClaw com Composio" (Elber Domingos / IMPACTUS AI, 2026-06-01)

---

## Resumo

O problema central abordado: conectar agentes como [[HermesAgent]] e OpenClaw a serviços externos (Gmail, Microsoft Teams, Google Drive, Instagram, etc.) exige criar aplicativos OAuth em cada plataforma separadamente — processo complexo e trabalhoso.

A solução apresentada é o [[Composio]], uma plataforma de integração que centraliza esse processo. Com o Composio instalado, o agente mesmo gera o link de autorização, o usuário clica, autoriza e a conexão está pronta — sem tocar em consoles de API ou gerenciar tokens.

**Como funciona na prática com Hermes:**
1. Usuário pede ao Hermes: *"Quero conectar no Microsoft Teams pelo Composio"*
2. Hermes (via skill do Composio) gera o link de autorização automaticamente
3. Usuário clica, autoriza na plataforma (ex: Microsoft)
4. Hermes confirma: "Teams conectado com sucesso"
5. A partir daí, o agente pode enviar mensagens, criar eventos, etc. naquela plataforma

---

## Citações Relevantes

> "Tem mais de 900 ferramentas que você pode conectar sem que você precise entrar no Google Console, ver esse monte de coisa aqui."

> "Procure sempre ferramentas que usem MCPs ou CLI. Elas são as melhores — proporcionam o uso profissional, um uso mais correto que não seja apenas via API."

> "Google Super: uma única conexão tem acesso a e-mail, calendário, tarefas e tudo mais." (do Google Workspace via Composio)

---

## Insights-Chave

- **Abstração de OAuth**: Composio elimina a necessidade de criar apps OAuth manualmente em cada plataforma
- **Tipos de integração**: Tools (ações que o agente executa) e Triggers (webhooks — quando algo acontece na ferramenta, o agente é notificado)
- **Google Super**: atalho que conecta todos os produtos Google (Gmail, Drive, Calendar, Sheets, Analytics) com uma única autorização
- **Nango**: concorrente do Composio com 800+ integrações; tem ferramentas que o Composio não tem (ex: AWS) e vice-versa — pode ser alternativa quando uma integração específica falha
- **Instalação no Hermes**: via skill — o agente roda `composio login -y` e gerencia a autenticação

---

## Conexões

- [[HermesAgent]] — agente que usa o Composio para conectar ferramentas externas
- [[AgentSkills]] — o Composio é instalado como skill no Hermes; cada integração vira uma skill disponível
- [[Composio]] — plataforma de integração (página de conceito)
- [[Nango]] — alternativa/concorrente ao Composio
- [[TelegramBot]] — interface pela qual o usuário instrui o agente a fazer as conexões
- [[OpenRouter]] — não diretamente relacionado, mas o agente que usa Composio ainda precisa de um LLM por trás

---

## Lacunas / Perguntas

- Composio é gratuito ou tem limites no plano free? O vídeo não especifica custos
- O Composio funciona bem com modelos menores (DeepSeek, Qwen) ou requer modelos mais capazes para tool calls?
- Como o Composio lida com rotação de tokens expirados? É automático?
- Triggers do Composio: como configurar no Hermes para que eventos externos disparem ações?
- Nango: quais integrações específicas ele tem que o Composio não tem?
