# Checklist de manutenção preventiva do Nominatim com Docker

Este documento reúne as principais tarefas de manutenção preventiva para manter o ambiente Nominatim saudável e funcionando de forma estável.

---

## 🗓️ Checklist de Manutenção

### 🔹 Diária
- Conferir se os containers estão rodando:
  ```bash
  docker ps
  ```
- Verificar se o serviço de atualização automática baixou o arquivo do Brasil:
  ```bash
  cat logs/update.log | tail -n 50
  ```
- Conferir uso de CPU e memória:
  ```bash
  docker stats
  ```

---

### 🔹 Semanal
- Revisar logs do Nominatim e Postgres.
- Conferir espaço em disco:
  ```bash
  df -h
  ```
- Validar se o cron do cleaner está rodando.
- Testar uma consulta simples na API:
  ```bash
  curl "http://localhost:8080/search.php?q=Salvador&format=json"
  ```

---

### 🔹 Mensal
- Rodar manualmente um `VACUUM FULL` no Postgres:
  ```bash
  docker exec nominatim-postgres vacuumdb --all --full --analyze
  ```
- Atualizar imagens Docker:
  ```bash
  docker compose pull && docker compose up -d
  ```
- Conferir se o alerta de disco está funcionando (simular enchendo um volume).
- Fazer backup dos volumes (`postgres-data` e `nominatim-data`).

---

### 🔹 Trimestral
- Testar restauração de backup.
- Revisar configurações de cache do Redis.
- Verificar se há novas versões do Nominatim e planejar upgrade.

---

## ⚡ Boas práticas
- Manter pelo menos **20% de espaço livre em disco**.
- Ajustar parâmetros do Postgres (`work_mem`, `shared_buffers`) se notar lentidão.
- Documentar qualquer alteração feita nos containers.
- Armazenar backups fora do servidor principal (ex.: S3, Google Drive, outro servidor).

---
## 🔙 Navegação

[⬅️ Voltar para o índice](../README.MD)
