# Manual rápido de operação do Nominatim com Docker

Este documento reúne os principais comandos e verificações para operar o ambiente Nominatim com Docker no dia a dia.

---

## 🔹 Verificar status dos serviços
```bash
docker ps
```
Confirma se todos os containers estão rodando.

---

## 🔹 Testar a API
```bash
curl "http://localhost:8080/search.php?q=Salvador&format=json"
```
Verifica se o Nominatim está respondendo corretamente.

---

## 🔹 Verificar uso de disco
```bash
df -h
```
Mostra o espaço livre em cada volume.

---

## 🔹 Monitorar recursos (CPU/RAM)
```bash
docker stats
```
Mostra uso de CPU e memória por container.

---

## 🔹 Verificar logs de atualização
```bash
cat logs/update.log | tail -n 50
```
Mostra as últimas linhas do log de atualização automática do Brasil.

---

## 🔹 Rodar atualização manual
```bash
docker exec nominatim-brasil nominatim refresh --input-file=/app/data.osm.pbf
```

---

## 🔹 Rodar limpeza manual
```bash
docker exec nominatim-postgres vacuumdb --all --analyze
```

---

## 🔹 Rodar backup manual
```bash
tar czf backup/postgres-manual.tar.gz postgres-data/
tar czf backup/nominatim-manual.tar.gz nominatim-data/
```

---

## 🔹 Restaurar volumes a partir de backup
```bash
docker volume rm nominatim-postgres nominatim-data
docker volume create nominatim-postgres
docker volume create nominatim-data

docker run --rm -v nominatim-postgres:/var/lib/postgresql/data -v $(pwd)/backup:/backup ubuntu tar xzf /backup/postgres-backup-YYYY-MM-DD.tar.gz -C /
docker run --rm -v nominatim-data:/var/lib/nominatim -v $(pwd)/backup:/backup ubuntu tar xzf /backup/nominatim-backup-YYYY-MM-DD.tar.gz -C /
```

---

## 🔹 Atualizar imagens Docker
```bash
docker compose pull
docker compose up -d
```

---

## 🔹 Simular alerta de disco (teste)
```bash
fallocate -l 10G logs/fakefile
```
Cria um arquivo falso para simular uso de disco e testar o alerta.

---

## ⚡ Observação
Este manual é voltado para operação diária.  
Para manutenção preventiva, consulte o documento **Checklist de manutenção preventiva**.

---

## 🔙 Navegação

[⬅️ Voltar para o índice](../README.MD)
