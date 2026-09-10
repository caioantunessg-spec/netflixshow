# 🎬 Análise do Catálogo Netflix

Projeto de portfólio em Dados — análise exploratória do catálogo de filmes
e séries da Netflix, usando dados reais públicos.

## 🎯 Objetivo

Simular a demanda de um time de conteúdo de streaming que precisa entender
o catálogo atual: composição (filme x série), crescimento ao longo do
tempo, países e gêneros predominantes, classificação etária e padrões de
duração.

## ❓ Perguntas de negócio respondidas

- Quantos títulos existem no catálogo? Quantos são filmes e quantos são séries?
- Como o catálogo cresceu ano a ano?
- Quais países produzem mais conteúdo?
- Quais gêneros são mais comuns?
- Qual é a classificação etária mais frequente?
- Qual a duração média dos filmes e o número médio de temporadas das séries?
- A Netflix adiciona majoritariamente conteúdo recém-lançado ou catálogo antigo?

## 📊 Dataset

**Netflix Movies and TV Shows** (Kaggle) — [link do dataset]
- 8.807 títulos
- Colunas: `type`, `title`, `director`, `cast`, `country`, `date_added`,
  `release_year`, `rating`, `duration`, `listed_in`, `description`

## 🛠️ Tecnologias

- **Python** (Pandas) — exploração e limpeza dos dados
- **Matplotlib/Seaborn** — visualizações exploratórias
- **SQLite** — banco de dados para prática de SQL
- **SQL** — consultas de negócio
- **Power BI** — dashboard (em andamento)
- **Git/GitHub** — versionamento

## 📁 Estrutura do projeto

```text
netflixshow/
├── data/
│   ├── raw/                  # CSV original (não versionado)
│   └── netflix.db            # banco SQLite gerado (não versionado)
├── notebooks/
│   └── exploracao.ipynb      # pipeline completo: carga → limpeza → análise → SQL
├── powerbi/                  # dashboard (em andamento)
├── .gitignore
└── README.md
```

## 🧹 Limpeza de dados — decisões tomadas

| Coluna | Problema encontrado | Decisão |
|---|---|---|
| `director`, `cast`, `country` | Muitos valores nulos (dado ausente, não erro) | Preenchidos com `"Não informado"` em vez de remover a linha |
| `date_added` | Vinha como texto | Convertida para data com `pd.to_datetime` |
| `duration` | Misturava minutos (filme) e temporadas (série) na mesma coluna | Separada em duas colunas numéricas: `duracao_minutos` e `temporadas` |
| `country`, `listed_in` | Múltiplos valores na mesma célula (ex.: "US, India, France") | Colunas "explodidas" para contar cada país/gênero individualmente |
| `defasagem_anos` (calculada) | Alguns títulos com defasagem negativa entre lançamento e adição ao catálogo | Investigado: causado por `release_year` refletir o ano oficial de lançamento (não a data real de estreia — comum em títulos de dezembro). Mantidas as linhas; usada **mediana** em vez de média para evitar distorção |

## 🔎 Principais descobertas

## 🔎 Principais descobertas

- [ ] % de filmes x séries no catálogo
- [ ] Ano com mais títulos adicionados
- [ ] Top 3 países com mais produções
- [ ] Top 3 gêneros mais comuns
- [ ] Classificação etária mais frequente
- [x] A Netflix adiciona majoritariamente conteúdo recém-lançado: metade do
      catálogo entra até 1 ano após o lançamento original (mediana = 1 ano)
- [x] Identificada uma particularidade nos dados: alguns títulos têm
      `release_year` posterior à data real de adição, por conta de
      lançamentos em dezembro rotulados com o ano seguinte — tratado
      usando mediana em vez de média para evitar distorção

*(itens ainda com [ ] serão preenchidos conforme forem confirmados no notebook)*


## 🗃️ SQL

Consultas praticadas no SQLite (`data/netflix.db`, tabela `titulos`):

- [x] Total de títulos
- [ ] Filmes x séries
- [ ] Top 10 anos com mais lançamentos
- [ ] Distribuição por classificação etária
- [ ] Duração média de filmes
- [ ] Filmes recentes (pós-2015)
- [ ] Séries com mais de 5 temporadas
- [ ] Títulos sem diretor informado

## 📈 Dashboard (Power BI)

*Em andamento — 1 página com cards (total de títulos, filmes, séries,
duração média), gráfico de títulos por ano, top gêneros e top países.*

## ▶️ Como rodar

```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```
1. Baixe o dataset em `data/raw/netflix_titles.csv`
2. Rode `notebooks/exploracao.ipynb` do início ao fim

## 🚀 Próximo passo

Este é meu primeiro projeto de portfólio em Dados — um dataset simples,
de uma tabela só, para treinar Python, SQL e Power BI antes de avançar
para um projeto mais complexo: análise de e-commerce com o dataset
relacional da Olist, aplicando modelagem dimensional (Star Schema) e SQL
avançado (JOINs, window functions).

---
Desenvolvido por Caio Antunes