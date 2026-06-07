---
type: summary
status: current
created: 2026-06-04
updated: 2026-06-04
tags: [headroom, installation, tutorial]
sources: []
importance: medium
agent: hermes
---

# Headroom — Instalação e Uso para Redução de Tokens

## Visão Geral
Headroom é uma camada de compressão de contexto para agentes de IA que reduz o número de tokens enviados aos LLMs em 60–95% sem perder a qualidade das respostas. Ele funciona como biblioteca, proxy local ou servidor MCP, suportando múltiplos algoritmos de compressão (SmartCrusher, CodeCompressor, Kompress-base, etc.).

## Stack Table
| Componente | Tecnologia/Versão |
|------------|-------------------|
| Headroom | 0.22.4 |
| Python | 3.12.3 (venv) |
| Dependências principais | fastapi, uvicorn, litellm, transformers, torch, mcp, etc. |
| Modo de uso | Proxy local (porta 8787) ou wrap de comandos |
| Licença | Apache 2.0 |

## Localização
- **Virtualenv**: `/home/marcus/headroom_venv/`
- **Executável**: `/home/marcus/headroom_venv/bin/headroom`
- **Proxy rodando**: `http://localhost:8787` (iniciado em background)
- **Logs de performance**: `~/.headroom/logs/` (vazio até o proxy receber tráfego)

## Arquivo de Configuração
Headroom não requer arquivo de configuração obrigatório para uso básico. Variáveis de ambiente úteis:
- `HEADROOM_CONTEXT_TOOL`: escolher ferramenta de contexto (ex: `lean-ctx`).
- `HEADROOM_WORKSPACE_DIR`, `HEADROOM_CONFIG_DIR`: para modo Docker.

## Comandos de Instalação
```bash
# 1. Criar virtualenv (opcional, mas recomendado)
python3 -m venv ~/headroom_venv
source ~/headroom_venv/bin/activate

# 2. Instalar Headroom com todos os extras
pip install "headroom-ai[all]"
# Se houver conflitos com pacotes do sistema, use --break-system-packages ou prefira pipx

# 3. Verificar instalação
headroom --version
# headroom, version 0.22.4

# 4. Iniciar proxy em background (porta 8787)
source ~/headroom_venv/bin/activate
headroom proxy --port 8787 &
# Ou usar nohup para persistência:
# nohup headroom proxy --port 8787 > ~/headroom_proxy.log 2>&1 &
```

## Exemplos de Uso
### Modo Wrap (compressão sob demanda)
```bash
source ~/headroom_venv/bin/activate
headroom wrap echo "Olá, teste de compressão"
# Saída comprimida (se aplicável)

# Commands mais úteis:
headroom wrap ls -la
headroom wrap git diff
headroom wrap cat arquivo_grande.txt
```

### Modo Proxy (zero código)
Depois de iniciar o proxy, basta apontar seu agente/LLM para `http://localhost:8787` como endpoint OpenAI‑compatible.

Exemplo com curl (simulando chamada ao modelo):
```bash
curl -X POST http://localhost:8787/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
        "model": "nemotron-3-super-120b-a12b",
        "messages": [{"role": "user", "content": "Explique licitações públicas em duas frases."}],
        "temperature": 0.7
      }'
```
O Headroom interceptará, comprimirá o prompt, enviará ao modelo real e devolverá a resposta (também pode comprimir a resposta se configurado).

### Métricas de Performance
Depois de usar o proxy por um tempo, verifique as estatísticas:
```bash
source ~/headroom_venv/bin/activate
headroom perf
```
Mostra taxa de compressão, economia de tokens, latência adicionada, etc.

## Pipeline / Procedimento (Passo a Passo)
1. Preparar ambiente com venv.
2. Instalar Headroom com extras.
3. Iniciar proxy na porta desejada (padrão 8787).
4. Configurar agentes para usar o proxy como endpoint OpenAI.
5. Monitorar logs e métricas com `headroom perf` e `headroom logs`.
6. Ajustar algoritmo de compressão via variáveis de ambiente se necessário (ex: `HEADROOM_COMPRESSOR=smartcrusher`).

## Problemas Resolvidos
| Problema | Solução |
|----------|---------|
| Alto consumo de tokens em prompts longos (logs, arquivos, saída de comandos) | Headroom comprime antes de enviar ao LLM, reduzindo custos e latência. |
| Necessidade de modificar código do agente para integrar compressão | Modo proxy permite uso zero‑basta mudar a URL do endpoint. |
| Instalação em sistemas com Python externamente gerenciado (ex: Pop!_OS) | Utilizar virtualenv ou pipx para evitar conflitos com pacotes do sistema. |
| Falta de métricas de economia | Comandos `headroom perf` e `headroom logs` fornecem feedback em tempo real. |

## Entrada no Log (`log.md`)
Adicionar a seguinte entrada em `/home/marcus/Documentos/vault01/vault01/log.md`:
```
## [2026-06-04] install | Headroom — Camada de compressão de contexto para LLMs
Versão: 0.22.4 | Método: pip install em virtualenv | Porta proxy: 8787
Componentes instalados: headroom-ai[all] (fastapi, uvicorn, transformers, torch, mcp, etc.)
Páginas criadas: [[Knowledge/Summaries/headroom-installation-tutorial]]
Proxy iniciado: headroom proxy --port 8787 (background)
Teste rápido: headroom wrap echo "teste" → saída comprimida
```

## Atualização do Índice (`index.md`)
Depois de criar a nota, atualizar `/home/marcus/Documentos/vault01/vault01/index.md`:
- Adicionar a fonte em “Resumos de Fontes” (`Knowledge/Summaries/headroom-installation-tutorial`).
- Incrementar contadores de resumos e atualizar data de atualização.

## Wikilinks Sugeridos
- [[AgentSkills]] – para ver como headroom pode ser integrado como skill.
- [[CronJobs]] – para agendar rotinas de limpeza de logs do headroom.
- [[HermesAgent]] – pois o próprio Hermes pode se beneficiar do proxy.
- [[LightRAG-NVIDIA-Setup]] – outro exemplo de instalação de IA no mesmo ambiente.

---
*Nota: Este tutorial foi criado automaticamente pelo agente Hermes após a instalação bem‑sucedida do Headroom. Qual agente que for reproduzir este procedimento deve adaptar caminhos e versões conforme seu ambiente.*