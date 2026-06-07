---
type: concept
created: 2026-06-06
updated: 2026-06-06
tags: [finanças, terminal, IA, analise-quantitativa, trading, ferramentas]
sources: [https://github.com/Fincept-Corporation/FinceptTerminal]
importance: medium
agent: claude
---

# FinceptTerminal

Terminal desktop nativo para análise financeira profissional. Construído em C++20 com Qt6 e Python embarcado como motor analítico. Roda como binário único sem dependência de navegador.

## O que faz

Plataforma de inteligência financeira que combina análise quantitativa clássica com 37 agentes de IA especializados. Cobre desde precificação de derivativos até monitoramento geopolítico, com 100+ conectores de dados e suporte a trading real.

## Agentes de IA (37)

Personas especializadas incluindo:
- **Trader** — sinais de entrada/saída, gestão de risco intraday
- **Investidor** — análise fundamentalista, DCF, valuation
- **Economista** — macro, dados do FRED/IMF/Banco Mundial
- **Analista Geopolítico** — risco de mercados emergentes

## Capacidades analíticas

| Módulo | Funcionalidades |
|--------|----------------|
| Renda Variável | DCF, P/E, EV/EBITDA, análise técnica |
| Portfolio | Otimização (Markowitz), VaR, Sharpe ratio |
| Derivativos | Precificação Black-Scholes, Greeks |
| Quantlib | 18 módulos: bonds, swaps, opções exóticas |
| Macro | Dados FRED, IMF, World Bank, DBnomics |

## Conectores de dados (100+)

- **Equities**: Yahoo Finance, Polygon
- **Crypto**: Kraken (WebSocket real-time)
- **Macro**: FRED, IMF, World Bank, DBnomics
- **Corretoras (16)**: Alpaca, Zerodha, Angel One e outros
- APIs governamentais diversas

## Workflows visuais

Editor node-based para criar pipelines de automação — conecta fontes de dados, análise e execução de ordens em fluxos visuais.

## Instalação no PC de Marcus

- Versão: 4.0.3
- Data: 2026-06-06
- Launcher: `fincept-terminal` (no PATH via `~/.local/bin/`)
- Detalhes completos: [[Journal/instalacoes]]

## Licença

Dual: AGPL-3.0 (open source) + Licença Comercial proprietária.
Uso comercial (SaaS, consultoria, forks) requer licenciamento pago.

## Relacionado

- [[Knowledge/Concepts/HermesAgent]] — outro agente de automação com análise de dados
- [[Knowledge/Concepts/OpenRouter]] — agregador de LLMs; relevante para os agentes IA internos do Fincept
- [[Journal/instalacoes]] — log de instalação com comandos e solução de dependências
