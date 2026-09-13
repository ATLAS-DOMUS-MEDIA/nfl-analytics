============================================================
PROMPT MESTRE — NFL ANALYTICS
SISTEMA DE ANÁLISE ESTATÍSTICA DE MERCADOS DA NFL
============================================================

INSTRUÇÃO PRINCIPAL

Você deverá projetar e posteriormente implementar um sistema
profissional de análise estatística da NFL.

O sistema deverá transformar dados históricos e atuais em
estimativas probabilísticas para mercados esportivos da NFL,
comparar essas estimativas com as informações do mercado e
registrar os resultados para posterior avaliação e backtesting.

O projeto deverá priorizar:

1. CORREÇÃO
2. PRECISÃO
3. RASTREABILIDADE
4. REPRODUTIBILIDADE
5. QUALIDADE DOS DADOS
6. SEGURANÇA
7. ESCALABILIDADE
8. SIMPLICIDADE DE MANUTENÇÃO

============================================================
REGRA ABSOLUTA SOBRE CUSTOS
============================================================

TODAS as fontes de dados, APIs, bibliotecas, frameworks,
serviços externos e ferramentas deverão priorizar alternativas
GRATUITAS.

Nenhuma API paga pode virar dependência estrutural do sistema.
O sistema deve funcionar mesmo sem ela. Uma API comercial,
quando necessária futuramente, entra como provider substituível,
e não como fundamento do projeto.

============================================================
1. OBJETIVO
============================================================

Criar uma plataforma de análise estatística da NFL capaz de:

- coletar dados;
- armazenar dados;
- validar dados;
- normalizar dados;
- construir indicadores;
- construir features;
- estimar distribuições;
- calcular probabilidades;
- receber linhas;
- receber odds;
- calcular probabilidade do mercado;
- calcular vantagem da previsão;
- calcular retorno estimado;
- calcular nível de confiança;
- explicar previsões;
- registrar previsões;
- registrar resultados reais;
- realizar backtesting;
- medir desempenho dos modelos;
- comparar modelos;
- permitir expansão para novos mercados.

O sistema NÃO deverá afirmar que uma aposta é garantida.
Toda saída deverá ser tratada como estimativa estatística.

============================================================
2. STACK DEFINITIVA
============================================================

Backend:
- Python 3.14+
- FastAPI
- Validação: Pydantic
- ORM: SQLAlchemy 2.x
- Migrações: Alembic
- Processamento: Polars, NumPy
- Estatística: SciPy
- Machine Learning: scikit-learn

Banco:
- PostgreSQL

Cache:
- Redis

Frontend:
- React
- Next.js
- TypeScript
- Visualização: Plotly (compatível com React)

Testes:
- pytest

Execução:
- Scheduler + Worker (open source)

============================================================
3. MVP: PASSING YARDS DE QUARTERBACKS
============================================================

O primeiro mercado será exclusivamente PASSING YARDS.

Entrada:
- game_id
- player_id
- market_type
- line
- selection
- bookmaker
- odd
- prediction_timestamp

Saída:
- prediction_id
- system_probability
- market_probability
- prediction_advantage
- estimated_return
- confidence_level
- uncertainty_interval
- sample_size
- model_name
- model_version
- prediction_timestamp
- factors
- status

============================================================
4. FONTES DE DADOS — GRATUITAS
============================================================

Dados Históricos:
- NFLverse (R package, dados públicos)
- nfl_data_py (Python wrapper)

Odds Atuais:
- The Odds API (plano gratuito)
- Alternativas: web scraping (com respeito a robots.txt)

Architecture:
- DataProvider (interface genérica)
- OddsProvider (interface genérica)
- Adapters substituíveis

============================================================
5. ARQUITETURA GERAL
============================================================

                 SISTEMA NFL
                      │
             ┌────────┴────────┐
             │                 │
       Dados estatísticos     Odds
             │                 │
       ┌─────┴─────┐     ┌─────┴────────┐
       │           │     │              │
   nflverse    Provider   Odds API   Outro Provider
               futuro

Fluxo de Dados:
RAW DATA → VALIDATION → NORMALIZATION → FEATURES → MODEL → PROBABILITY → BACKTESTING

Banco de Dados:
- Schemas: raw, app, analytics, audit
- Storage RAW: Parquet files
- Metadata: PostgreSQL

Cache:
- Redis para odds (TTL: 30-60s)
- Redis para jogos (TTL: 60s)
- Redis para previsões (TTL: 5min)

============================================================
6. REGRAS DE NEGÓCIO CRÍTICAS
============================================================

UUID v7 como PK (nunca ID externo como PK)
Timezone UTC (TIMESTAMPTZ no banco)
Nenhum arredondamento em cálculos (apenas na exibição)
Data Leakage: ZERO tolerância
Múltiplas fontes: preservar conflitos, não sobrescrever
Amostra mínima: por mercado, não universal
Idempotência: todas as previsões requerem Idempotency-Key

============================================================
7. ENTIDADES PRINCIPAIS
============================================================

seasons
teams
players
games
player_game_stats
team_game_stats
data_sources
raw_objects
data_ingestion_runs
markets
bookmakers
market_lines
odds
model_versions
prediction_features
predictions
prediction_results
prediction_snapshots
backtests
backtest_predictions

============================================================
8. PRÓXIMAS FASES
============================================================

FASE 1: Requisitos ✓
FASE 2: Entradas e saídas
FASE 3: Arquitetura detalhada
FASE 4: Modelo conceitual
FASE 5: Modelo lógico
FASE 6: Modelo físico (SQL)
FASE 7: Data layer (SQLAlchemy)
FASE 8: MVP Passing Yards
FASE 9: Modelo estatístico
FASE 10: Backtesting
FASE 11: API
FASE 12: Frontend
FASE 13: Testes
FASE 14: Novos mercados

============================================================
