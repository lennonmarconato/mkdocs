---
title: "Runbook: Deploy em Produção"
tags:
  - runbook
  - deploy
  - produção
---

# Runbook: Deploy em Produção

!!! danger "Atenção"
    Este procedimento afeta o ambiente de produção.
    Sempre execute em dupla (pair deploy).

## Pré-requisitos

- [ ] Acesso SSH ao servidor de produção
- [ ] VPN ativa
- [ ] Branch `main` atualizada
- [ ] Todos os testes passando na pipeline

## Passos

### 1. Verificar estado atual

```bash
ssh producao "docker ps | grep api"
ssh producao "docker logs api --tail 20"
```

### 2. Executar deploy

```bash
ssh producao "cd /opt/api && docker compose pull && docker compose up -d"
```

### 3. Validar

```bash
curl -s https://api.meudominio.com/health | jq .
# Esperado: { "status": "healthy", "version": "1.x.x" }
```

## Rollback

```bash
ssh producao "cd /opt/api && docker compose down"
ssh producao "cd /opt/api && docker compose up -d --no-deps api"
```

!!! tip "Monitoramento"
    Após o deploy, acompanhe os logs por 10 minutos:
    ```bash
    ssh producao "docker logs -f api --since 5m"
    ```