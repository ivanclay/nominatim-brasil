# O que o Nominatim resolve (e o que não resolve)

Este documento explica as capacidades e limitações do **Nominatim**, para ajudar na escolha e integração correta em sistemas que envolvem dados geográficos.

---

## ✅ O que o Nominatim resolve

O Nominatim é um serviço de **geocodificação** baseado em OpenStreetMap. Ele resolve os seguintes problemas:

### 🔹 Geocodificação (endereço → coordenadas)
Transforma endereços textuais em latitude/longitude.
```bash
"Av. Paulista, São Paulo" → (-23.5614, -46.6559)
```

### 🔹 Reverse geocoding (coordenadas → endereço)
Converte coordenadas em endereços legíveis.
```bash
(-12.9714, -38.5014) → "Salvador, Bahia, Brasil"
```

### 🔹 Busca geográfica
Localiza cidades, bairros, ruas e pontos de interesse (POIs) com base em palavras-chave.
```bash
?q=farmácia+em+Copacabana
```

### 🔹 Integração com sistemas
Permite incorporar dados geográficos em sistemas internos, sem depender de APIs comerciais.

### 🔹 Uso em rastreamento
Traduz coordenadas de GPS em endereços para relatórios, mapas e monitoramento de veículos.

### 🔹 Atualização contínua
Pode ser configurado para atualizar os dados do Brasil diariamente com os dumps do OpenStreetMap.

---

## ❌ O que o Nominatim não resolve

Apesar de poderoso, o Nominatim possui limitações importantes:

### 🔸 Não oferece visualização de mapas
Não possui interface gráfica ou mapas interativos.  
Para isso, use bibliotecas como **Leaflet.js** ou **OpenLayers**.

### 🔸 Não calcula rotas
Não possui motor de navegação.  
Para isso, use **OSRM** ou **GraphHopper**.

### 🔸 Não desenha cercas ou polígonos
Não permite desenhar áreas geográficas diretamente.  
Isso é feito com bibliotecas de mapas interativos.

### 🔸 Não substitui serviços como Google Maps
Não possui recursos prontos de navegação, trânsito, rotas otimizadas ou visualização integrada.

---

## 🧩 Como complementar o Nominatim

Para montar um sistema completo, combine:

- **Nominatim** → geocodificação e busca
- **Leaflet.js** → mapas interativos e desenho de pontos/cercas
- **OSRM** → cálculo de rotas
- **OpenStreetMap** → base de dados geográficos

---

## ✅ Em resumo

O Nominatim resolve problemas de **localização, busca e integração de dados geográficos**, mas precisa ser combinado com outras ferramentas para oferecer visualização, navegação e interatividade.
