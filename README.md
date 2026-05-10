# Pipeline de Vendas — Digital College

Pipeline completo de dados com extração, DW, Data Lake, Data Mart e dashboard interativo.

## Descrição

Projeto desenvolvido na Aula 14 da Formação Python para Dados da Digital College.  
Implementa uma cadeia completa de dados: do PostgreSQL transacional ao dashboard interativo com Dash/Plotly, passando por Amazon Redshift, HDFS e Data Mart com dimensão geográfica.

## Arquitetura

```
PostgreSQL (fonte)
    ↓
Amazon Redshift (DW)
    ↓
HDFS / Data Lake (Parquet)
    ↓
PostgreSQL (Data Mart)
    ↓
Dashboard Dash/Plotly (porta 8050)
```

## Tecnologias

| Ferramenta | Finalidade |
|---|---|
| Python + pandas + SQLAlchemy | Extração, transformação e carga |
| Amazon Redshift | Data Warehouse com dimensões e fato |
| HDFS + pyarrow | Data Lake em formato Parquet |
| PostgreSQL | Data Mart agregado |
| Dash + Plotly | Dashboard interativo |
| Docker + docker-compose | Containerização do dashboard |
| Apache Airflow | Orquestração do pipeline |
| Git + GitHub | Versionamento do código |

## Pré-requisitos

- Python 3.10+
- Docker e docker-compose instalados
- Acesso ao banco PostgreSQL de origem
- Acesso ao Amazon Redshift
- HDFS disponível

## Como rodar localmente

### 1. Clone o repositório

```bash
git clone https://github.com/fernandapeyxoto01-rgb/pipeline-vendas-digital-college.git
cd pipeline-vendas-digital-college
```

### 2. Configure o .env

```bash
cp .env.example .env
```

Edite o arquivo `.env` com suas credenciais:

```
DASHBOARD_DATABASE_URL=postgresql://usuario:senha@host:porta/banco
```

### 3. Instale as dependências

```bash
pip install -r requirements.txt
```

### 4. Rode o dashboard

```bash
python app.py
```

Acesse em: [http://localhost:8050](http://localhost:8050)

### 5. Ou rode com Docker

```bash
docker-compose up
```

## Configuração do .env

| Variável | Descrição |
|---|---|
| `DASHBOARD_DATABASE_URL` | URL de conexão com o banco do Data Mart (PostgreSQL) |

Consulte o arquivo `.env.example` para o template completo.

## Estrutura do repositório

```
├── app.py                  # Dashboard Dash/Plotly
├── analise.ipynb           # Notebook com todas as etapas do pipeline
├── dags/
│   └── pipeline_vendas.py  # DAG do Apache Airflow
├── Dockerfile              # Containerização do dashboard
├── docker-compose.yml      # Orquestração dos containers
├── requirements.txt        # Dependências Python
├── script_redshift.sql     # Scripts SQL do Redshift
├── .env.example            # Template de variáveis de ambiente
└── .gitignore              # Arquivos ignorados pelo Git
```

## Dashboard

O painel exibe:
- **KPIs**: Receita Real, Meta Esperada, Qtde Vendida, % Atingimento e Melhor Mês
- **Receita Real vs Esperada** por mês
- **% Atingimento da Meta** por mês
- **Quantidade Vendida** por mês
- **Desvio Real − Esperado** por mês
- **Top 10 Estados** por receita
- **Top 10 Cidades** por receita

Todos os gráficos respondem ao filtro de ano no cabeçalho.

---

Formação Python para Dados — Digital College · Atividade Pós Aula 14
