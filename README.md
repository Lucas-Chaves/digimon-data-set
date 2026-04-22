# Digimon Data Set

Projeto para extrair dados da Digi-API, salvar arquivos brutos em JSON, transformar uma amostra em CSV e carregar tudo em um banco PostgreSQL com relacionamentos.

## Estrutura do projeto
```
.
├── digimon_data.ipynb
├── requirements.txt
└── data/
    ├── raw/
    │   ├── attributes.json
    │   ├── digimons.json
    │   ├── fields.json
    │   ├── levels.json
    │   ├── skills.json
    │   └── types.json
    └── processed/
        └── digimons.csv
```

## Requisitos
- Python 3.10+
- PostgreSQL em execucao
- Dependencias Python:
  - requests
  - pandas
  - psycopg2-binary

Instalacao:
```bash
pip install -r requirements.txt
```

## Configuracao do banco
As celulas do notebook usam estas variaveis de ambiente:

- `PGHOST` (padrao: `localhost`)
- `PGPORT` (padrao: `5432`)
- `PGDATABASE` (padrao: `digimon_db`)
- `PGUSER` (padrao: `postgres`)
- `PGPASSWORD` (sem padrao)
- `PGMAINTENANCE_DB` (padrao: `postgres`, usada para criar `PGDATABASE` quando necessario)

Exemplo no PowerShell:
```powershell
$env:PGHOST="localhost"
$env:PGPORT="5432"
$env:PGDATABASE="digimon_db"
$env:PGUSER="postgres"
$env:PGPASSWORD="SUA_SENHA"
```

Se `PGPASSWORD` nao estiver definida, o notebook solicita a senha interativamente.

## Fluxo no notebook
Execute as celulas nesta ordem:

1. Importacoes e funcoes utilitarias.
2. Extracao da API para `data/raw/`:
   - attribute
   - field
   - level
   - type
   - skill
   - digimon
3. Transformacao para `data/processed/digimons.csv`.
4. Carga no PostgreSQL:
   - cria o banco automaticamente se nao existir
   - cria tabelas lookup e tabela principal `digimons`
   - cria tabelas de relacionamento:
     - `digimon_levels`
     - `digimon_types`
     - `digimon_attributes`
     - `digimon_fields`
     - `digimon_skills`
     - `digimon_prior_evolutions`
     - `digimon_next_evolutions`

## Consultas uteis
Para ver apenas dados da tabela principal:
```sql
SELECT d.*
FROM public.digimons AS d
ORDER BY d.id
LIMIT 5;
```

Para ver Digimon com relacionamentos, use JOIN/AGGREGATE (ja existe celula de validacao no notebook com exemplo pronto).

## Solucao de problemas
- Erro `no password supplied`:
  - defina `PGPASSWORD` ou informe a senha quando o notebook solicitar.

- Erro `database "digimon_db" does not exist`:
  - a celula de carga tenta criar automaticamente o banco usando `PGMAINTENANCE_DB`.
  - confirme se o usuario tem permissao para `CREATE DATABASE`.

- Tabela relacional vazia:
  - execute novamente a extracao da API antes da carga.
  - confirme se os arquivos em `data/raw/` foram atualizados.