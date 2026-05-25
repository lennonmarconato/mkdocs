---
title: Git Workflow
description: Convenções de branches e commits
tags:
  - git
  - workflow
---

# Git Workflow

## Branches

```mermaid
gitGraph
  commit id: "init"
  branch develop
  commit id: "feat-1"
  branch feature/login
  commit id: "login-ui"
  commit id: "login-api"
  checkout develop
  merge feature/login
  branch release/1.0
  commit id: "bump"
  checkout main
  merge release/1.0 tag: "v1.0.0"
```

## Commits convencionais

Usamos **Conventional Commits**:

| Prefixo | Uso |
|:---------|:----|
| `feat:` | Nova funcionalidade |
| `fix:` | Correção de bug |
| `docs:` | Documentação |
| `refactor:` | Refatoração |
| `test:` | Testes |
| `chore:` | Tarefas internas |

!!! example "Exemplos"
    ```
    feat: adicionar endpoint de pedidos
    fix: corrigir validação de CPF
    docs: atualizar guia de onboarding
    ```

## Code Review

??? tip "Checklist do reviewer"
    - [ ] Testes passando?
    - [ ] Cobertura adequada?
    - [ ] Segue Clean Architecture?
    - [ ] Documentação atualizada?
    - [ ] Sem secrets hardcoded?