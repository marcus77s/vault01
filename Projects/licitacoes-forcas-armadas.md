---
type: project
status: current
created: 2026-06-07
updated: 2026-06-07
tags: [licitacoes, rag, chromadb, anthropic, pncp, forcass-armadas, direito-administrativo, llm-agent]
sources: 
  - https://pncp.gov.br/pncp-api/v1
  - https://compras.gov.br
  - Lei 14.133/2021 (Nova Lei de Licitações)
  - Lei 8.666/1993 (Lei Antiga)
importance: high
agent: Hermes
paths:
  code: /home/marcus/editais_forcas/
  knowledge_base: /home/marcus/editais_forcas/txt/
  lightrag: /home/marcus/projeto_licitacoes/lightrag/
---

# Projeto: RAG Híbrido para Editais das Forças Armadas

## Objetivo

Construir um sistema de geração automática de editais militares (FAB, Marinha, Exército) usando **RAG Híbrido** — combinando:

1. **Conhecimento local** (ChromaDB com 1800+ TXTs de editais e legislação)
2. **Consulta em tempo real** à API do PNCP (Portal Nacional de Contratações Públicas)
3. **Geração via LLM** (Anthropic Claude)

O objetivo final é produzir editais que **passem em auditorias** — com aderência total à Lei 14.133/2021, Lei 8.666/1993 e jurisprudência do TCU.

## Stack

| Componente | Tecnologia |
|---|---|
| **Vector DB local** | ChromaDB |
| **Embeddings** | `sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2` |
| **API online** | PNCP.gov.br (REST) |
| **LLM gerador** | Anthropic Claude |
| **Corpus** | 1800+ TXTs (editais, contratos, avisos, legislação) |
| **Knowledge graph** | LightRAG v1.5.0 (NVIDIA API backend) |
| **Análise de código** | graphify (qwen2.5-coder:7b via Ollama) |

## Arquitetura (3 Módulos)

```
┌─────────────────────────────────────────────┐
│            SistemaHibrido (orquestrador)      │
└──────────────┬──────────────────────────────┘
               │
   ┌───────────┼───────────┐
   ▼           ▼           ▼
IndiceLocal  ApiPNCP   GeradorEdital
(ChromaDB)   (REST)    (Anthropic)
   │           │           │
   │  1800+    │  tempo    │  Claude
   │  TXTs     │  real     │  gera edital
   ▼           ▼           ▼
Busca        Busca       Texto
similar      PNCP        final
```

## Forças Armadas Cobertas

| Força | CNPJ |
|---|---|
| **FAB** (Força Aérea Brasileira) | 00394429000100 |
| **Marinha do Brasil** | 00394502000144 |
| **Exército Brasileiro** | 00394452000103 |

## Corpus

```
/home/marcus/editais_forcas/txt/
├── EDITAL_*.txt       # Editais de pregão, concorrência, dispensa
├── CONTRATO_*.txt     # Contratos já celebrados
├── AVISO_*.txt        # Avisos de licitação
└── legislacao/txt/
    ├── Lei_14.133.txt        # Nova Lei de Licitações (2021)
    ├── Lei_8.666.txt         # Lei Antiga (1993, ainda aplicável)
    └── Decretos_*.txt        # Regulamentação
```

## Modos de Operação

- **Modo A (Local)** — só ChromaDB, sem rede
- **Modo B (Online)** — só API PNCP
- **Modo C (Híbrido)** — combina A+B para melhor recall

## Estado Atual

- ✅ **RAG híbrido funcional** (`rag_hibrido.py` — 19KB)
- ✅ **ChromaDB populado** com 1800+ documentos
- ✅ **API PNCP integrada** (busca em tempo real)
- ✅ **LightRAG configurado** em `/home/marcus/projeto_licitacoes/lightrag/`
  - LLM: `meta/llama-3.2-90b-vision-instruct` (NVIDIA)
  - Embedding: `nvidia/nv-embed-v1` (4096 dims)
  - Porta: 9621
- ✅ **Graphify analisado** — 24 nós, 34 arestas, 4 comunidades
  - God nodes: `ApiPNCP`, `SistemaHibrido`, `IndiceLocal`, `GeradorEdital`
- ⏳ **Extração semântica completa** (1800 TXTs) pendente
  - Precisa de API cloud (Gemini, Anthropic ou OpenAI real)
  - Ollama 7B não aguenta textos jurídicos PT-BR em JSON estruturado
- ⏳ **Testes de auditoria** nos editais gerados

## Próximos Passos

1. [ ] Rodar extração graphify completa com API cloud (Gemini free tier)
2. [ ] Validar editais gerados contra checklist do TCU
3. [ ] Adicionar memória de longo prazo via LightRAG
4. [ ] Interface web simples (Streamlit) pra operadores
5. [ ] Teste A/B: edital gerado vs edital humano
6. [ ] Integrar com sistema de tramitação (SEI?)

## Decisões de Arquitetura

| Decisão | Motivo |
|---|---|
| ChromaDB em vez de FAISS | Persistência nativa + metadata filter |
| Sentence-transformers multilingual | Documentos em PT-BR |
| Anthropic Claude em vez de GPT | Melhor em texto jurídico/longo |
| PNCP em tempo real | Editais recentes, jurisprudência atual |
| LightRAG + ChromaDB | Graph RAG pega relações entre leis; vector pega similaridade semântica |

## Conhecimentos Relacionados

- [[Fontes-Oficiais-Licitacoes]] — PNCP, Compras.gov.br
- [[LightRAG-NVIDIA-Setup]] — configuração do LightRAG com NVIDIA API
- [[Constituicao]] — princípios da administração pública
- [[Lei-14133]] — nova lei de licitações
- [[Lei-8666]] — lei antiga (transição)

## Referências

- [[HermesAgent]] — orquestrador de agentes
- [[LLMWiki]] — padrão de memória
- [[RAG]] — conceito geral de Retrieval-Augmented Generation
- [[HybridRAG]] — combinar vector + API em tempo real
