---
type: synthesis
status: current
created: 2026-06-05
updated: 2026-06-05
tags: [scraping, twitter, x, python, automação, cookies, oauth]
sources: []
importance: high
agent: claude
---

# Tutorial: Autenticação no X via Cookies + twscrape

Guia prático completo para autenticar e interagir com a API do X (Twitter) usando cookies de sessão do navegador, sem precisar de acesso à API oficial paga.

---

## Por que usar cookies em vez da API oficial?

A API oficial do X passou a exigir planos pagos a partir de 2023. A alternativa é usar os **cookies de sessão do navegador** — os mesmos que o site usa internamente — para fazer requisições autenticadas à API interna do X.

| Método | Custo | Limite | Complexidade |
|--------|-------|--------|--------------|
| API Oficial (Basic) | US$100/mês | 10k tweets/mês | Baixa |
| API Oficial (Pro) | US$5.000/mês | 1M tweets/mês | Baixa |
| Cookies + twscrape | Gratuito | Limitado pela conta | Média |

> **Importante**: use apenas com sua própria conta. Não viole os Termos de Serviço do X para scraping em massa ou uso comercial não autorizado.

---

## Conceitos Fundamentais

### Os cookies críticos do X

O X usa três cookies para autenticar uma sessão web:

| Cookie | Função |
|--------|--------|
| `auth_token` | Token de sessão OAuth — identifica você como usuário autenticado |
| `ct0` | Token CSRF — protege contra ataques cross-site (deve ser enviado como header também) |
| `twid` | Seu Twitter User ID codificado em URL (ex: `u%3D42095864` = ID `42095864`) |

### Por que curl direto na API não funciona?

A API REST pública do X (`api.x.com/1.1/`) exige um **Bearer Token** específico do app web — que muda periodicamente e é gerado dinamicamente via JavaScript. O [[Twscrape]] extrai esse token automaticamente, por isso é a abordagem mais robusta.

---

## Passo a Passo

### 1. Exportar os cookies do navegador

**Opção A — Extensão (mais fácil):**

