---
tags:
  - licitacoes
  - fontes-oficiais
  - api
  - pncp
  - comprasgov
created: 2026-06-02
---

# Fontes Oficiais de Dados de Licitações

## 1. PNCP — Portal Nacional de Contratações Públicas

O sítio eletrônico oficial exigido pela [[Lei 14.133/2021]] para centralizar todas as contratações públicas do país.

- **Site:** https://pncp.gov.br
- **API:** https://pncp.gov.br/api/swagger/index.html
- **Conteúdo:** Editais, contratações diretas, atas de registro de preços, planos de contratações anuais

## 2. Compras.gov.br

Principal plataforma de execução das licitações federais (utilizada em massa pelas Forças Armadas).

- **Site:** https://gov.br/compras
- **API:** https://www.gov.br/compras/pt-br/api
- **Conteúdo:** 
  - Manuais e guias para fase preparatória (ETPs, TRs)
  - Modelos padronizados da AGU
  - Legislação compilada (INs, Decretos, Portarias)

## 3. Legislação Pura — Portal do Planalto

Textos oficiais da lei para alimentar sistemas de IA.

- **Lei 14.133/2021 (Nova Lei de Licitações):** https://www.planalto.gov.br/ccivil_03/_ato2019-2022/2021/lei/l14133.htm
- **Decreto 11.461/2023 (Leilão e Credenciamento):** https://www.planalto.gov.br/ccivil_03/_ato2023-2026/2023/decreto/D11461.htm
- **Decreto 10.024/2019 (Pregão Eletrônico):** https://www.planalto.gov.br/ccivil_03/_ato2019-2022/2019/decreto/D10024.htm

## Como Usar no Projeto

As APIs oficiais permitem baixar dados automaticamente com scripts Python para alimentar o LightRAG local:
- API do PNCP para editais e contratações
- API do Compras.gov.br para modelos e normativos
- Scraping do Planalto para textos de lei puros

## Observações

- A API do PNCP é REST e não requer autenticação para consultas básicas
- O Compras.gov.br tem documentação em https://www.gov.br/compras/pt-br/acesso-a-informacao/dados-abertos
- A [[Lei 14.133/2021]] substituiu definitivamente a antiga Lei 8.666/1993
