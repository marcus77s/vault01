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

## [2026-06-03] Fix de Áudio — PipeWire/WirePlumber sem detectar placa de som

### Problema
Após cabo de fone de ouvido ser esticado/puxado, o áudio sumiu. Após reiniciar o PC não voltou.

### Diagnóstico

| Sintoma | Causa raiz |
|---------|------------|
| `pactl list sinks short` mostrava apenas `auto_null` | WirePlumber não criava sinks para a placa |
| Destino padrão: `auto_null` | Perfil da placa em "off" + jack detect retornando `available=no` |
| `wpctl get-volume @DEFAULT_AUDIO_SINK@` retornava `-1` | WirePlumber exclui nós sem routes disponíveis (`lutils.haveAvailableRoutes` retorna false) |
| Portas `analog-output-lineout` e `analog-output-headphones` "não disponível" | Jack detect falhou após hot-plug event (cabo puxado) |

**Placa de som**: Realtek ALC897 (`alsa_card.pci-0000_09_00.4`, HD-Audio Generic via AMD Matisse)  
**Stack de áudio**: PipeWire 1.5.85 + WirePlumber 0.5.12 + PulseAudio compat (Pop!_OS)

### Por que aconteceu (causa técnica completa)
O WirePlumber 0.5 usa `lutils.haveAvailableRoutes()` ao montar a lista de nós disponíveis
para seleção de default. Quando todos os routes de um dispositivo têm `available="no"` (jack
detect falhou), o nó é **excluído completamente** — não vira default, mesmo que exista.

O perfil `output:analog-stereo` retorna `available="no"` porque o ALC897 usa jack detection
baseada em evento HDA pin-sense. Após um hot-plug event (cabo puxado violentamente), o estado
do pino fica inconsistente e o detector reporta "desconectado" mesmo com o fone plugado.

### Solução permanente (já aplicada)

Arquivo criado: `~/.config/wireplumber/wireplumber.conf.d/50-alc897-force-analog.conf`

```conf
# Força perfil pro-audio — não tem routes com jack detect, sempre disponível
device.profile.priority.rules = [
  {
    matches = [{ device.name = "alsa_card.pci-0000_09_00.4" }]
    actions = {
      update-props = {
        priorities = ["pro-audio"]
      }
    }
  }
]
```

O perfil `pro-audio` expõe os pinos ALSA diretos sem lógica de jack detect, então sempre
fica marcado como disponível. O WirePlumber o seleciona como default normalmente.

### Se o áudio sumir novamente (antes do reboot)

```bash
# Forçar perfil pro-audio na sessão atual
pactl set-card-profile alsa_card.pci-0000_09_00.4 pro-audio
```

### Verificação
```bash
wpctl status           # deve mostrar * no sink do ALC897
wpctl get-volume @DEFAULT_AUDIO_SINK@   # deve retornar Volume: X.XX
pw-play /usr/share/sounds/alsa/Front_Center.wav   # deve tocar
```

---

## [2026-06-03] NotebookLM MCP — Automação do Google NotebookLM via MCP

### O que é
MCP server que automatiza o Google NotebookLM localmente. Permite Q&A com citações, geração de Studio (áudio, vídeo, infográfico, relatório, apresentação, tabela de dados), gerenciamento de notebooks e fontes, rotação multi-conta com auto-reautenticação, e `batch_to_vault` para cache offline de respostas. Roda um navegador real (Playwright) contra a conta Google do usuário.

### Instalação

| Item | Detalhe |
|------|---------|
| Pacote | `@roomi-fields/notebooklm-mcp` |
| Versão | 2.0.1 |
| Método | Clonado/instalado em `/home/marcus/tools/notebooklm-mcp/` |
| Entry point | `/home/marcus/tools/notebooklm-mcp/dist/index.js` |
| Transporte | stdio (MCP padrão) |
| Config | `~/.claude/mcp.json` — chave `"notebooklm"` |
| Porta | N/A (stdio) — REST API local opcional disponível |
| Data | 2026-06-03 |

### Configuração (`~/.claude/mcp.json`)
```json
{
  "mcpServers": {
    "notebooklm": {
      "command": "node",
      "args": ["/home/marcus/tools/notebooklm-mcp/dist/index.js"]
    }
  }
}
```

