---
type: concept
status: current
created: 2026-06-03
updated: 2026-06-03
tags: [mcp, notebooklm, tools]
sources: []
importance: medium
agent: hermes
---

# McpNotebooklmTools

Lista completa de habilidades e ferramentas disponíveis no servidor MCP do NotebookLM integrado ao Hermes Agent.

## Visão geral
O servidor MCP `notebooklm` fornece acesso programático às funcionalidades do NotebookLM (Google) via Model Context Protocol. Após a configuração, o Hermes expõe 30 ferramentas que podem ser chamadas diretamente por agentes ou usadas em fluxos de trabalho.

## Ferramentas (30 total)

1. **notebook.ask**  
   Conversational Research Partner (NotebookLM • Gemini 2.5 • ...)  
   – Permite fazer perguntas em linguagem natural sobre as fontes carregadas e obter respostas contextualizadas.

2. **library.discover**  
   🚀 AUTO-DISCOVERY — Automatically generate notebook metadata ...  
   – Descobre e cria metadata para notebooks existentes de forma automática.

3. **library.add**  
   📝 MANUAL ENTRY — Add notebook with manually specified metadata ...  
   – Adiciona um notebook ao repositório com metadata definida manualmente.

4. **library.list**  
   List all library notebooks with metadata (name, topics, use ...)  
   – Lista todos os notebooks disponíveis, incluindo tópicos e casos de uso.

5. **library.get**  
   Get detailed information about a specific notebook by ID  
   – Recupera informações completas de um notebook específico usando seu identificador.

6. **library.select**  
   Set a notebook as the active default (used when ask_question ...)  
   – Define um notebook como padrão para operações subsequentes como `notebook.ask`.

7. **library.update**  
   Update notebook metadata based on user intent.  
   – Atualiza os metadados de um notebook conforme a intenção do usuário.

8. **library.remove**  
   Dangerous — requires explicit user confirmation.  
   – Remove um notebook da biblioteca (necessita de confirmação explícita).

9. **library.search**  
   Search library by query (name, description, topics, tags). U...  
   – Realiza busca na biblioteca por termo em nome, descrição, tópicos ou tags.

10. **library.stats**  
    Get statistics about your notebook library (total notebooks,...)  
    – Retorna estatísticas gerais da biblioteca (contagem de notebooks, etc.).

11. **session.list**  
    List all active sessions with stats (age, message count, las...)  
    – Lista todas as sessões de chat ativas com métricas como idade e contagem de mensagens.

12. **session.close**  
    Close a specific session by session ID. Ask before closing i...  
    – Fecha uma sessão específica pelo ID (pede confirmação).

13. **session.reset**  
    Reset a session's chat history (keep same session ID). Use f...  
    – Limpa o histórico de chat de uma sessão mantendo o mesmo ID.

14. **server.health**  
    Get server health status including authentication state, act...  
    – Verifica a saúde do servidor MCP, incluindo estado de autenticação.

15. **auth.setup**  
    Google authentication for NotebookLM access - opens a browse...  
    – Inicia o fluxo de autenticação com Google para acessar o NotebookLM.

16. **auth.logout**  
    De-authenticate (logout) - Clears all authentication data fo...  
    – Remove todos os dados de autenticação (logout).

17. **auth.switch**  
    Switch to a different Google account or re-authenticate. Use...  
    – Troca de conta Google ou força re-autenticação.

18. **server.cleanup**  
    ULTRATHINK Deep Cleanup - Scans entire system for ALL Notebo...  
    – Executa uma limpeza profunda no sistema inteiro relacionada ao NotebookLM.

19. **source.add**  
    Add a source (document, URL, text, YouTube video) to the cur...  
    – Adiciona uma fonte (arquivo, URL, texto ou vídeo do YouTube) ao notebook atual.

20. **source.delete**  
    Delete a source from the current NotebookLM notebook.  
    – Remove uma fonte do notebook atualmente selecionado.

21. **content.generate**  
    Generate content from your NotebookLM sources.  
    – Gera novos conteúdos (respostas, resumos, etc.) com base nas fontes carregadas.

22. **content.list**  
    List all sources and generated content in the current notebook...  
    – Lista todas as fontes e o conteúdo gerado associado ao notebook ativo.

23. **content.download**  
    Download or export generated content from NotebookLM.  
    – Faz download ou exporta o conteúdo gerado pelo NotebookLM.

24. **note.create**  
    Create a note in the NotebookLM Studio panel.  
    – Cria uma nova nota no painel Studio do NotebookLM.

25. **note.save_chat**  
    Save the current NotebookLM chat/discussion to a note.  
    – Salva o histórico de bate-papo atual como uma nota fixa.

26. **note.to_source**  
    Convert a note to a source document in NotebookLM.  
    – Converte uma nota existente em uma fonte de documento que pode ser usada para geração.

27. **vault.batch**  
    Run a list of questions against a notebook and persist each ...  
    – Executa um lote de perguntas contra um notebook e persiste cada resposta individualmente.

28. **notebook.list**  
    Scrape the NotebookLM homepage to get a real list of all not...  
    – Obtém uma lista atualizada de todos os notebooks disponíveis no serviço NotebookLM.

29. **notebook.create**  
    Create a brand-new empty notebook directly in NotebookLM (no...  
    – Cria um notebook completamente vazio diretamente no serviço NotebookLM.

30. **notebook.delete**  
    Delete one or more notebooks directly from NotebookLM (UI-le...  
    – Exclui um ou mais notebooks diretamente da interface do NotebookLM.

## Como usar
As ferramentas podem ser invocadas via linha de comando do Hermes:
```bash
hermes mcp call notebooklm <nome-da-tool> --<argumentos>
```
Exemplo:
```bash
hermes mcp call notebooklm notebook.ask --question "Como fazer licitação perfeita que passe na auditoria?"
```
Ou deixado que o agente Hermes decida automaticamente quando usar cada ferramenta com base no contexto da conversa.

## Integração com o Vault
Esta página foi criada no vault Obsidian em `/home/marcus/Documentos/vault01/vault01/Knowledge/Concepts/McpNotebooklmTools.md` e pode ser linkada usando wikilinks do tipo `[[McpNotebooklmTools]]`.

---
*Atualizado automaticamente pelo Hermes Agent em 2026-06-03.*