# Composio Integration — Hermes Agent

Data: 2026-06-02

## Configuração

- Nome do MCP server: `composio`
- URL: `https://connect.composio.dev/mcp`
- Autenticação: API key configurada no `config.yaml` do Hermes
- Transporte: HTTP (sem headers adicionais — o OAuth roda automático via Composio)

## Aviso importante

Não adicionar headers de autenticação manualmente. O Composio gerencia o fluxo OAuth automaticamente para cada app conectado.

## Apps suportados

O Composio oferece +1000 integrações. Os apps mais relevantes para este usuário, baseado no uso histórico do Hermes:

- Google Workspace / Gmail
- Notion / Airtable
- WhatsApp / Telegram / Slack
- Planilhas (Google Sheets, Excel)
- Nubank / PicPay
- ComprasGov / APIs governamentais

## Como usar

1. Carregar/recarregar os MCP servers no Hermes:
   ```bash
   hermes mcp reload
   ```
2. Os conectores do Composio aparecem como ferramentas específicas do app conectado, não como tools genéricas.
3. Para conectar um novo app, usar a dashboard do Composio: https://dashboard.composio.dev
4. Docs oficiais: https://docs.composio.dev

## Referências

- Setup page: https://composio.dev/hermes
- Discord do Composio: https://discord.gg/composio
- API pública de apps: https://www.freepublicapis.com/api (579 APIs públicas gratuitas listadas)