### Comandos úteis
```bash
# Verificar se o MCP está carregado no Claude Code
# (aparece como "notebooklm" na lista de MCPs disponíveis)

# Rodar o servidor manualmente para teste
node /home/marcus/tools/notebooklm-mcp/dist/index.js

# Diretório do projeto
cd /home/marcus/tools/notebooklm-mcp/
```

### Contexto
Instalado para automatizar interações com o Google NotebookLM — especialmente útil para Q&A com citações a partir de notebooks existentes e geração de conteúdo Studio (áudio overview, etc.) diretamente via Claude Code.

### Relacionado
- [[Knowledge/Concepts/RAG]] — NotebookLM usa RAG internamente com citações
- [[Journal/instalacoes]] — n8n e LightRAG também instalados no mesmo PC

### Aprendizados

**Arquitetura do MCP (insights técnicos):**
- MCPs com `stdio` não abrem porta — rodam como subprocesso do cliente (Claude Code). Diferente do n8n/LightRAG que ficam em portas persistentes.
- O NotebookLM MCP usa Playwright para controlar um navegador real, não uma API pública. Isso significa que depende da sessão Google ativa no navegador — não é stateless.
- A configuração fica em `~/.claude/mcp.json` (global para Claude Code), não em settings do projeto. Qualquer projeto que abrir o Claude Code vai ter acesso ao MCP.

**Padrão de localização:**
- Ferramenta instalada em `~/tools/<nome>/` em vez de instalar globalmente via npm. Isso facilita updates manuais (git pull + rebuild) e evita conflitos de versão com outros pacotes globais.
- O `dist/index.js` é o ponto de entrada compilado — se houver update, precisa rodar `npm run build` antes de usar a nova versão.

**O que fazer diferente:**
- Verificar se a autenticação Google foi feita antes de usar o MCP (o servidor pode travar aguardando login no browser se a sessão expirar).
- Considerar anotar qual conta Google está associada, se houver mais de uma configurada.

---

<!-- Novas instalações abaixo desta linha -->

## [2026-06-06] FinceptTerminal v4.0.3 — Terminal de Análise Financeira com IA

### O que é
Terminal desktop nativo (C++20 + Qt6) de análise financeira profissional. Inclui 37 agentes de IA cobrindo personas de trader/investidor, análise econômica e geopolítica. Sem dependência de navegador — binário único.

### Instalação

| Item | Detalhe |
|------|---------|
| Versão instalada | 4.0.3 |
| Método | AppImage extraída manualmente (FUSE indisponível no ambiente) |
| Binário original | `/home/marcus/tools/fincept/FinceptTerminal-4.0.3-linux-x64-setup.run` |
| App extraída | `/home/marcus/tools/fincept/squashfs-root/` |
| Launcher | `/home/marcus/.local/bin/fincept-terminal` |
| Desktop entry | `~/.local/share/applications/fincept-terminal.desktop` |
| Ícone | `~/.local/share/icons/hicolor/256x256/apps/fincept-terminal.png` |
| Data | 2026-06-06 |

### Como abrir

```bash
# Via terminal
fincept-terminal

# Ou pelo menu de aplicações do desktop (entrada "Fincept Terminal")
```

### Dependência resolvida manualmente
`libOpenGL.so.0` não estava instalada no sistema e sudo não estava disponível.
Solução: baixado `libopengl0_1.7.0-1build1_amd64.deb` via `apt-get download` e
extraído o `.so` diretamente para `/home/marcus/tools/fincept/squashfs-root/usr/lib/`.
O launcher (`~/.local/bin/fincept-terminal`) já seta `LD_LIBRARY_PATH` corretamente.

> Se quiser instalar o `.so` de forma limpa no sistema no futuro: `sudo apt install libopengl0`

### Funcionalidades principais
- DCF, otimização de portfólio, VaR, Sharpe ratio, precificação de derivativos
- 37 agentes de IA: trader, investidor, análise econômica, geopolítica
- 100+ conectores de dados: Yahoo Finance, FRED, IMF, Banco Mundial, Polygon, Kraken, DBnomics
- Trading real-time: WebSocket crypto, paper trading, 16 corretoras (Alpaca, Zerodha, etc.)
- Suite QuantLib: 18 módulos quantitativos
- Editor visual de workflows (node-based)

### Relacionado
- [[Knowledge/Concepts/FinceptTerminal]] — página de conceito
- [[Journal/instalacoes]] — outras ferramentas instaladas no mesmo PC
