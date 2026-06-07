# Regras do Repositório vault01

## Branch Protection
- `main` é protegida — requer PR + review para merge
- Commits diretos em `main` só via `sync-vault.sh` (auto-sync)

## Commits
- Auto-sync: `auto-sync: YYYY-MM-DD HH:MM` (script cron)
- Manuais: `tipo: descrição curta` (ex: `docs: add REPO_RULES.md`)

## Estrutura do Vault (Obsidian)
```
/Clippings/          # Fontes brutas - IMUTÁVEL
/Knowledge/          # Conhecimento processado
   /Concepts/        # Conceitos (PascalCase)
   /Summaries/       # Resumos (kebab-case)
   /Synthesis/       # Sínteses (kebab-case)
   /Decisions/       # Decisões
   /Pending/         # Conflitos aguardando revisão
/Journal/            # Diário (append-only)
/Projects/           # Projetos ativos
/Constitution/       # Governança
```

## Pull Requests
- Obrigatório para mudanças em `Constitution/`, `Knowledge/Concepts/`
- Auto-sync bypassa PR (configurado no branch protection)

## Secrets
- NUNCA commitar tokens, chaves, senhas
- Usar `gh secret` ou variáveis de ambiente
