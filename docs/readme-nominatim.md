# Nominatim com Docker (Brasil)

Este projeto monta um ambiente completo do **Nominatim** usando **Docker Compose**, já preparado para funcionar com os dados do Brasil.  
Inclui:
- Postgres + Redis
- Nominatim API
- Atualização automática diária dos dados do Brasil
- Limpeza de logs e otimização do banco
- Monitoramento de disco com alertas
- Backups automáticos

---

## 🚀 Inicialização

### 1. Preparar diretório
Crie uma pasta e salve o `docker-compose.yml` nela:
```bash
mkdir nominatim-brasil
cd nominatim-brasil
```

### 2. Subir os serviços
```bash
docker compose up -d
```
- O container Nominatim baixa automaticamente o arquivo do Brasil na primeira execução.
- Em seguida, importa os dados para o Postgres.

### 3. Acompanhar logs
```bash
docker logs -f nominatim-brasil
```

### 4. Testar a API
```bash
curl "http://localhost:8080/search.php?q=Salvador&format=json"
```

---

## 🛠️ Serviços auxiliares

- **Updater**: baixa dados atualizados diariamente às 03:00 e aplica refresh.  
- **Cleaner**: roda às 04:00, apaga logs antigos e otimiza o banco.  
- **Disk Monitor**: verifica uso de disco a cada 30 min e envia alerta se passar de 80%.  
- **Backup**: gera backups diários às 02:00 em `./backup`.

---

## 📋 Checklist rápido

### Status dos serviços
```bash
docker ps
```

### Logs de atualização
```bash
cat logs/update.log | tail -n 50
```

### Uso de disco
```bash
df -h
```

### Recursos (CPU/RAM)
```bash
docker stats
```

### Atualização manual
```bash
docker exec nominatim-brasil nominatim refresh --input-file=/app/data.osm.pbf
```

### Limpeza manual
```bash
docker exec nominatim-postgres vacuumdb --all --analyze
```

### Backup manual
```bash
tar czf backup/postgres-manual.tar.gz postgres-data/
tar czf backup/nominatim-manual.tar.gz nominatim-data/
```

### Restaurar volumes
```bash
docker volume rm nominatim-postgres nominatim-data
docker volume create nominatim-postgres
docker volume create nominatim-data

docker run --rm -v nominatim-postgres:/var/lib/postgresql/data -v $(pwd)/backup:/backup ubuntu tar xzf /backup/postgres-backup-YYYY-MM-DD.tar.gz -C /
docker run --rm -v nominatim-data:/var/lib/nominatim -v $(pwd)/backup:/backup ubuntu tar xzf /backup/nominatim-backup-YYYY-MM-DD.tar.gz -C /
```

---

## ⚡ Boas práticas
- Manter pelo menos **20% de espaço livre em disco**.  
- Testar restauração de backup trimestralmente.  
- Atualizar imagens Docker mensalmente:
```bash
docker compose pull && docker compose up -d
```
- Documentar alterações nos containers.

---

## 📌 Observação
Este ambiente foi projetado para uso local ou em servidor dedicado.  
Para produção, recomenda-se monitoramento adicional e ajustes de performance no Postgres.

---

## 🔙 Navegação

[⬅️ Voltar para o índice](../README.MD)
