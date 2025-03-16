# IA_AzureCognitiveSearchTestDio

# Azure Cognitive Search - Guia Básico

Este repositório contém um guia básico para iniciar um projeto com o **Azure Cognitive Search**, utilizando **AI Search** para indexação e consulta de dados.

##  Pré-requisitos
Antes de começar, certifique-se de ter:
- Uma conta ativa no [Microsoft Azure](https://azure.microsoft.com/)
- Criado um serviço do **Azure Cognitive Search**
- Conhecimento básico sobre APIs e requisições HTTP

##  Criando um Serviço no Azure Cognitive Search

### 1️⃣ Criar um Recurso no Azure
1. Acesse o [Portal do Azure](https://portal.azure.com/)
2. No menu de navegação, clique em **Criar um recurso**
3. Pesquise por **Azure Cognitive Search** e selecione a opção correspondente
4. Clique em **Criar**
5. Preencha os detalhes:
   - **Grupo de Recursos**: Escolha um existente ou crie um novo
   - **Nome do Serviço**: Defina um nome único
   - **Região**: Escolha a mais próxima de sua localização
   - **Plano de Tarifas**: Escolha um plano adequado (o gratuito é recomendado para testes)
6. Clique em **Revisar e Criar**, depois **Criar**
7. Após a criação, copie a **Chave de Administração** e o **Endpoint** disponíveis na página do serviço

### 2️⃣ Criando um Índice no Azure Cognitive Search

1. Acesse o **Azure Cognitive Search** pelo portal do Azure
2. Clique em **Índices** e depois em **Criar um índice**
3. Defina um nome para o índice (ex: `meu-indice`)
4. Defina os campos do índice, por exemplo:
   - `id` (String, Chave Primária)
   - `titulo` (String, Pesquisável e Filtrável)
   - `descricao` (String, Pesquisável)
   - `data_publicacao` (DateTime, Ordenável)
5. Salve o índice

## 🔎 Indexando e Consultando Dados

### 🔹 Adicionar Documentos ao Índice (via API)
```bash
curl -X POST "<YOUR_SEARCH_ENDPOINT>/indexes/meu-indice/docs/index?api-version=2023-07-01-Preview" \
     -H "Content-Type: application/json" \
     -H "api-key: <YOUR_ADMIN_KEY>" \
     --data-raw '{
       "value": [
         { "@search.action": "upload", "id": "1", "titulo": "Azure Cognitive Search", "descricao": "Um poderoso mecanismo de busca AI", "data_publicacao": "2025-03-16T12:00:00Z" }
       ]
     }'
```

### 🔹 Consultando o Índice (via API)
```bash
curl -X GET "<YOUR_SEARCH_ENDPOINT>/indexes/meu-indice/docs?api-version=2023-07-01-Preview&search=Azure" \
     -H "api-key: <YOUR_ADMIN_KEY>"
```

### 🔹 Exemplo de Busca com Python
```python
import requests
import json

endpoint = "<YOUR_SEARCH_ENDPOINT>/indexes/meu-indice/docs?api-version=2023-07-01-Preview&search=Azure"
api_key = "<YOUR_ADMIN_KEY>"

headers = {"api-key": api_key, "Content-Type": "application/json"}
response = requests.get(endpoint, headers=headers)
print(json.dumps(response.json(), indent=2))
```

##  Referências
- [Documentação Oficial do Azure Cognitive Search](https://learn.microsoft.com/en-us/azure/search/)
- [Tutoriais e Exemplos](https://learn.microsoft.com/en-us/azure/search/search-what-is-azure-search)