1. Instale a extensão **"Get cookies.txt LOCALLY"** no Chrome/Firefox
2. Acesse [x.com](https://x.com) e faça login normalmente
3. Clique na extensão → "Export as Netscape format"
4. Salve o arquivo `.txt`

**Opção B — DevTools (sem extensão):**

1. Acesse [x.com](https://x.com) logado
2. Abra DevTools (`F12`) → aba **Application** → **Cookies** → `https://x.com`
3. Copie manualmente os valores de `auth_token`, `ct0` e `twid`

> **Atenção**: exporte os cookies enquanto a sessão está ativa. Se você sair da conta depois de exportar, os cookies são invalidados imediatamente pelo servidor.

### 2. Instalar o twscrape

```bash
pip install twscrape
```

### 3. Autenticar com os cookies

#### Método A — String de cookies (mais direto)

```python
import asyncio
from twscrape import API

async def main():
    api = API()
    
    await api.pool.add_account(
        username="seu_username",
        password="",
        email="",
        email_password="",
        cookies="auth_token=SEU_AUTH_TOKEN; ct0=SEU_CT0; twid=u%3DSEU_ID"
    )
    
    # Verificar se está autenticado
    user = await api.user_by_login("twitter")
    print(f"Autenticado! Encontrou: @{user.username}")

asyncio.run(main())
```

#### Método B — Arquivo JSON de cookies

Salve seus cookies em `cookies.json`:

```json
{
  "auth_token": "SEU_AUTH_TOKEN_AQUI",
  "ct0": "SEU_CT0_AQUI",
  "twid": "u%3DSEU_USER_ID"
}
```

```python
import asyncio
from twscrape import API

async def main():
    api = API()
    client = api.pool._client  # acesso ao cliente HTTP interno
    
    # Carregar cookies do arquivo
    api.pool._client.cookies.update(
        json.load(open("cookies.json"))
    )
    
asyncio.run(main())
```

#### Método C — Arquivo Netscape (formato exportado pelo navegador)

```python
import asyncio
from twscrape import API

async def main():
    api = API()
    
    await api.pool.add_account(
        username="minha_conta",
        cookies="auth_token=...; ct0=...; twid=..."
        # leia o arquivo .txt e extraia os valores
    )

asyncio.run(main())
```

---

## API Completa do twscrape

### Busca de tweets

```python
# Buscar tweets por termo
async for tweet in api.search("inteligência artificial", limit=50):
    print(f"@{tweet.user.username}: {tweet.rawContent}")
    print(f"  Likes: {tweet.likeCount} | RT: {tweet.retweetCount}")
    print(f"  Data: {tweet.date}")
```

```python
# Busca avançada (mesmo operadores que o site)
async for tweet in api.search("python lang:pt -is:retweet min_faves:100", limit=20):
    print(tweet.url)
```

### Perfis de usuários

```python
# Buscar usuário pelo @username
user = await api.user_by_login("elonmusk")
print(f"Nome: {user.displayname}")
print(f"Bio: {user.rawDescription}")
print(f"Seguidores: {user.followersCount}")
print(f"Verificado: {user.verified}")

# Informações detalhadas
about = await api.user_about("elonmusk")
```

### Tweets de um usuário

```python
# Tweets recentes
async for tweet in api.user_tweets("elonmusk", limit=20):
    print(tweet.rawContent[:100])

# Tweets e respostas (inclui replies)
async for tweet in api.user_tweets_and_replies("elonmusk", limit=20):
    print(tweet.rawContent[:100])

# Mídia (só tweets com fotos/vídeos)
async for tweet in api.user_media("elonmusk", limit=10):
    print(tweet.media)
```

### Detalhes de um tweet específico

```python
# Por ID do tweet
tweet = await api.tweet_details(1234567890123456789)
print(f"Texto: {tweet.rawContent}")
print(f"Autor: @{tweet.user.username}")

# Thread completa (replies encadeados)
async for t in api.tweet_thread(1234567890123456789):
    print(t.rawContent)

# Replies de um tweet
async for reply in api.tweet_replies(1234567890123456789, limit=20):
    print(f"@{reply.user.username}: {reply.rawContent}")
```

### Relações sociais

```python
# Seguidores de um usuário
async for follower in api.followers("elonmusk", limit=100):
    print(f"@{follower.username}")

# Quem o usuário segue
async for following in api.following("elonmusk", limit=100):
    print(f"@{following.username}")

# Quem deu RT em um tweet
async for user in api.retweeters(tweet_id, limit=50):
    print(f"@{user.username}")
```

### Tendências

```python
# Trending topics
trends = await api.trends()
for trend in trends:
    print(f"{trend.name}: {trend.tweetCount} tweets")

# Busca por trend
async for tweet in api.search_trend("ChatGPT", limit=30):
    print(tweet.rawContent[:80])
```

### Bookmarks

```python
# Seus bookmarks (requer autenticação)
async for tweet in api.bookmarks(limit=50):
    print(tweet.rawContent)
```

---

## Estrutura dos Objetos Retornados

### Tweet

```python
tweet.id               # ID numérico
tweet.url              # URL do tweet
tweet.date             # datetime
tweet.rawContent       # texto completo
tweet.likeCount        # número de likes
tweet.retweetCount     # número de RTs
tweet.replyCount       # número de replies
tweet.quoteCount       # número de quotes
tweet.viewCount        # visualizações
tweet.lang             # idioma detectado
tweet.user             # objeto User (ver abaixo)
tweet.media            # lista de mídias (fotos, vídeos)
tweet.links            # URLs mencionadas
tweet.hashtags         # hashtags do tweet
tweet.mentionedUsers   # usuários mencionados
tweet.retweetedTweet   # tweet original (se for RT)
tweet.quotedTweet      # tweet citado (se for quote)
tweet.inReplyToUser    # usuário respondido
```

### User

```python
user.id                # ID numérico
user.username          # @handle (sem o @)
user.displayname       # nome exibido
user.rawDescription    # bio completa
user.followersCount    # número de seguidores
user.friendsCount      # número de seguindo
user.statusesCount     # total de tweets
user.verified          # verificado azul (legado)
user.location          # localização no perfil
user.profileImageUrl   # URL da foto de perfil
user.created           # data de criação da conta
```

---

## Exportar dados para CSV / JSON

```python
import asyncio
import json
import csv
from twscrape import API

async def exportar_busca(termo: str, limite: int, arquivo: str):
    api = API()
    await api.pool.add_account(
        username="minha_conta",
        cookies="auth_token=...; ct0=...; twid=..."
    )
    
    tweets = []
    async for tweet in api.search(termo, limit=limite):
        tweets.append({
            "id": tweet.id,
            "data": tweet.date.isoformat(),
            "autor": tweet.user.username,
            "texto": tweet.rawContent,
            "likes": tweet.likeCount,
            "retweets": tweet.retweetCount,
            "url": tweet.url,
        })
    
    # JSON
    with open(f"{arquivo}.json", "w", encoding="utf-8") as f:
        json.dump(tweets, f, ensure_ascii=False, indent=2)
    
    # CSV
    with open(f"{arquivo}.csv", "w", newline="", encoding="utf-8") as f:
        writer = csv.DictWriter(f, fieldnames=tweets[0].keys())
        writer.writeheader()
        writer.writerows(tweets)
    
    print(f"✓ {len(tweets)} tweets exportados para {arquivo}.json e {arquivo}.csv")

asyncio.run(exportar_busca("inteligência artificial", 100, "tweets_ia"))
```

---

## Monitoramento contínuo (polling)

```python
import asyncio
from datetime import datetime
from twscrape import API

async def monitorar(termo: str, intervalo_segundos: int = 60):
    api = API()
    await api.pool.add_account(
        username="minha_conta",
        cookies="auth_token=...; ct0=...; twid=..."
    )
    
    vistos = set()
    print(f"Monitorando '{termo}' a cada {intervalo_segundos}s...")
    
    while True:
        async for tweet in api.search(f"{termo} -is:retweet", limit=20):
            if tweet.id not in vistos:
                vistos.add(tweet.id)
                print(f"[{datetime.now():%H:%M:%S}] @{tweet.user.username}: {tweet.rawContent[:100]}")
        
        await asyncio.sleep(intervalo_segundos)

asyncio.run(monitorar("Claude Anthropic"))
```

---

## Diagnóstico de problemas

| Sintoma | Causa provável | Solução |
|---------|---------------|---------|
| `error 89: Invalid or expired token` via curl direto | Bearer token incorreto | Use twscrape em vez de curl |
| `error 32: Could not authenticate you` via curl | Usando API REST sem bearer correto | Use twscrape |
| `Couldn't get KEY_BYTE indices` no twikit | auth_token inválido ou revogado | Re-exporte os cookies do navegador |
| Conta adicionada mas requisições falham | Sessão revogada após exportação | Faça login no navegador e re-exporte |
| Rate limit (429) | Muitas requisições seguidas | Adicione `await asyncio.sleep(2)` entre chamadas |

### Verificar se os cookies ainda são válidos

```python
# Se retornar dados reais = cookies válidos
user = await api.user_by_login("twitter")
print(user.username)  # deve imprimir "twitter"
```

---

## Segurança e boas práticas

1. **Nunca commite cookies em repositórios** — coloque em `.env` ou variáveis de ambiente
2. **Cookies = senha da sua conta** — quem tiver o `auth_token` consegue acessar sua conta
3. **Re-exporte periodicamente** — sessões podem ser invalidadas sem aviso
4. **Rate limiting**: não faça mais de 1 requisição por segundo para evitar bloqueio
5. **Use contas secundárias** para scripts de produção — proteja sua conta principal

```python
# Carregar de variável de ambiente (recomendado)
import os
from dotenv import load_dotenv

load_dotenv()
cookies = f"auth_token={os.getenv('X_AUTH_TOKEN')}; ct0={os.getenv('X_CT0')}; twid={os.getenv('X_TWID')}"
```

---

## Conexões

- [[Twscrape]] — biblioteca Python usada neste tutorial
- [[XCookieAuth]] — mecanismo de autenticação via cookies de sessão
- [[Composio]] — alternativa gerenciada para integrações OAuth com X e outros serviços
- [[AgentMemory]] — padrão de persistência útil para armazenar tweets coletados
- [[HermesAgent]] — agente que pode executar scripts de scraping como skills agendadas
- [[CronJobs]] — agendar coletas automáticas de tweets em intervalos regulares

---

## Lacunas / Próximos passos

- Testar com `twscrape` via CLI (`twscrape search "termo" --limit 100`)
- Explorar integração com [[ChromaDB]] para armazenar tweets como embeddings
- Avaliar [[Composio]] como alternativa gerenciada para OAuth sem gestão de cookies
- Rate limits reais do X não estão documentados publicamente — testar empiricamente
