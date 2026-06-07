---
type: concept
status: current
created: 2026-06-05
updated: 2026-06-05
tags: [autenticação, cookies, oauth, twitter, x, sessão]
sources: []
importance: medium
agent: claude
---

# XCookieAuth

Técnica de autenticação que usa cookies de sessão do navegador para acessar a API interna do X (Twitter), contornando a necessidade de credenciais de desenvolvedor pagas.

## Os três cookies essenciais

| Cookie | Tipo | Função |
|--------|------|--------|
| `auth_token` | HttpOnly, Secure | Token OAuth de sessão — identifica o usuário autenticado. Equivale à senha para fins de acesso à API. |
| `ct0` | Secure | Token CSRF — deve ser enviado tanto como cookie quanto como header `x-csrf-token` em todas as requisições mutáveis |
| `twid` | - | Twitter User ID codificado em URL (ex: `u%3D42095864` decodifica para o ID `42095864`) |

## Por que cookies funcionam como OAuth

O X usa internamente OAuth 2.0 com sessões web. O `auth_token` é o equivalente de um **access token OAuth** vinculado à sessão do browser. Quando enviado junto com o Bearer Token do app web e o header `x-csrf-token`, o servidor trata a requisição como autenticada.

## Ciclo de vida dos cookies

```
Login no X.com
    ↓
X gera auth_token (validade ~1 ano)
    ↓
Exportar cookies enquanto logado
    ↓
Usar em scripts/bibliotecas
    ↓
X pode revogar a qualquer momento:
  - Logout manual
  - Atividade suspeita detectada
  - Troca de senha
  - Inatividade prolongada
```

## Por que curl direto não funciona

Chamadas diretas à API REST (`api.x.com/1.1/`) retornam erros mesmo com cookies válidos:

- **Erro 32** — `Could not authenticate you`: Bearer Token incorreto ou ausente
- **Erro 89** — `Invalid or expired token`: token OAuth inválido (ou Bearer errado)

O Bearer Token necessário é gerado dinamicamente via JavaScript pelo app web — não é um valor fixo público. Bibliotecas como [[Twscrape]] extraem esse token automaticamente.

## Validade e renovação

- Timestamps de expiração nos cookies são **apenas datas máximas** — o X pode invalidar antes
- Revogar acontece server-side: o timestamp do cookie continua no futuro, mas requisições falham
- Solução: re-exportar cookies do navegador após fazer login novamente

## Ferramentas que suportam

| Ferramenta | Linguagem | Suporte a cookies |
|------------|-----------|-------------------|
| [[Twscrape]] | Python | ✓ Nativo via `add_account(cookies=...)` |
| twikit | Python | ✓ Via `set_cookies()` |
| curl | Shell | Parcial (falta Bearer Token correto) |

## Segurança

O `auth_token` é equivalente à senha da conta:
- Nunca commitar em repositórios públicos
- Armazenar em variáveis de ambiente (`.env`)
- Usar contas secundárias para automação em produção

## Relacionado

- [[Twscrape]] — biblioteca que abstrai este mecanismo
- [[Synthesis/x-scraping-com-cookies]] — tutorial completo
- [[Composio]] — alternativa: gerencia OAuth para X sem exposição de cookies
