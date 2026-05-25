---
title: "ADR-001: PostgreSQL como banco principal"
tags:
  - adr
  - banco-de-dados
---

# ADR-001: PostgreSQL como banco principal

## Status

**Aceita** — 2025-01-15

## Contexto

Precisamos de um banco relacional para o sistema de pedidos.
Requisitos: ACID, JSON support, performance em queries complexas.

## Decisão

Adotamos **PostgreSQL 16** como banco principal.

## Justificativa

| Critério | PostgreSQL | SQL Server | MySQL |
|:---------|:-----------|:-----------|:------|
| Licença | MIT (free) | Pago | GPL |
| JSON nativo | ✅ jsonb | ✅ | Parcial |
| Partitioning | ✅ | ✅ | ✅ |
| Full-text PT-BR | ✅ | ✅ | Parcial |
| Custo cloud | Menor | Maior | Médio |

## Consequências

- Equipe precisa aprender PostgreSQL (maioria vem de SQL Server)
- Migrations via EF Core continuam funcionando
- Economia de ~40% em custos de licenciamento