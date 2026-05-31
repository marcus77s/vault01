---
type: journal
created: 2026-05-31
updated: 2026-05-31
tags: [instalações, infraestrutura, ferramentas]
importance: medium
agent: claude
---

# Registro de Instalações — PC Local Marcus

Log de softwares instalados no PC de Marcus com detalhes técnicos para referência futura.
Append-only: novas instalações sempre adicionadas ao final.

---

## [2026-05-31] n8n — Plataforma de Automação de Workflows

### O que é
n8n é uma plataforma de automação de workflows open-source (self-hosted), similar ao Zapier/Make.com mas rodando localmente. Permite conectar APIs, serviços e criar automações com interface visual.

### Instalação

| Item | Detalhe |
|------|---------|
| Versão instalada | 2.22.5 |
| Método | `npm install -g n8n` |
| Node.js | v24.16.0 (via nvm) |
| Gerenciador de processos | pm2 |
| Porta | 5678 |
| URL local | http://localhost:5678 |
| Data | 2026-05-31 |

### Comandos úteis

```bash
# Verificar status
pm2 status

# Ver logs
pm2 logs n8n

# Reiniciar
pm2 restart n8n

# Parar
pm2 stop n8n

# Iniciar (se parado)
pm2 start n8n
```

### Auto-start no boot
Para ativar auto-start (rodar uma vez):
```bash
sudo env PATH=$PATH:/home/marcus/.nvm/versions/node/v24.16.0/bin /home/marcus/.nvm/versions/node/v24.16.0/lib/node_modules/pm2/bin/pm2 startup systemd -u marcus --hp /home/marcus
```
Depois do comando acima, rodar `pm2 save` para salvar lista de processos.

### Arquivos de dados
- Banco de dados: `~/.n8n/database.sqlite`
- Configuração: `~/.n8n/`
- Logs pm2: `~/.pm2/logs/n8n-out.log` e `~/.pm2/logs/n8n-error.log`

### Contexto
Instalado pois o usuário tentou usar via `npx` (que ficou apenas no cache) e não conseguia abrir. Resolvido instalando globalmente via npm e configurando pm2 como gerenciador de processos para persistência.

### Relacionado
- [[Knowledge/Concepts/HermesAgent]] — outro agente de automação self-hosted
- [[Knowledge/Concepts/CronJobs]] — alternativa para tarefas agendadas

---

<!-- Novas instalações abaixo desta linha -->
