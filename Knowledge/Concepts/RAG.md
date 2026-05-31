---
type: concept
status: current
created: 2026-05-30
updated: 2026-05-30
tags: [rag, retrieval, llm, knowledge-base]
sources: [raw/llm-wiki.md]
importance: medium
agent: claude
---

# RAG (Retrieval-Augmented Generation)

Padrão de retrieval onde o LLM recupera chunks relevantes de documentos no momento da query e gera uma resposta.

## Funcionamento

1. Documentos são fragmentados em chunks e transformados em embeddings (vetores)
2. Na query, chunks semanticamente próximos são recuperados do vector DB
3. O LLM recebe os chunks + query e gera a resposta

## Exemplos

NotebookLM, ChatGPT file uploads, a maioria dos sistemas de "chat com documentos".

## Limitações vs [[LLMWiki]]

- Conhecimento re-derivado a cada query — sem acumulação
- Sínteses multi-documento requerem que o LLM encontre e conecte fragmentos relevantes toda vez
- Não sinaliza contradições entre documentos
- Não mantém cross-references

## Quando usar RAG vs LLM Wiki

**RAG é melhor quando:**
- Grande volume de documentos (milhares+)
- Documentos são consultados pontualmente, não acumulados
- Não há padrão de exploração progressiva

**LLM Wiki é melhor quando:**
- Conhecimento é acumulado incrementalmente ao longo do tempo
- Síntese entre fontes é frequente
- Navegabilidade e conexões entre conceitos têm valor

## Ligações

- [[LLMWiki]] — alternativa para knowledge bases pessoais
- [[AgentMemory]] — memória em agentes; RAG é uma das implementações possíveis
