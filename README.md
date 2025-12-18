# Projeto Nominatim (local) com Docker

Este repositório contém a configuração completa do **Nominatim com Docker**, incluindo documentação separada por tema para facilitar consulta e manutenção.

___

---

## 📂 Documentos disponíveis

### 1. [README.md](/docs/readme-nominatim.md)
Guia principal de instalação e inicialização do ambiente:
- Preparar diretório
- Subir serviços com `docker compose up`
- Acompanhar logs
- Testar API
- Estrutura dos serviços auxiliares

---

### 2. [README-checklist.md](/docs/checklist-manutencao.md)
Checklist de manutenção preventiva:
- Tarefas diárias, semanais, mensais e trimestrais
- Comandos úteis para cada etapa
- Boas práticas de operação

---

### 3. [README-operacao.md](/docs/manual-operacao-nominatim.md)
Manual rápido de operação:
- Comandos para verificar status dos serviços
- Testar API
- Monitorar recursos
- Rodar atualização, limpeza e backup manual
- Restaurar volumes a partir de backup
- Atualizar imagens Docker
- Simular alerta de disco

---

### 4. [README-capacidades.md](/docs/capacidades.md)
O que o Nominatim resolve (e o que não resolve):
- Geocodificação e reverse geocoding
- Busca geográfica e integração com sistemas
- Aplicações em rastreamento
- Limitações: mapas, rotas, cercas e visualização
- Ferramentas complementares recomendadas

---

## 📁 Estrutura de diretórios

```plaintext
nominatim-brasil/
├── docker-compose.yml        # Arquivo principal para subir todo o ambiente
├── README.md                 # Guia principal de instalação e inicialização
│
├── postgres-data/            # Volume persistente do Postgres
├── nominatim-data/           # Volume persistente do Nominatim
├── logs/                     # Logs de atualização, limpeza e monitoramento
├── backup/                   # Backups automáticos (diários)
│
└── docs/                     # Documentação adicional
    ├── README-operacao.md    # Manual rápido de operação
    ├── README-checklist.md   # Checklist de manutenção preventiva
    ├── README-indice.md      # Índice geral com links para todos os docs
    ├── arquitetura.png       # Diagrama visual da arquitetura
    └── outros.md             # Notas extras ou futuras expansões
```
___

## 🧩 Diagrama de arquitetura

Este diagrama mostra a estrutura lógica do ambiente Nominatim com Docker, destacando os principais componentes e suas interações:

- **Nominatim API** no centro
- **Postgres** como banco de dados
- **Redis** como cache
- **Updater** para baixar e atualizar dados do Brasil
- **Cleaner** para otimizar e limpar logs
- **Disk Monitor** para alertas de uso de disco
- **Backup** para cópias automáticas dos volumes

![Diagrama de arquitetura](/docs/arquitetura.png)

___

## 🚀 Como usar
- Consulte o **README principal** para instalar e iniciar o ambiente.  
- Use o **manual de operação** para tarefas do dia a dia.  
- Use o **checklist de manutenção** para manter o sistema saudável a longo prazo.  

---

## ⚡ Observação
Cada documento foi criado para ser independente e direto ao ponto.  
Este índice serve como guia central para navegar entre eles.
