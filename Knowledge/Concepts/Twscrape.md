---
type: concept
status: current
created: 2026-06-05
updated: 2026-06-05
tags: [scraping, twitter, x, python, biblioteca]
sources: []
importance: medium
agent: claude
---

# Twscrape

Biblioteca Python assíncrona para scraping do X (Twitter) usando autenticação por cookies de sessão, sem depender da API oficial paga.

## Características

- **Autenticação via cookies**: usa `auth_token` + `ct0` + `twid` do navegador
- **Assíncrona**: baseada em `asyncio` — todas as funções são `async`
- **Pool de contas**: suporta múltiplas contas para distribuir requisições e evitar rate limits
- **Sem API key**: não requer credenciais de desenvolvedor do X

## Instalação

```bash
pip install twscrape
```

## Métodos principais

| Método | O que faz |
|--------|-----------|
| `api.search(query, limit)` | Busca tweets por termo ou operadores avançados |
| `api.user_by_login(username)` | Perfil pelo @handle |
| `api.user_tweets(username, limit)` | Tweets recentes de um usuário |
| `api.user_tweets_and_replies(username, limit)` | Tweets + replies de um usuário |
| `api.user_media(username, limit)` | Apenas tweets com mídia |
| `api.tweet_details(tweet_id)` | Detalhes de um tweet específico |
| `api.tweet_replies(tweet_id, limit)` | Replies de um tweet |
| `api.tweet_thread(tweet_id)` | Thread completa |
| `api.followers(username, limit)` | Seguidores |
| `api.following(username, limit)` | Quem o usuário segue |
| `api.retweeters(tweet_id, limit)` | Quem deu RT |
| `api.trends()` | Trending topics |
| `api.bookmarks(limit)` | Bookmarks da conta autenticada |

## Como funciona internamente

O twscrape usa os cookies para autenticar e obtém dinamicamente o **Bearer Token** que o web app do X gera via JavaScript — eliminando o erro `code 32 / code 89` que ocorre ao chamar a API REST diretamente com curl sem o token correto.

## Limitações

- Sessões são vinculadas a contas — se o X revogar a sessão, os cookies param de funcionar
- Sem suporte a ações de escrita (post, like, follow) — apenas leitura
- Rate limits não documentados — testar empiricamente

## Relacionado

- [[XCookieAuth]] — mecanismo de autenticação que o twscrape usa
- [[Synthesis/x-scraping-com-cookies]] — tutorial completo de uso
- [[Composio]] — alternativa gerenciada para integrações OAuth com X
