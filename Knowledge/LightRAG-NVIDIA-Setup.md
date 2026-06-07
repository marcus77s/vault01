---
tags:
  - lightrag
  - nvidia
  - rag
  - setup
created: 2026-06-02
---

# LightRAG + NVIDIA API — Configuração Completa

## Visão Geral

LightRAG (v1.5.0) configurado com API da NVIDIA via endpoint compatível com OpenAI. Usa `meta/llama-3.2-90b-vision-instruct` como LLM e `nvidia/nv-embed-v1` para embeddings.

## Stack

| Componente | Tecnologia |
|---|---|
| Framework | [[LightRAG]] v1.5.0 (HKU) |
| LLM | `meta/llama-3.2-90b-vision-instruct` via NVIDIA |
| Embedding | `nvidia/nv-embed-v1` (4096 dims) via NVIDIA |
| Binding | OpenAI (compatível com NVIDIA API) |
| Servidor | FastAPI + Uvicorn na porta 9621 |
| Gerenciador de pacotes | `uv` (v0.11.16) |
| Storages | JsonKVStorage, JsonDocStatusStorage, NetworkXStorage, NanoVectorDBStorage |

## Localização

- **Diretório:** `/home/marcus/projeto_licitacoes/lightrag/`
- **Repositório original:** https://github.com/hkuds/lightrag
- **Servidor:** http://localhost:9621

## Arquivo `.env`

```env
LLM_BINDING=openai
LLM_BINDING_HOST=https://integrate.api.nvidia.com/v1
LLM_BINDING_API_KEY=nvapi-...
LLM_MODEL=meta/llama-3.2-90b-vision-instruct

EMBEDDING_BINDING=openai
EMBEDDING_BINDING_HOST=https://integrate.api.nvidia.com/v1
EMBEDDING_BINDING_API_KEY=nvapi-...
EMBEDDING_MODEL=nvidia/nv-embed-v1
EMBEDDING_DIM=4096
EMBEDDING_SEND_DIM=false

ENTITY_EXTRACTION_USE_JSON=true

HOST=0.0.0.0
PORT=9621
SUMMARY_LANGUAGE=Portuguese
```

> **⚠️ Atenção:** `EMBEDDING_DIM=4096` é obrigatório! O `nvidia/nv-embed-v1` retorna 4096 dimensões, não 1024. Se configurar 1024, o embedding quebra com erro "4 vectors returned, expected 1".

> **⚠️ Atenção 2:** `ENTITY_EXTRACTION_USE_JSON=true` é obrigatório pra extração de entidades funcionar com a LLM da NVIDIA. Sem isso, a LLM retorna formato incompatível (ex.: 53 campos em vez de 4).

## Instalação

```bash
cd /home/marcus/projeto_licitacoes/lightrag

# Instalar dependências
uv sync
uv sync --extra api   # para servidor HTTP

# Iniciar servidor
lightrag-server --host 0.0.0.0 --port 9621
```

## Endpoints da API

| Método | Endpoint | Descrição |
|---|---|---|
| GET | `/health` | Status do servidor |
| POST | `/documents/text` | Inserir documento de texto |
| GET | `/documents/track_status/{track_id}` | Status de processamento |
| GET | `/documents/pipeline_status` | Status do pipeline |
| POST | `/query` | Fazer pergunta (modos: naive, local, global, hybrid) |
| GET | `/graph/label/list` | Listar labels do grafo |

## Exemplos de Uso

### Inserir documento
```bash
curl -X POST http://localhost:9621/documents/text \
  -H "Content-Type: application/json" \
  -d '{"text": "Seu texto aqui...", "file_source": "meu-doc.txt"}'
```

### Fazer query (modo híbrido — recomenda
do)
```bash
curl -X POST http://localhost:9621/query \
  -H "Content-Type: application/json" \
  -d '{"query": "Sua pergunta?", "mode": "hybrid"}'
```

### Fazer query (modo naive — busca vetorial)
```bash
curl -X POST http://localhost:9621/query \
  -H "Content-Type: application/json" \
  -d '{"query": "Sua pergunta?", "mode": "naive"}'
```

## Pipeline de Processamento

1. **Chunking** — Divide o texto em chunks (Fixed token: 1200 chars, overlap 100)
2. **Embedding** — Gera vetores com `nvidia/nv-embed-v1` (4096 dims)
3. **Extração de Entidades** — LLM da NVIDIA extrai entidades e relações do texto
4. **Construção do Grafo** — Cria grafo de conhecimento (NetworkX)
5. **Indexação** — Armazena vetores no NanoVectorDB
6. **Query** — Recupera informação via busca vetorial (naive) ou grafo + vetores (hybrid)

## Problemas Resolvidos

### 1. Erro "4 vectors returned, expected 1"
- **Causa:** `EMBEDDING_DIM=1024` quando `nvidia/nv-embed-v1` retorna 4096 dims
- **Solução:** Alterar `EMBEDDING_DIM` para `4096` e limpar o storage

### 2. Extração de entidades retorna 0 entidades
- **Causa:** LLM da NVIDIA retorna formato incompatível com o parser do LightRAG
- **Solução:** Ativar `ENTITY_EXTRACTION_USE_JSON=true` no `.env`
- **Resultado:** 17 entidades e 14 relações extraídas do texto de teste sobre Nvidia

### 3. Query modo hybrid retorna "no-context"
- **Causa:** Grafo vazio (extração de entidades não funcionou)
- **Solução:** Corrigir extração de entidades e reprocessar os documentos

## Testes Realizados

### Documento: nvidia-info.txt
- **Tamanho:** ~600 chars
- **Entidades extraídas:** 17
- **Relações extraídas:** 14
- **Query teste:** "Quem fundou a Nvidia e quando?"
- **Resposta:** Jensen Huang, Chris Malachowsky e Curtis Priem em 1993 ✅
- **Query teste:** "Em quais mercados a Nvidia atua?"
- **Resposta:** Jogos, Data Centers, Automotivo, Robótica, IA/ML ✅

## Referências

- Repositório LightRAG: https://github.com/hkuds/lightrag
- API NVIDIA: https://integrate.api.nvidia.com/v1
- Documentação NVIDIA API: https://build.nvidia.com/explore/discover
